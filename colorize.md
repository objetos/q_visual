---
weight: 5
draft: false
title: colorize(args)
---

Colorize quadrille according to upper-left corner `color0`, bottom-left corner `color1`, upper-right corner `color2`, and bottom-right corner `color3` colors. Call [colorizeTriangle()]({{< ref "colorize_triangle" >}}) on the two non-overlapping triangles entirely covering the quadrille.

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
const ROWS = 20;
const COLS = 20;
const LENGTH = 20;
let quadrille;

function setup() {
  createCanvas(COLS * LENGTH, ROWS * LENGTH);
  quadrille = createQuadrille(20, 20);
  quadrille.colorize('red', 'green', 'blue', 'cyan');
}

function draw() {
  drawQuadrille(quadrille, { cellLength: LENGTH, outline: 'green' });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
const ROWS = 20;
const COLS = 20;
const LENGTH = 20;
let quadrille;

function setup() {
  createCanvas(COLS * LENGTH, ROWS * LENGTH);
  quadrille = createQuadrille(20, 20);
  quadrille.colorize('red', 'green', 'blue', 'cyan');
}

function draw() {
  drawQuadrille(quadrille, { cellLength: LENGTH, outline: 'green' });
}
```
{{< /details >}}

## Syntax

> `colorize(color0, [color1], [color2], [color3])`

## Parameters

| Param     | description                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| `color0`  | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner0 color to be interpolated                   |
| `color1`  | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner1 color to be interpolated default is `color0` |
| `color2`  | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner2 color to be interpolated default is `color0` |
| `color3`  | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner2 color to be interpolated default is `color0` |