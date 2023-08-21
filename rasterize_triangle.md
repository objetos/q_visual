---
weight: 4
draft: false
---

# `rasterizeTriangle()`

Rasterize the triangle defined by vertices `(row0, col0)`, `(row1, col1)`, and `(row2, col2)`, using [barycentric coordinates](https://fgiesen.wordpress.com/2013/02/06/the-barycentric-conspirac/). The user provided [software rendered](https://en.wikipedia.org/wiki/Software_rendering) [(fragment) shader](https://en.wikipedia.org/wiki/Shader) is a function parameterized with the object literal `{ pattern: interpolated_data_array, row: i, col: j }` and that should return a [p5.Color](https://p5js.org/reference/#/p5.Color). Refer to the [colorizeTriangle()]({{< ref "colorize_triangle" >}}) method for an example.

# Example

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="425" height="425" >}}
`use strict`;
const ROWS = 20;
const COLS = 20;
const LENGTH = 20;
let quadrille;
let row0, col0, row1, col1, row2, col2;

function setup() {
  createCanvas(COLS * LENGTH, ROWS * LENGTH);
  quadrille = createQuadrille(20, 20);
  //randomize();
  // highlevel call:
  //quadrille.colorizeTriangle(row0, col0, row1, col1, row2, col2, [255, 0, 0], [0, 255, 0], [0, 0, 255]);
  //quadrille.colorizeTriangle(row0, col0, row1, col1, row2, col2, 'red', 'green', 'blue');
  quadrille.colorize('red', 'green', 'blue', 'cyan');
}

function draw() {
  background('#060621');
  drawQuadrille(quadrille, { cellLength: LENGTH, outline: 'green' });
  tri();
}

function tri() {
  push();
  stroke('cyan');
  strokeWeight(3);
  noFill();
  triangle(col0 * LENGTH + LENGTH / 2, row0 * LENGTH + LENGTH / 2, col1 * LENGTH + LENGTH / 2, row1 * LENGTH + LENGTH / 2, col2 * LENGTH + LENGTH / 2, row2 * LENGTH + LENGTH / 2);
  pop();
}

function keyPressed() {
  randomize();
  quadrille.clear();
  if (key === 'r') {
    // low level call:
    // [r, g, b, x, y]: rgb -> color components; x, y -> 2d normal
    quadrille.rasterizeTriangle(row0, col0, row1, col1, row2, col2, colorize_shader, [255, 0, 0, 7, 4], [0, 255, 0, -1, -10], [0, 0, 255, 5, 8]);
  }
  if (key === 's') {
    quadrille.rasterize(colorize_shader, [255, 0, 0, 7, 4], [0, 255, 0, -1, -10], [0, 0, 255, 5, 8], [255, 255, 0, -1, -10]);
  }
  /*
  if (key === 't') {
    quadrille.clear(5, 5);
    quadrille.fill(6, 6, color('cyan'));
  }
  */
}

// pretty similar to what p5.Quadrille.colorizeTriangle does
function colorize_shader({ pattern: mixin }) {
  let rgb = mixin.slice(0, 3);
  // debug 2d normal
  console.log(mixin.slice(3));
  // use interpolated color as is
  return color(rgb);
}

function randomize() {
  col0 = int(random(0, COLS));
  row0 = int(random(0, ROWS));
  col1 = int(random(0, COLS));
  row1 = int(random(0, ROWS));
  col2 = int(random(0, COLS));
  row2 = int(random(0, ROWS));
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js

```
{{< /details >}}

# Syntax

> `rasterizeTriangle(row0, col0, row1, col1, row2, col2, shader, pattern0, [pattern1], [pattern2])`

# Parameters

| parameter | description                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------|
| row0      | Number: vertex0 row coordinate                                                                            |
| col0      | Number: vertex0 col coordinate                                                                            |
| row1      | Number: vertex1 row coordinate                                                                            |
| col1      | Number: vertex1 col coordinate                                                                            |
| row2      | Number: vertex2 row coordinate                                                                            |
| col2      | Number: vertex2 col coordinate                                                                            |
| shader    | Function: taking `{ pattern: interpolated_data_array, row: i, col: j }` params and returning a `p5.Color` |
| pattern0  | Array: vertex0 attributes to be interpolated                                                              |
| pattern1  | Array: vertex1 attributes to be interpolated default is pattern0                                          |
| pattern2  | Array: vertex2 attributes to be interpolated default is pattern0                                          |