---
weight: 2
draft: false
title: sort()
---

Sort source cells according to their coloring.

## Example

{{< p5-global-iframe quadrille="true" width="425" height="925" >}}
'use strict';
Quadrille.background = 'black';
let ascending;
let source, target;
let array;

function preload() {
  array = [];
  for (let i = 1; i <= 13; i++) {
    array.push(loadImage(`../p${i}.jpg`));
  }
  array.push(210);
  array.push('🐒');
  array.push(80);
}

function setup() {
  createCanvas(400, 900);
  source = createQuadrille(4, array);
  target = source.clone();
  target.sort();
  ascending = createCheckbox('ascending', true);
  ascending.position(10, height / 2);
  ascending.style('color', 'yellow');
  ascending.input(() => target.sort( { ascending: ascending.checked() }));
}

function draw() {
  background(Quadrille.background);
  drawQuadrille(source);
  drawQuadrille(target, { row: 5 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.background = 'black';
let ascending;
let source, target;
let array;

function preload() {
  array = [];
  for (let i = 1; i <= 13; i++) {
    array.push(loadImage(`p${i}.jpg`));
  }
  array.push(210);
  array.push('🐒');
  array.push(80);
}

function setup() {
  createCanvas(400, 900);
  source = createQuadrille(4, array);
  target = source.clone();
  target.sort();
  ascending = createCheckbox('ascending', true);
  ascending.position(10, height / 2);
  ascending.style('color', 'yellow');
  ascending.input(() => target.sort( { ascending: ascending.checked() }));
}

function draw() {
  background(Quadrille.background);
  drawQuadrille(source);
  drawQuadrille(target, { row: 5 });
}
```
{{< /details >}}

## Syntax

> `sort([{[mode], [target], [ascending], [textColor], [textZoom], [background], [cellLength]}])`

## Parameters

| parameter   | description                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------|
| mode        | String: Either `LUMA`, `AVG`, or `DISTANCE` default is `LUMA`.                                                  |
| target      | [p5.Color](https://p5js.org/reference/#/p5.Color): `DISTANCE` mode target color, default is [Quadrille.outline]({{< ref "outline" >}}) |
| ascending   | Boolean: sort cells ascending default is true.                                                                  |
| textColor   | [p5.Color](https://p5js.org/reference/#/p5.Color): text sampling color default is [Quadrille.textColor]({{< ref "text_color" >}}) |
| textZoom    | Number: text zoom level default is [source.textZoom]({{< ref "text_zoom" >}})                               |
| background  | [p5.Color](https://p5js.org/reference/#/p5.Color): background sampling default is `Quadrille.background`, which is set to `white` |
| cellLength  | Number: cell sampling length default is source [width]({{< ref "width" >}})                                  |