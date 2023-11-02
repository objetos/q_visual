---
bookCollapseSection: true
weight: 8
draft: false
---

# Visual computing methods

Visual computing methods to perform [image processing](https://en.wikipedia.org/wiki/Digital_image_processing), sorting of the quadrille cells and emulate [shaders](https://en.wikipedia.org/wiki/Shader) in software employ the quadrille cells as a [raster graphics](https://en.wikipedia.org/wiki/Raster_graphics).

{{< hint info >}}
**Observation**\
The methods found in this section may be [chained](https://en.wikipedia.org/wiki/Method_chaining), e.g., `quadrille.filter(mask).rasterize(shader, array)` which is equivalent to:
```js
quadrille.filter(mask);
quadrille.rasterize(shader, array);
```
{{< /hint >}}