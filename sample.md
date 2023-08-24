---
weight: 3
draft: false
---

# `sample()`

Sample cell as the `{r, g, b, a, total}` object literal. Used by the [sort]({{< ref "sort" >}}) algorithm. For instance `LUMA` sorting is [implemented](https://github.com/objetos/p5.quadrille.js/blob/main/p5.quadrille.js#L1018) as follows:

``` js
// excerpt from sort
let memory1D = this.toArray();
// ...
memory1D.sort((cellA, cellB) => {
  let sa = Quadrille.sample({ cell: cellA, background: background,
                              cellLength: cellLength,
                              textColor: textColor, textZoom: textZoom });
  let sb = Quadrille.sample({ cell: cellB, background: background,
                              cellLength: cellLength,
                              textColor: textColor, textZoom: textZoom });
  let wa = 0.299 * sa.r + 0.587 * sa.g + 0.114 * sa.b;
  let wb = 0.299 * sb.r + 0.587 * sb.g + 0.114 * sb.b;
  return wa - wb;
});
```

Use this method to implementing other sorting criteria of the `quadrille` cells.

# Syntax

> `sample([{cell, imageDisplay, colorDisplay, stringDisplay, numberDisplay, arrayDisplay, objectDisplay, background, cellLength, outlineWeight, outline, textColor, textZoom}])`

# Parameters

<!--
imageDisplay = this.IMAGE,
colorDisplay = this.COLOR,
stringDisplay = this.STRING,
numberDisplay = this.NUMBER,
arrayDisplay,
objectDisplay,
background = this.BACKGROUND,
cellLength = this.CELL_LENGTH,
outlineWeight = this.OUTLINE_WEIGHT,
outline = this.OUTLINE,
textColor = this.TEXT_COLOR,
textZoom = this.TEXT_ZOOM}]
-->

| parameter   | description                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------|
| mode        | String: Either `LUMA`, `AVG`, or `DISTANCE` default is `LUMA`.                                                  |
| target      | [p5.Color](https://p5js.org/reference/#/p5.Color): `DISTANCE` mode target color, default is `Quadrille.OUTLINE` |
| ascending   | Boolean: sort cells ascending default is true.                                                                  |
| textColor   | [p5.Color](https://p5js.org/reference/#/p5.Color): text sampling color default is `Quadrille.TEXT_COLOR`        |
| textZoom    | Number:: text zoom level default is `Quadrille.TEXT_ZOOM`                                                       |
| background  | [p5.Color](https://p5js.org/reference/#/p5.Color): background sampling default is `Quadrille.BACKGROUND`        |
| cellLength  | Number: cell sampling length default is quadrille [width]({{< ref "width" >}})                                  |