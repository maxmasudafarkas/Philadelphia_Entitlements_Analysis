---
title: "Zoning Appeals Decision Prediction Model"
date: 2020-12-21
published: true
tags: [dataviz]
excerpt: "Using scikit-learn to predict whether a zoning permit appeal will be approved or denied by the Philadelphia Zoning Board of Adjustment."
toc: true
toc_sticky: true
---

Like the Olympian government agencies portrayed in the stories of Franz Kafka, zoning boards are notorious for being unpredictable and impossible to bargain with, plead as one might. Acquiring the requisite permits and entitlements can create a great deal of uncertainty for small property owners and large developers alike, adding excess costs to a real estate development process that is already excessively costly.

This problem begs an important question: Are zoning decisions as unpredictable as they often appear to be? Stated differently, are there metrics, or "features," which we can use to predict whether an agency will give a zoning appeal its blessing? The machine learning model below would suggest that the answer is, sometimes, yes.

## Altair Example

Below is a chart of the incidence of measles since 1928 for the 50 US states.

<div id="altair-chart-1"></div>

This was produced using Altair and embedded in this static web page. Note that you can also display Python code on this page:

```python
import altair as alt
alt.renderers.enable('notebook')
```

## HvPlot Example

Lastly, the measles incidence produced using the HvPlot package:

<div id="hv-chart-1"></div>

## Notes

- See the [raw source code](https://raw.githubusercontent.com/MUSA-550-Fall-2020/github-pages-starter/master/_posts/2019-04-13-measles-charts.md) of this post for details on how these charts were embedded.
- See the [lecture 13A slides](https://github.com/MUSA-550-Fall-2020/week-13/blob/master/lecture-13A.ipynb) for the code that produced these plots.

**Important: When embedding charts, you will likely need to adjust the width/height of the charts before embedding them in the page so they fit nicely when embedded.**