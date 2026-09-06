---
title: Draw.io
description: A diagram drawn in draw.io, stored as its own XML and edited on a canvas.
published: true
date: '2026-09-06T00:57:16.838Z'
tags: []
editor: markdown
dateCreated: '2026-09-06T00:50:44.358Z'
---

# Description

A diagram drawn in draw.io, stored as its own XML and edited on a canvas.

# Demo

::block-drawio
```xml
<mxfile host="embed.diagrams.net">
  <diagram name="Page-1" id="0">
    <mxGraphModel dx="2432" dy="1341" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="850" pageHeight="1100" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-3" edge="1" parent="1" source="6mDFXCWUos-c4wh-Ew7k-1" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" target="6mDFXCWUos-c4wh-Ew7k-2">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-1" parent="1" style="ellipse;whiteSpace=wrap;html=1;shapeInside=1;aspect=fixed;fillColor=#dae8fc;strokeColor=#6c8ebf;" value="Node A" vertex="1">
          <mxGeometry height="80" width="80" x="30" y="30" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-5" edge="1" parent="1" source="6mDFXCWUos-c4wh-Ew7k-2" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" target="6mDFXCWUos-c4wh-Ew7k-4">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-2" parent="1" style="shape=hexagon;perimeter=hexagonPerimeter2;whiteSpace=wrap;html=1;shapeInside=1;fixedSize=1;" value="Node B" vertex="1">
          <mxGeometry height="80" width="120" x="170" y="30" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-10" edge="1" parent="1" source="6mDFXCWUos-c4wh-Ew7k-4" style="edgeStyle=orthogonalEdgeStyle;rounded=0;orthogonalLoop=1;jettySize=auto;html=1;entryX=1;entryY=0.5;entryDx=0;entryDy=0;" target="6mDFXCWUos-c4wh-Ew7k-8">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-4" parent="1" style="rhombus;whiteSpace=wrap;html=1;shapeInside=1;fillColor=#f8cecc;strokeColor=#b85450;strokeWidth=6;" value="" vertex="1">
          <mxGeometry height="80" width="80" x="345" y="30" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-6" parent="1" style="swimlane;fontStyle=0;childLayout=stackLayout;horizontal=1;startSize=30;horizontalStack=0;resizeParent=1;resizeParentMax=0;resizeLast=0;collapsible=1;marginBottom=0;whiteSpace=wrap;html=1;" value="List" vertex="1">
          <mxGeometry height="120" width="140" x="160" y="150" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-7" parent="6mDFXCWUos-c4wh-Ew7k-6" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;rotatable=0;whiteSpace=wrap;html=1;" value="Item 1" vertex="1">
          <mxGeometry height="30" width="140" y="30" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-8" parent="6mDFXCWUos-c4wh-Ew7k-6" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;rotatable=0;whiteSpace=wrap;html=1;" value="Item 2" vertex="1">
          <mxGeometry height="30" width="140" y="60" as="geometry" />
        </mxCell>
        <mxCell id="6mDFXCWUos-c4wh-Ew7k-9" parent="6mDFXCWUos-c4wh-Ew7k-6" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;rotatable=0;whiteSpace=wrap;html=1;" value="Item 3" vertex="1">
          <mxGeometry height="30" width="140" y="90" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>

```
::


# Parameters

| Parameter | Default Value | Example Value |
| :-- | :-- | :-- |
| `server` | `<none>` | `https://drawio.example.org` or leave empty for the public draw.io server. |
| `height` | `420` | `svg` or `png` |
| `caption` | `<none>` | `Some caption` |
| `align` | `left` | `center` or `left` |
{.table-leading-col .table-code-nohighlight}

# Default Code

````md
::block-drawio
```xml
<mxfile>
  <diagram name="Page-1">
    <mxGraphModel dx="800" dy="600" grid="1" gridSize="10" page="1" pageWidth="850" pageHeight="1100">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```
::
````

