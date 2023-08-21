---
weight: 2
draft: false
---

# `rasterize()`

Rasterize quadrille according to upper-left corner vertex `pattern0`, bottom-left corner vertex `pattern1`, upper-right corner vertex `pattern2`, and bottom-right corner vertex `pattern3`,  using (fragment) `shader`. Call [rasterizeTriangle()]({{< ref "rasterize_triangle" >}}) on the two non-overlapping triangles entirely covering the quadrille.

# Example

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="425" height="425" >}}
`use strict`;
const ROWS = 20;
const COLS = 20;
const LENGTH = 20;
let quadrille;

function setup() {
  createCanvas(COLS * LENGTH, ROWS * LENGTH);
  quadrille = createQuadrille(20, 20);
  // /*
  quadrille.rasterize(colorizeShader,
                      [255, 0, 0],
                      [0, 255, 0],
                      [0, 0, 255],
                      [255, 255, 0]);
  // */
  /*
  quadrille.rasterize(colorizeShader,
                      [255, 0, 0, 7, 4],
                      [0, 255, 0, -1, -10],
                      [0, 0, 255, 5, 8],
                      [255, 255, 0, -1, -10]);
  // */
}

function draw() {
  drawQuadrille(quadrille, { cellLength: LENGTH, outline: 'green' });
}

// /*
function colorizeShader({ pattern: rgb }) {
  return color(rgb);
}
// */

/*
// pretty similar to what p5.Quadrille.colorizeTriangle does
function colorizeShader({ pattern: mixin }) {
  let rgb = mixin.slice(0, 3);
  // debug 2d normal
  console.log(mixin.slice(3));
  // use interpolated color as is
  return color(rgb);
}
// */
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
  quadrille.rasterize(colorizeShader,
                      [255, 0, 0],
                      [0, 255, 0],
                      [0, 0, 255],
                      [255, 255, 0]);
}

function draw() {
  drawQuadrille(quadrille, { cellLength: LENGTH, outline: 'green' });
}

function colorizeShader({ pattern: rgb }) {
  return color(rgb);
}
```
{{< /details >}}

# Syntax

> `rasterize(shader, pattern0, [pattern1], [pattern2], [pattern3])`

# Parameters

| parameter | description                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------|
| shader    | Function: taking `{ pattern: interpolated_data_array, row: i, col: j }` params and returning a `p5.Color` |
| pattern0  | Array: corner0 attributes to be interpolated                                                              |
| pattern1  | Array: corner1 attributes to be interpolated default is pattern0                                          |
| pattern2  | Array: corner2 attributes to be interpolated default is pattern0                                          |
| pattern3  | Array: corner3 attributes to be interpolated default is pattern0                                          |