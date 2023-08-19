---
weight: 4
draft: false
---

# `rasterizeTriangle()`

Rasterize the triangle defined by vertices `(row0, col0)`, `(row1, col1)`, and `(row2, col2)`, using [barycentric coordinates](https://fgiesen.wordpress.com/2013/02/06/the-barycentric-conspirac/). The user provided [software rendered](https://en.wikipedia.org/wiki/Software_rendering) [(fragment) shader](https://en.wikipedia.org/wiki/Shader) is a function parameterized with the object literal `{ pattern: interpolated_data_array, row: i, col: j }` and that should return a [p5.Color](https://p5js.org/reference/#/p5.Color). Refer to the [colorizeTriangle()]({{< ref "colorize_triangle" >}}) method for an example.

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