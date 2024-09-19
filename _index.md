---
bookCollapseSection: true
weight: 8
draft: false
---

# Visual algorithms

The visual algorithms suite comprises functions that manipulate and visually represent data within quadrille cells. Algorithms like [filter]({{< relref "filter" >}}) for image convolutions, [rasterize]({{< relref "rasterize" >}}) for software-based barycentric interpolations, and [sort]({{< relref "sort" >}}) for arranging cells based on visual criteria, enable the creation of dynamic visualizations. These methods collectively transform the quadrille into an interactive canvas for illustrating and navigating visual computing concepts, offering an intuitive way to understand and apply various algorithms from rasterization and image processing to data sorting.

{{< callout type="info" >}}
**Observation**\
The methods found in this section may be [chained](https://en.wikipedia.org/wiki/Method_chaining), e.g., `quadrille.filter(mask).rasterize(shader, array)` which is equivalent to:
```js
quadrille.filter(mask);
quadrille.rasterize(shader, array);
```
{{< /callout >}}