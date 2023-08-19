---
weight: 3
draft: false
---

# `colorize()`

Colorize quadrille according to upper-left corner `color0`, bottom-left corner `color1`, upper-right corner `color2`, and bottom-right corner `color3` colors. Call [colorizeTriangle()]({{< ref "colorize_triangle" >}}) on the two non-overlapping triangles entirely covering the quadrille.
# Syntax

> `colorize(color0, [color1], [color2], [color3])`

# Parameters

| parameter | description                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| color0    | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner0 color to be interpolated                   |
| color1    | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner1 color to be interpolated default is color0 |
| color2    | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner2 color to be interpolated default is color0 |
| color3    | [p5.Color](https://p5js.org/reference/#/p5.Color) : corner2 color to be interpolated default is color0 |