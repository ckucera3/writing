+++
date = "2016-05-14T15:23:09-04:00"
draft = true
title = "D3 Tips and Snippets"

+++

I enjoy working with D3, and keep a list of code snippets and notes at hand for quick reference. I'll dump the notes here.

## Create a quantitative scale

```
// linear

var scale = d3.scale.linear()
    .domain([-1, 1])
    .range([height, 0])

```

## Insert an element rather than append

```
selection.insert("div", ":first-child"); //this inserts a div before the first child of the element selected.

```


## Change the width, height of an svg
```js

```

## Give svg a border
```js

var borderPath = svg.append("rect")
    .attr("x", 0)
    .attr("y", 0)
    .attr("height", svgHeight)
    .attr("width", svgWidth)
    .style("stroke", bordercolor)
    .style("fill", "none")
    .style("stroke-width", borderwidth);
```



## Get the bounds of an SVG

You can call `.node().getBBox()` on SVG elements to get their bounding box in terms of SVG coordinates


## Get a style attribute of an SVG

`selection.style("attribute-name")` should do the trick.


## Basic transition

```js

selection.transition() // this transition runs from t=1s to t=3s
    .delay(1000)
    .duration(2000)
  .transition() // then a delay from t=3s to t=4s
    .duration(1000)
  .transition() // then lastly another transition from t=4s to t=5s

```
