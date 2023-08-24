---
weight: 2
draft: false
---

# `sort()`

Sort quadrille cells according to their coloring.

# Example

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="425" height="425" >}}
`use strict`;

{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js

```
{{< /details >}}

# Syntax

> `sort([{[mode], [target], [ascending], [textColor], [textZoom], [background], [cellLength]}])`

# Parameters

| parameter   | description                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------|
| mode        | String: Either `LUMA`, `AVG`, or `DISTANCE` default is `LUMA`.                                                  |
| target      | [p5.Color](https://p5js.org/reference/#/p5.Color): `DISTANCE` mode target color, default is `Quadrille.OUTLINE` |
| ascending   | Boolean: sort cells ascending default is true.                                                                  |
| textColor   | [p5.Color](https://p5js.org/reference/#/p5.Color): text sampling color default is `Quadrille.TEXT_COLOR`        |
| textZoom    | Number:: text zoom level default is `Quadrille.TEXT_ZOOM`                                                       |
| background  | [p5.Color](https://p5js.org/reference/#/p5.Color): background sampling default is `Quadrille.BACKGROUND`        |
| cellLength  | Number: cell sampling length default is quadrille [width]({{< ref "width" >}})                                  |