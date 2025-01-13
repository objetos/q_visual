---
weight: 1
draft: false
title: filter(args)
---

Apply [convolution mask](https://en.wikipedia.org/wiki/Kernel_%28image_processing%29) filter either to the whole quadrille or at specific `(row, col)` cell.

{{< callout type="info" >}}
Only pixelated quadrille images may be filtered, i.e., those created either with `createQuadrille(width, image, true)` or `createQuadrille(width, image, false)`.
{{< /callout >}}

## Examples

### filter(mask)

(press **f** to toggle filtered image; **m** to toggle mask display; and, **s** to rescale image)  
{{< p5-global-iframe quadrille="true" width="537" height="537" >}}
'use strict';
let scl = 4;
let mask, quadrille, source, target;
let image;
let numberDisplay;
let displayMask;

function update() {
  const displaySource = !quadrille || quadrille === source;
  source = createQuadrille(2 ** scl, image, false);
  target = source.clone();
  target.filter(mask);
  quadrille = displaySource ? source : target;
}

function preload() {
  image = loadImage('../mandrill.png');
}

function setup() {
  createCanvas(512, 512);
  mask = createQuadrille([
    [1 / 256, 4 / 256, 6 / 256, 4 / 256, 1 / 256],
    [4 / 256, 16 / 256, 24 / 256, 16 / 256, 4 / 256],
    [6 / 256, 24 / 256, 36 / 256, 24 / 256, 6 / 256],
    [4 / 256, 16 / 256, 24 / 256, 16 / 256, 4 / 256],
    [1 / 256, 4 / 256, 6 / 256, 4 / 256, 1 / 256]]);
  /*
  numberDisplay = ({ graphics, value, outline, outlineWeight, cellLength }) => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    graphics.colorMode(graphics.RGB, 255);
    graphics.fill(graphics.color(red(numberColor), green(numberColor), blue(numberColor),
                  graphics.map(value, min, max, 0, 255)));
    graphics.rect(0, 0, cellLength, cellLength);
    Quadrille.tileDisplay({ graphics: graphics, outline: outline, outlineWeight: outlineWeight,
                     cellLength: cellLength });
  }
  */
  numberDisplay = ({ graphics, value, outline, outlineWeight, cellLength }) => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    colorMode(RGB, 255);
    fill(color(red(numberColor), green(numberColor), blue(numberColor),
               map(value, min, max, 0, 255)));
    rect(0, 0, cellLength, cellLength);
    Quadrille.tileDisplay({ graphics, outline, outlineWeight, cellLength });
  }
  update();
}

function draw() {
  background('#060621');
  if (displayMask) {
    drawQuadrille(mask, { cellLength: width / mask.width, outline: 'magenta',
                          numberDisplay: numberDisplay });
  } else {
    drawQuadrille(quadrille,
                  { cellLength: 512 / (2 ** scl),
                    outlineWeight: 16 / (2 ** scl),
                    outline: quadrille === source ? 'magenta' : 'cyan' });
  }
}

function keyPressed() {
  if (key === 'f') {
    quadrille = quadrille === source ? target : source;
  }
  if (key === 'm') {
    displayMask = !displayMask;
  }
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    update();
  }
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let scl = 4;
let mask, quadrille, source, target;
let image;
let numberDisplay;
let displayMask;

function update() {
  const displaySource = !quadrille || quadrille === source;
  source = createQuadrille(2 ** scl, image, false);
  target = source.clone();
  target.filter(mask);
  quadrille = displaySource ? source : target;
}

function preload() {
  image = loadImage('mandrill.png');
}

function setup() {
  createCanvas(512, 512);
  mask = createQuadrille([
    [1 / 256, 4 / 256, 6 / 256, 4 / 256, 1 / 256],
    [4 / 256, 16 / 256, 24 / 256, 16 / 256, 4 / 256],
    [6 / 256, 24 / 256, 36 / 256, 24 / 256, 6 / 256],
    [4 / 256, 16 / 256, 24 / 256, 16 / 256, 4 / 256],
    [1 / 256, 4 / 256, 6 / 256, 4 / 256, 1 / 256]]);
  numberDisplay = ({graphics, value, outline, outlineWeight, cellLength}) => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    colorMode(RGB, 255);
    fill(color(red(numberColor), green(numberColor), blue(numberColor),
               map(value, min, max, 0, 255)));
    rect(0, 0, cellLength, cellLength);
    Quadrille.tileDisplay({ graphics, outline, outlineWeight, cellLength });
  }
  update();
}

function draw() {
  background('#060621');
  if (displayMask) {
    drawQuadrille(mask, { cellLength: width / mask.width, outline: 'magenta',
                          numberDisplay: numberDisplay });
  } else {
    drawQuadrille(quadrille,
                  { cellLength: 512 / (2 ** scl),
                    outlineWeight: 16 / (2 ** scl),
                    outline: quadrille === source ? 'magenta' : 'cyan' });
  }
}

function keyPressed() {
  if (key === 'f') {
    quadrille = quadrille === source ? target : source;
  }
  if (key === 'm') {
    displayMask = !displayMask;
  }
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    update();
  }
}
```
{{< /details >}}

### filter(mask, row, col)

(mouse move to apply filter locally; press **r** to reset filtered image & **s** to rescale it)  
{{< p5-global-iframe quadrille="true" width="537" height="537" >}}
'use strict';
let scl = 4;
let mask, quadrille;
let image;
let numberDisplay;

function preload() {
  image = loadImage('../mandrill.png');
}

function setup() {
  createCanvas(512, 512);
  mask = createQuadrille([
    [0.0625, 0.125, 0.0625],
    [0.125, 0.25, 0.125],
    [0.0625, 0.125, 0.0625]]);
  numberDisplay = ({ graphics, value, outline, outlineWeight, cellLength }) => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    colorMode(RGB, 255);
    fill(color(red(numberColor), green(numberColor), blue(numberColor),
               map(value, min, max, 0, 255)));
    rect(0, 0, cellLength, cellLength);
    Quadrille.tileDisplay({ graphics, outline, outlineWeight, cellLength });
  }
  quadrille = createQuadrille(2 ** scl, image, false);
}

function draw() {
  background('#060621');
  drawQuadrille(quadrille, { cellLength: 512 / (2 ** scl),
                             outlineWeight: 16 / (2 ** scl) });
  const half_size = (mask.width - 1) / 2;
  drawQuadrille(mask, { col: quadrille.mouseCol - half_size,
                        row: quadrille.mouseRow - half_size,
                        cellLength: 512 / (2 ** scl),
                        outline: 'green',
                        numberDisplay: numberDisplay });
}

function mouseMoved() {
  quadrille.filter(mask, quadrille.mouseRow, quadrille.mouseCol);
  return false;
}

function keyPressed() {
  if (key === 'r') {
    quadrille = createQuadrille(2 ** scl, image);
  }
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    quadrille = createQuadrille(2 ** scl, image);
  }
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let scl = 4;
let mask, quadrille;
let image;
let numberDisplay;

function preload() {
  image = loadImage('mandrill.png');
}

function setup() {
  createCanvas(512, 512);
  mask = createQuadrille([
    [0.0625, 0.125, 0.0625],
    [0.125, 0.25, 0.125],
    [0.0625, 0.125, 0.0625]]);
  numberDisplay = ({graphics, value, outline, outlineWeight, cellLength}) => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    colorMode(RGB, 255);
    fill(color(red(numberColor), green(numberColor), blue(numberColor),
               map(value, min, max, 0, 255)));
    rect(0, 0, cellLength, cellLength);
    Quadrille.tileDisplay({ graphics, outline, outlineWeight, cellLength });
  }
  quadrille = createQuadrille(2 ** scl, image, false);
}

function draw() {
  background('#060621');
  drawQuadrille(quadrille, { cellLength: 512 / (2 ** scl),
                             outlineWeight: 16 / (2 ** scl) });
  const half_size = (mask.width - 1) / 2;
  drawQuadrille(mask, { col: quadrille.mouseCol - half_size,
                        row: quadrille.mouseRow - half_size,
                        cellLength: 512 / (2 ** scl),
                        outline: 'green',
                        numberDisplay: numberDisplay });
}

function mouseMoved() {
  quadrille.filter(mask, quadrille.mouseRow, quadrille.mouseCol);
  return false;
}

function keyPressed() {
  if (key === 'r') {
    quadrille = createQuadrille(2 ** scl, image);
  }
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    quadrille = createQuadrille(2 ** scl, image);
  }
}
```
{{< /details >}}

## Syntax

> `filter(mask, [row], [col])`

## Parameters

| Param     | Description                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| `mask`    | Quadrille: quadrille of numbers representing the [convolution mask](https://en.wikipedia.org/wiki/Kernel_%28image_processing%29) |
| `row`     | Number: cell row coordinate, if `undefined` applies filter to the whole     quadrille                                            |
| `col`     | Number: cell col coordinate, if `undefined` applies filter to the whole     quadrille                                            |