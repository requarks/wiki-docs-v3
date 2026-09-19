---
title: Custom Blocks
description: Create your own content blocks
published: true
date: '2026-09-19T07:30:54.114Z'
tags:
  - dev
editor: markdown
dateCreated: '2026-09-19T03:07:35.984Z'
---

# Overview

Write your own custom content blocks for use in your personal wiki, your organization or to be shared with the community.
Content blocks are built using web standards and offer infinite flexibility.

# Getting Started

::block-steps
1. Clone the [repository](https://github.com/requarks/wiki)
    > [!IMPORTANT] Requirements
    > Either open the project inside the [devcontainer](/dev)
    > **or** install **Node.js 26.x or later** on your system
2. Open the `blocks` directory into your editor.
3. Create a new directory named `block-xyz` *(where `xyz` is the name of your custom block)*.
4. Inside this new directory, create a file named `component.js`.
5. Use one of the base templates below to write your block.
::

# Base Templates

:::block-tabs
::block-tab{label="Minimal Example"}
```js title=component.js
import { css, html, LitElement } from 'lit'

export class BlockExampleElement extends LitElement {
  /**
   * Read out of this file's AST at build time, so every value has to be a plain literal.
   *
   * `props` are the attributes an author may set: the picker builds its form from them, and anything
   * NOT listed here is stripped out of the page when it is saved.
   */
  static definition = {
    block: 'example',
    name: 'Example',
    description: 'A minimal block.',
    icon: 'plugin',
    props: [
      {
        name: 'title',
        type: 'string',
        label: 'Title',
        default: ''
      }
    ]
  }

  static get styles() {
    return css`
      /* -> Custom elements are inline by default, which is almost never what a block wants */
      :host {
        display: block;
      }

      /*
        The block's bottom margin goes on an element inside the shadow root, never on :host -- the app
        resets the margin on every element, and a page rule beats a :host rule whatever its
        specificity.
      */
      .box {
        margin-bottom: 16px;
      }
    `
  }

  static get properties() {
    return {
      title: { type: String }
    }
  }

  constructor() {
    super()
    this.title = ''
  }

  render() {
    return html`
      <div class="box">
        ${this.title ? html`<h3>${this.title}</h3>` : null}
        <!-- -> Where the body the author wrote between the block's opening and closing lines lands -->
        <slot></slot>
      </div>
    `
  }
}

window.customElements.define('block-example', BlockExampleElement)
```
::

::block-tab{label="Full Annotated Example"}
```js title=component.js
/**
 * A starting point for a block of your own.
 *
 * **The key is the identity, and three names have to agree**: the directory `block-example`, the
 * `block: 'example'` in the definition, and the element `<block-example>`. The packager refuses a
 * mismatch, since everything else is derived from that one word — so renaming the block is a matter
 * of replacing `example` and `Example` throughout, the element's name and this class's included.
 *
 * A block is a Lit component in a shadow root, which is what keeps the page's stylesheet out of it
 * and its own styles off the page. It loads only once its tag turns up in a page, so pulling in a
 * heavy library is fine — nobody who is not reading a page that uses it ever downloads it.
 *
 * Nothing here is required beyond `static definition` and `render()`. Delete the rest as you go.
 */

import { css, html, LitElement } from 'lit'
import { unsafeSVG } from 'lit/directives/unsafe-svg.js'

// Resolves an Iconify reference (`mdi:home`) to inline SVG, from this instance's own `/_icons` —
// never from Iconify itself, so a wiki that is offline still draws the icons it has been asked for
// before. `iconImageUrl` picks off an `img:` reference, which names a file rather than an icon.
// Only needed by a block that shows an icon the author picked.
import { fetchIcon, iconImageUrl } from '../shared/icons.js'

// Keeps a `dark` attribute on this element in step with the app's theme — see STYLES below. Always
// this, never `:host-context()`: only Chromium ever shipped that selector, so elsewhere a block
// silently stayed light on a dark page.
import { DarkMode } from '../shared/theme.js'

/**
 * Block Example
 */
export class BlockExampleElement extends LitElement {
  /**
   * ── DEFINITION ────────────────────────────────────────────────────────────────────────────────
   *
   * Metadata for the admin area and the editor's block picker. It is read out of this file's AST at
   * build time — the component itself cannot be imported outside a browser — and collected into the
   * manifest, or into the package.
   *
   * **Values must be plain literals.** No imports, no computed keys, no template interpolation; a
   * backtick string with nothing in it is fine and is the readable way to write a multi-line
   * template. Anything else fails the build.
   */
  static definition = {
    /** The key. Must match this directory's name, minus `block-`. Lowercase, digits and dashes. */
    block: 'example',

    /** What the admin area and the picker call it. */
    name: 'Example',

    /** One line, shown under the name in both places. */
    description: 'A starting point for a block of your own.',

    /**
     * An icon name from the app's bundled `ultraviolet-*` set, drawn in the editor's picker.
     * A block installed from a package always shows the generic `plugin` icon instead, since a
     * package cannot bring an icon with it — so this only matters for a block shipping with the wiki.
     */
    icon: 'plugin',

    /**
     * What the editor writes BETWEEN the opening and closing lines when inserting the block — the
     * starter body, for a block that takes content. Leave it out for one that does not.
     */
    template: 'Your content here.',

    /**
     * The same starter body written in AsciiDoc, for a template that spells STRUCTURE — nested
     * blocks, or a list with paragraphs hanging off its items — since AsciiDoc writes both
     * differently. Almost every block leaves this out, and leaving it out is a complete answer: a
     * body that is one fenced source is rewritten mechanically, and plain prose reads the same in
     * both syntaxes.
     */
    // asciidocTemplate: '...',

    /**
     * Names an editor for the block's BODY, which the markdown editor then offers as an
     * "Edit Content" lens beside "Edit Block Parameters". For a body that is a fenced source the
     * props form has nothing to say about — a diagram, a drawing. Most blocks name none.
     */
    // contentEditor: 'code',

    /**
     * The authorable attributes, which the picker turns into a form and the server turns into the
     * sanitiser's allow list for this tag. **A prop that is not declared here is stripped out of the
     * page when it is saved**, so every attribute an author may set has to be in this list.
     *
     * Five types: `string`, `number`, `boolean`, `select`, and `icon` (a string holding an Iconify
     * reference, offered with the app's icon picker).
     *
     * `default` is worth stating even where it repeats the constructor: it is what the editor treats
     * as "unset", so a field put back to its default writes nothing into the page.
     */
    props: [
      {
        name: 'title',
        type: 'string',
        label: 'Title',
        hint: 'Heading shown above the content. Leave empty for none.',
        default: ''
      },
      {
        name: 'count',
        type: 'number',
        label: 'Count',
        hint: 'How many times to say it.',
        default: 1
      },
      {
        name: 'showBorder',
        type: 'boolean',
        label: 'Show Border',
        hint: 'Draw a border around the block.',
        default: true
      },
      {
        name: 'tone',
        type: 'select',
        label: 'Tone',
        // -> Plain strings where the value IS the wording. Use `{ label, value }` where they differ:
        //    `{ label: 'Heading 3', value: '3' }`.
        options: ['neutral', 'info', 'warning'],
        default: 'neutral'
      },
      {
        name: 'icon',
        type: 'icon',
        label: 'Icon',
        hint: 'Drawn to the left of the title.',
        default: ''
      }
    ]
  }

  /**
   * ── STYLES ────────────────────────────────────────────────────────────────────────────────────
   *
   * Scoped to this shadow root, so class names cannot collide with the page or with another block.
   * Nothing from the article's stylesheet reaches in here either — which is the point, and also why
   * a block has to draw everything it needs.
   */
  static get styles() {
    return css`
      /* -> Custom elements are inline by default, which is almost never what a block wants */
      :host {
        display: block;
      }

      /*
        Theme colours come from the app as CSS custom properties -- var(--q-primary) below. The
        --q- prefix is historical; they are declared in frontend/src/css/tailwind.css and rewritten
        at runtime for per-site theming, so a block reading them follows the wiki it is installed on.
        Always give a fallback: the block is also drawn in the editor's preview.
      */
      .box {
        padding: 16px 20px;
        border-radius: 6px;
        background-color: var(--example-bg);
        color: var(--example-fg);
      }
      .box.has-border {
        border: 1px solid var(--example-border);
      }

      /*
        The gap below a block lives on this element, not on :host.

        The app resets the margin on every element, and a rule in the page beats a :host rule in the
        shadow tree whatever its specificity -- so a margin set on the host is simply dropped. Set
        inside the shadow root it is out of that rule's reach, and collapses out through the host,
        which carries no padding or border of its own.
      */
      .box {
        margin-bottom: 16px;
      }

      .title {
        display: flex;
        align-items: center;
        gap: 8px;
        margin-bottom: 8px;
        font-weight: 500;
        color: var(--q-primary, #1976d2);
      }

      .title svg,
      .title img {
        width: 20px;
        height: 20px;
      }

      /*
        Dark mode. The DarkMode controller in the constructor puts a "dark" attribute on this element
        whenever the app is dark, and takes it off again -- so the two rules below are the whole of
        it, and the rest of the stylesheet never mentions the theme.

        Declaring the colours as custom properties in one place, rather than restating every rule
        under :host([dark]), is what keeps those two rules the only thing to keep in step.
      */
      :host {
        --example-bg: #f5f5f5;
        --example-fg: #424242;
        --example-border: #e0e0e0;
      }
      :host([dark]) {
        --example-bg: #161b22;
        --example-fg: rgba(255, 255, 255, 0.75);
        --example-border: rgba(255, 255, 255, 0.15);
      }

      /* -> A prop that changes appearance rather than content is a class, not a second render() */
      .box.tone-info {
        --example-border: #1976d2;
      }
      .box.tone-warning {
        --example-border: #f57c00;
      }
    `
  }

  /**
   * ── PROPERTIES ────────────────────────────────────────────────────────────────────────────────
   *
   * One entry per prop above, plus whatever internal state the block keeps. Lit re-renders when any
   * of them changes.
   *
   * Names are declared in camelCase and written in the page in camelCase, and Lit observes the
   * lowercased form (`showborder`) — which is the same attribute as far as HTML is concerned, so
   * there is nothing to configure. Don't set `attribute:` to work around it.
   *
   * `{ state: true }` marks a property as this block's own business: it is not an attribute, does not
   * appear in the page, and is where the results of a fetch or a click belong.
   */
  static get properties() {
    return {
      /** @type {string} */
      title: { type: String },
      /** @type {number} */
      count: { type: Number },
      /** @type {boolean} */
      showBorder: { type: Boolean },
      /** @type {string} */
      tone: { type: String },
      /** @type {string} */
      icon: { type: String },

      // Internal state
      _iconSvg: { state: true }
    }
  }

  constructor() {
    super()
    // -> Defaults, matching the definition's. An attribute the author did not write is absent from
    //    the markup entirely, so this is what the block is actually drawn with.
    this.title = ''
    this.count = 1
    this.showBorder = true
    this.tone = 'neutral'
    this.icon = ''
    this._iconSvg = ''

    // -> Puts `dark` on this element for the styles above to key off. A block that has to ACT on the
    //    change rather than restyle for it passes `{ onChange: (dark) => … }`, or reads
    //    `this._darkMode.isDark` at the moment it needs it — redrawing a library's canvas in its own
    //    dark theme, say.
    this._darkMode = new DarkMode(this)
  }

  /**
   * ── LIFECYCLE ─────────────────────────────────────────────────────────────────────────────────
   *
   * `connectedCallback` runs when the element enters the page, `disconnectedCallback` when it
   * leaves — anything started in the first has to be stopped in the second, since a reader moving
   * between pages is a router transition and this element is thrown away without a reload.
   *
   * `willUpdate(changed)` runs before each render, for work that depends on a prop: recomputing a
   * derived value, or kicking off a fetch when the prop it reads has actually changed. Guard on
   * `changed.has('...')` or it runs on every keystroke in the editor's preview.
   */
  connectedCallback() {
    super.connectedCallback()
    // this._timer = setInterval(() => this.requestUpdate(), 1000)
  }

  disconnectedCallback() {
    super.disconnectedCallback()
    // clearInterval(this._timer)
  }

  willUpdate(changed) {
    // -> Guarded, or this runs on every keystroke in the editor's preview
    if (changed.has('icon')) {
      // -> Resolving an icon is a fetch, so it lands in state and draws on the render after this
      //    one. `fetchIcon` answers '' for anything it cannot serve: a missing icon is a block
      //    without one, not a block that breaks.
      this._iconSvg = ''
      if (this.icon && !iconImageUrl(this.icon)) {
        fetchIcon(this.icon).then((svg) => {
          this._iconSvg = svg
        })
      }
    }
  }

  /** The chosen icon: an `<img>` for an `img:` reference, the fetched SVG for everything else. */
  _icon() {
    const image = iconImageUrl(this.icon)
    if (image) {
      return html`<img src="${image}" alt="" />`
    }
    // -> `unsafeSVG` because this markup is an SVG document, not a value. It came from this wiki's
    //    own icon endpoint; never reach for it with a string built out of a prop.
    return this._iconSvg ? unsafeSVG(this._iconSvg) : null
  }

  /**
   * ── RENDER ────────────────────────────────────────────────────────────────────────────────────
   *
   * Runs on every property change. Keep it a function of the properties and nothing else — no
   * reading the DOM, no side effects — and Lit patches only what actually differs.
   *
   * `<slot></slot>` is where the block's BODY goes, i.e. whatever the author wrote between the
   * opening and closing lines in the page. Leave it out for a block that takes no content.
   *
   * `unsafeHTML` and `unsafeSVG` exist and are almost always the wrong answer: a string built out of
   * a prop and inserted as markup is an injection, and the wiki's sanitiser never saw it. Interpolate
   * values as values — `${this.title}` escapes — and keep the unsafe directives for markup you
   * produced yourself, such as the SVG that came back from `fetchIcon` above.
   */
  render() {
    const classes = ['box', `tone-${this.tone}`, this.showBorder ? 'has-border' : ''].join(' ')

    return html`
      <div class="${classes}">
        ${
          this.title || this.icon
            ? html`<div class="title">${this._icon()}${this.title}</div>`
            : null
        }
        <div class="content">
          <slot></slot>
        </div>
        ${this.count > 1 ? html`<p>Said ${this.count} times.</p>` : null}
      </div>
    `
  }
}

/**
 * ── REGISTRATION ────────────────────────────────────────────────────────────────────────────────
 *
 * The tag is `block-` plus the definition's key, and registering it is what makes the file do
 * anything — the wiki loads this module by URL and nothing else calls into it.
 */
window.customElements.define('block-example', BlockExampleElement)

/*
  ── TWO MORE FILES, IF YOU NEED THEM ──────────────────────────────────────────────────────────────

  `worker.js` beside this one is compiled as a second entry point, to `block-example.worker.js`, for
  work that must come off the page's thread. A worker is loaded by URL rather than imported, so it
  cannot be part of the bundle that starts it:

      new Worker(new URL('block-example.worker.js', import.meta.url), { type: 'module' })

  `assets.json` beside this one lists directories of runtime data files to copy to
  `block-example/…` — for a library that deliberately keeps part of itself out of the bundle and
  fetches it only when a document turns out to need it. A package subpath, or `./something` for a
  directory of your own, mapped to the name it should have:

      { "somelib/cmaps": "cmaps", "./data": "data" }

  Both end up inside the package, and are served beside the block at `/_blocks/`.
*/

```
::
:::

# Reference

A block is a [Lit component](https://lit.dev/docs/components/overview/), with it's own logic, template, styles and internal state.
Lit components are standard [Web Components](https://developer.mozilla.org/en-US/docs/Web/API/Web_components) and are compatible with all modern browsers.

At its core, a block must extend a LitElement and export it in the window `customElements`:
```js
export class BlockExampleElement extends LitElement {
  ...
}
window.customElements.define('block-example', BlockExampleElement)
```

## Definition

A static `definition` object describes the configuration of the block.

| Attribute | Description | Example Value |
| :-- | :-- | :-- |
| block | The key. Must match this directory's name, minus `block-`. Lowercase, digits and dashes. | `example` |
| name | The human readable name, shown in the admin and block picker. | `My Example` |
| description | A short description of the block, shown in the admin and block picker. | `An example block that does X and Y.` |
| icon | Icon key matching one of the bundled `ultraviolet-*` icons. Use `plugin` by default. | `plugin` |
| template | Sample content that gets inserted between the opening and closing tags of your block. **Omit if not needed.** | `Your content here.` |
| asciidocTemplate | Sample content but in AsciiDoc syntax. **Omit if the same as template or not needed.** |  |
| contentEditor | The editor to use to edit the content of the block. **Omit unless your block has nested code that needs an editor.** |  |
| props | An array of properties the user can configure when inserting your block. **See reference below.** | `[]` |
{.table-leading-col}

### Props

The `props` attribute describes what the user can change. Only properties defined here are presented as a form to the user and saved alongside the page content.

| Attribute | Description | Example Value |
| :-- | :-- | :-- |
| name | The property key, in camelCase. | `myCustomProperty` |
| type | The type of the property: `string`, `number`, `boolean`, `select` or `icon` | `string` |
| label | The human readable title of the property. | `My Custom Property` |
| hint | A short helper text or description of the property. | `Heading shown above the content. Leave empty for none.` |
| options | **For select properties only**, an array of strings or objects the user can choose from. | `['abc', 'def', 'ghi']`<br>or<br>`[{ label: 'Option A', value: 'abc'}, {label: 'Option B', value: 'def'}]` |
| default | The default value. This should always be set, even if empty, false or 0. | `abc` |
{.table-leading-col}

## Properties

The static `properties()` method holds the internal state of the block. It **MUST** include all the props defined in the definition above.

Refer to the [Lit Reactive Properties Documentation](https://lit.dev/docs/components/properties/) on how to define properties and the internal state.

## Styles

CSS is embedded using the static `styles()` method. Styles are scoped to the block element, so there's no possible conflict with the page or other blocks.

Refer to the [Lit Styles Documentation](https://lit.dev/docs/components/styles/) for more details.

```js
static get styles() {
  return css`
    /* -> Custom elements are inline by default, which is almost never what a block wants */
    :host {
      display: block;
    }

    .something {
      padding: 16px;
      border-radius: 5px;
      background-color: var(--example-bg);
      color: var(--example-fg);
    }

    /*
      Dark mode. The DarkMode controller in the constructor puts a "dark" attribute on this element
      whenever the app is dark, and takes it off again -- so the two rules below are the whole of
      it, and the rest of the stylesheet never mentions the theme.

      Declare the colours as custom properties in one place, rather than restating every rule under :host([dark])
    */
    :host {
      --example-bg: #f5f5f5;
      --example-fg: #424242;
    }
    :host([dark]) {
      --example-bg: #161b22;
      --example-fg: rgba(255, 255, 255, 0.75);
    }
  `
}
```

## Render

The `render()` method is responsible for generating the HTML template.

Refer to the [Lit Rendering Documentation](https://lit.dev/docs/components/rendering/) for more details.

```js
render() {
  return html`<p>Hello from my template.</p>`;
}
```

## Advanced Capabilities

Your block can use much more advanced capabilities like [lifecycle methods](https://lit.dev/docs/components/lifecycle/), [handling events](https://lit.dev/docs/components/events/), work with the [ShadowDOM](https://lit.dev/docs/components/shadow-dom/), [templates expressions](https://lit.dev/docs/templates/overview/), [async tasks](https://lit.dev/docs/data/task/) and more.

Refer to the [Lit Components Documentation](https://lit.dev/docs/components/overview/) for more details.

## Worker

For use cases where a worker is used to offload processing off the page's thread, it can be registered by naming it `worker.js` and place it alongside `component.js`.

A worker is loaded by URL rather than imported, so it cannot be part of the bundle that starts it. Once installed in a wiki, it becomes accessible as `block-example.worker.js` (where `example` is the name of your block) alongside your block, e.g.:

```js
new URL('block-example.worker.js', import.meta.url).href
```

## Assets

Your block may contain additional runtime data files like libraries, fonts, images, etc. where including them in the component directly doesn't make sense.

Create an `assets.json` file alongside your `component.js` which contains the list of directories/files to bundle.

Each property corresponds to a `"source": "destination"` pair. The source can be either a directory or a file, e.g.:

```json
{
  "data/reference.csv": "reference.csv"
  "images": "images",
  "libs/foobar": "foobar",
  "ics/current": "ics/current"
}
```

All 4 directories/files will end up inside the package, and be served from `/_blocks/block-example/`.

> [!CAUTION]
> - **DO NOT** include `component.js` or `worker.js` in the `assets.json` file. They are already bundled automatically during packaging.
> - **AVOID** bundling large files as part of the block. Large files should instead be hosted elsewhere and have your block load them remotely asynchronously.

# Packaging

Once your custom block is ready, it's time to package it so that it can be installed into a Wiki.js instance.

From the `./blocks` directory, run the command *(replacing `example` with the name of your block)*:
```sh
npm run package -- block-example
```

A `.wkblock` file will be generated and stored in the `packages` subdirectory. It contains everything necessary to install your custom block.


