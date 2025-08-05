---
weight: 2
draft: false
title: sort({options})
---

Sort source cells according to their coloring.

## Example

{{< p5-global-iframe quadrille="true" width="425" height="925" >}}
'use strict';
Quadrille.background = 'black';
let ascending;
let source, target;
let array;

async function setup() {
  createCanvas(400, 900);
  array = [];
  for (let i = 1; i <= 13; i++) {
    array.push(await loadImage(`../p${i}.jpg`));
  }
  array.push(210);
  array.push('🐒');
  array.push(80);
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

{{% details title="code" open=true %}}
```js
Quadrille.background = 'black';
let ascending;
let source, target;
let array;

async function setup() {
  createCanvas(400, 900);
  array = [];
  for (let i = 1; i <= 13; i++) {
    array.push(await loadImage(`p${i}.jpg`));
  }
  array.push(210);
  array.push('🐒');
  array.push(80);
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
````

{{% /details %}}

## Syntax

> `sort([{[mode], [target], [ascending], [textColor], [textZoom], [background], [cellLength], [tileDisplay], [imageDisplay], [colorDisplay], [stringDisplay], [numberDisplay], [booleanDisplay], [bigintDisplay], [symbolDisplay], [arrayDisplay], [objectDisplay]}])`

## Parameters

| Param            | Description                                                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `mode`           | String: Either `LUMA`, `AVG`, or `DISTANCE`; default is `LUMA`                                                                               |
| `target`         | [p5.Color](https://p5js.org/reference/#/p5.Color): target color for `DISTANCE` mode; default is [Quadrille.outline]({{< ref "outline" >}}) |
| `ascending`      | Boolean: sort order; default is `true`                                                                                                       |
| `textColor`      | [p5.Color](https://p5js.org/reference/#/p5.Color): text sampling color; default is [Quadrille.textColor]({{< ref "text_color" >}})        |
| `textZoom`       | Number: text zoom level; default is [source.textZoom]({{< ref "text_zoom" >}})                                                            |
| `background`     | [p5.Color](https://p5js.org/reference/#/p5.Color): background sampling; default is `Quadrille.background`, which is set to `white`           |
| `cellLength`     | Number: cell sampling length; default is source [width]({{< ref "width" >}})                                                               |
| `tileDisplay`    | Function: empty cell drawing procedure; default is [Quadrille.tileDisplay]({{< ref "display_fns" >}})                                     |
| `imageDisplay`   | Function: drawing procedure for image-filled cells; default is [Quadrille.imageDisplay]({{< ref "display_fns" >}})                        |
| `colorDisplay`   | Function: drawing procedure for color-filled cells; default is [Quadrille.colorDisplay]({{< ref "display_fns" >}})                        |
| `stringDisplay`  | Function: drawing procedure for string-filled cells; default is [Quadrille.stringDisplay]({{< ref "display_fns" >}})                      |
| `numberDisplay`  | Function: drawing procedure for number-filled cells; default is [Quadrille.numberDisplay]({{< ref "display_fns" >}})                      |
| `booleanDisplay` | Function: drawing procedure for boolean-filled cells; default is [Quadrille.booleanDisplay]({{< ref "display_fns" >}})                    |
| `bigintDisplay`  | Function: drawing procedure for BigInt-filled cells; default is [Quadrille.bigintDisplay]({{< ref "display_fns" >}})                      |
| `symbolDisplay`  | Function: drawing procedure for Symbol-filled cells (no default provided)                                                                    |
| `arrayDisplay`   | Function: drawing procedure for array-filled cells (no default provided)                                                                     |
| `objectDisplay`  | Function: drawing procedure for object-filled cells (no default provided)                                                                    |