---
title: >-
  Let custom blocks provide their own content editor to the "Edit Content"
  button
description: >-
  Background contentEditor is a first-class key of a block definition (spec:
  dev/specs/wkblock.md §5), and backend/helpers/wkblock.ts reads it off an
  imported package. But the only place the key is res…
published: true
date: '2026-11-21T07:43:43.504Z'
tags:
  - blocks
  - editing
editor: markdown
dateCreated: '2026-11-20T13:12:58.186Z'
---

**Background**

`contentEditor` is a first-class key of a block definition (spec: `dev/specs/wkblock.md` §5), and `backend/helpers/wkblock.ts` reads it off an imported package. But the only place the key is resolved - `BlockContentEditorOverlay.vue` - resolves it against a hardcoded, module-scoped registry:

 ```js
   const EDITORS = { bpmn: …, code: …, drawio: … }
   const editorComponent = computed(() => EDITORS[editorKey] ?? null)
 ```

 A custom block (`.wkblock`, installed via Admin → Content Blocks) cannot register in that registry. If its definition declares contentEditor: 'xyz', the "Edit Content" lens is offered by the editors, and opening it shows the red "unknown editor" card. So the canvas-style editing experience (like the DrawIO or ExcaliDraw) is only reachable by **patching and rebuilding the frontend SPA** of the target installation — which defeats the central promise of the `.wkblock` format: _an administrator uploads a file and nothing on the instance is rebuilt or restarted_.

**Proposal**

Add one fallback branch to the overlay's resolution: when editorKey is not in the built-in registry and the block is a custom block, load the editor from the block's own package:

 ```
   /_blocks/<blockKey>/<editorKey>.js
 ```

 The module would export a framework-agnostic factory, e.g.:

 ```js
   export function createEditor(container, { value, params, onChange, onApply }) → { destroy() }
 ```

The overlay then mounts it in one small generic wrapper (the same modelValue / params / save contract the registry components already follow), and the "unknown editor" card becomes the true fallback. The existing serving machinery needs no change: packages may already ship arbitrary files under block-<key>/**, they are served with no-cache + ETag, and a re-import upgrades the row - so an editor fix ships exactly like a block fix: one file re-upload, live immediately, no rebuild on any node.

Trust-wise this changes nothing: a `.wkblock` is code that runs in every reader's browser, installed by someone holding manage:sites - the same gate the raw head/body fields under Admin → Theme already open. An editor module is the same kind of code, arriving through a documented convention instead of a patched bundle.

**Concrete motivation: a bpmn-js block**

I'm developing a block-bpmn (custom block) that renders BPMN 2.0 diagrams with bpmn-js. The read-side renderer works perfectly as a pure .wkblock. The editing side, though, is a whole application bpmn-js Modeler plus the properties panel, over ~1 MB of JS — and it only works because I patch BlockContentEditorOverlay.vue in my own checkout. BPMN is one use case of mine, more popular js editors may follow.

With the proposed convention the block would simply ship:

 ```
   block-bpmn.js            ← renderer (NavigatedViewer)
   block-bpmn/bpmn.js       ← self-contained Modeler + properties panel, exports createEditor
 ```

…declare contentEditor: 'bpmn', and the "edit content" works on any installation with a single file upload. The heavy dependency stays inside the package (nothing new enters frontend/package.json), and every editor improvement is a re-upload rather than a rebuild.

**Scope**

I'd expect this to be small: one fallback branch in BlockContentEditorOverlay.vue, one generic `mount/unmount wrapper`, and a paragraph in the wkblock spec documenting the convention and the createEditor contract.
