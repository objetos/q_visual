---
weight: 1
draft: false
---

# `filter()`

Apply [convolution mask](https://en.wikipedia.org/wiki/Kernel_%28image_processing%29) filter either to the whole quadrille or at specific `(row, col)` cell.

# Examples

## filter(mask)

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="537" height="537" >}}
`use strict`;
let scl = 4;
let mask, quadrille, source, target;
let image;
let numberDisplay;
let displayMask;

function update() {
  const displaySource = quadrille === source || quadrille === undefined;
  source = createQuadrille(2 ** scl, image);
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
    [0.0625, 0.125, 0.0625],
    [0.125, 0.25, 0.125],
    [0.0625, 0.125, 0.0625]]);
  /*
  numberDisplay = ({ graphics: graphics, cell: cell, outline: outline,
                     outlineWeight: outlineWeight, cellLength: cellLength }) => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    graphics.colorMode(graphics.RGB, 255);
    graphics.fill(graphics.color(red(numberColor), green(numberColor), blue(numberColor),
                  graphics.map(cell, min, max, 0, 255)));
    graphics.rect(0, 0, cellLength, cellLength);
    Quadrille.TILE({ graphics: graphics, outline: outline, outlineWeight: outlineWeight,
                     cellLength: cellLength });
  }
  */
  numberDisplay = ({ graphics: graphics, cell: cell, outline: outline,
                     outlineWeight: outlineWeight, cellLength: cellLength })
                  => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    colorMode(RGB, 255);
    fill(color(red(numberColor), green(numberColor), blue(numberColor),
               map(cell, min, max, 0, 255)));
    rect(0, 0, cellLength, cellLength);
    Quadrille.TILE({ graphics: graphics, outline: outline,
                     outlineWeight: outlineWeight, cellLength: cellLength });
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
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    update();
  }
  if (key === 'c') {
    quadrille = quadrille === source ? target : source;
  }
  if (key === 'm') {
    displayMask = !displayMask;
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
  const displaySource = quadrille === source || quadrille === undefined;
  source = createQuadrille(2 ** scl, image);
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
    [0.0625, 0.125, 0.0625],
    [0.125, 0.25, 0.125],
    [0.0625, 0.125, 0.0625]]);
  numberDisplay = ({ graphics: graphics, cell: cell, outline: outline,
                     outlineWeight: outlineWeight, cellLength: cellLength })
                  => {
    const numberColor = 'magenta';
    const min = 0.0625;
    const max = 0.25;
    colorMode(RGB, 255);
    fill(color(red(numberColor), green(numberColor), blue(numberColor),
               map(cell, min, max, 0, 255)));
    rect(0, 0, cellLength, cellLength);
    Quadrille.TILE({ graphics: graphics, outline: outline,
                     outlineWeight: outlineWeight, cellLength: cellLength });
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
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    update();
  }
  if (key === 'c') {
    quadrille = quadrille === source ? target : source;
  }
  if (key === 'm') {
    displayMask = !displayMask;
  }
}
```
{{< /details >}}

## filter(mask, row, col)

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="537" height="537" >}}
`use strict`;
let scl = 4;
let mask, edge3, blur3, blur5, quadrille, source, target;
let image;
let numberDisplay;
let local = false;
let image_mode = true;

function update() {
  let c = quadrille == null ? false : quadrille === target;
  source = createQuadrille(2 ** scl, image);
  target = source.clone();
  target.filter(mask);
  quadrille = source;
  quadrille = c ? target : source;
}

function preload() {
  image = loadImage('../mandrill.png');
}

function setup() {
  createCanvas(512, 512);
  blur3 = createQuadrille([
    [0.0625, 0.125, 0.0625],
    [0.125, 0.25, 0.125],
    [0.0625, 0.125, 0.0625]]);
  blur5 = createQuadrille([
    [1 / 256, 4 / 256, 6 / 256, 4 / 256, 1 / 256],
    [4 / 256, 16 / 256, 24 / 256, 16 / 256, 4 / 256],
    [6 / 256, 24 / 256, 36 / 256, 24 / 256, 6 / 256],
    [4 / 256, 16 / 256, 24 / 256, 16 / 256, 4 / 256],
    [1 / 256, 4 / 256, 6 / 256, 4 / 256, 1 / 256]]);
  /*
  edge3 = createQuadrille([[-1, -1, -1],
                           [-1,  8, -1],
                           [-1, -1, -1]]); 
  */
  edge3 = createQuadrille([
    [0, -1, 0],
    [-1, 5, -1],
    [0, -1, 0]]);
  //mask = blur5;
  mask = blur3;
  numberDisplay = ({ graphics: graphics, cell: cell, outline: outline, outlineWeight: outlineWeight, cellLength: cellLength, row: i, col: j }) => {
    let numberColor = local ? 'green' : 'magenta';
    let min = 0.0625;
    let max = 0.25;
    graphics.colorMode(graphics.RGB, 255);
    graphics.fill(graphics.color(red(numberColor), green(numberColor), blue(numberColor), graphics.map(cell, min, max, 0, 255)));
    graphics.rect(0, 0, cellLength, cellLength);
    Quadrille.TILE({ graphics: graphics, outline: outline, outlineWeight: outlineWeight, cellLength: cellLength, row: i, col: j });
  }
  update();
}

function draw() {
  background('#060621');
  if (local) {
    drawQuadrille(source, { cellLength: 512 / (2 ** scl), outlineWeight: 16 / (2 ** scl) });
    const half_size = (mask.width - 1) / 2;
    drawQuadrille(mask, { col: source.mouseCol - half_size, row: source.mouseRow - half_size, cellLength: 512 / (2 ** scl), outline: 'green', numberDisplay: numberDisplay });
  }
  else {
    if (image_mode) {
      drawQuadrille(quadrille, { cellLength: 512 / (2 ** scl), outlineWeight: 16 / (2 ** scl), outline: quadrille === source ? 'magenta' : 'cyan' });
    } else {
      drawQuadrille(mask, { cellLength: width / mask.width, outline: 'magenta', numberDisplay: numberDisplay });
    }
  }
}

function mouseMoved() {
  if (local) {
    source.filter(mask, source.mouseRow, source.mouseCol);
    return false;
  }
}

function keyPressed() {
  if (key === 'r') {
    update();
  }
  if (key === 's') {
    scl = scl < 7 ? scl + 1 : 4;
    update();
  }
  if (key === 'c') {
    quadrille = quadrille === source ? target : source;
  }
  if (key === 'i') {
    image_mode = !image_mode;
  }
  if (key === 'l') {
    local = !local;
  }
}
{{< /p5-global-iframe >}}

# Syntax

> `filter(mask, [row], [col])`

# Parameters

| parameter | description                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| mask      | Quadrille: quadrille of numbers representing the [convolution mask](https://en.wikipedia.org/wiki/Kernel_%28image_processing%29) |
| row       | Number: cell row coordinate, default is 0 which applies filter to the whole quadrille                                            |
| col       | Number: cell col coordinate, default is 0 which applies filter to the whole quadrille                                            |