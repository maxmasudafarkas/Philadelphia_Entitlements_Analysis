---
title: "Zoning Appeals in Philadelphia"
date: 2020-12-18
published: true
tags: [dataviz, hvplot]
excerpt: "Analyzing and mapping zoning appeals decisions in Philadelphia."
folium-loader:
  folium-chart-1: ["charts/foliumChart.html", "400"]
  folium-chart-2: ["charts/percent_no_internet.html", "400"]
toc: true
toc_sticky: true
---

A property owner who is denied a zoning or use permit by the Department of Licenses and Inspections (L&I) is entitled to appeal that decision to the Zoning Board of Adjustment (ZBA), an administrative committee that will review within 30 days any decision by L&I that the property owner believes to be improper or that L&I has directed for ZBA's consideration. Relative to the total number of zoning permits issued by L&I as described in the previous post, appeals are not very common, but they are nonetheless significant. Appeals represent the edge cases of land use: a creative office space in a former industrial tract, or a multi-family residential building that has upset the neighbors. An appeal usually signals some form of underlying conflict for which the appellant is turning to ZBA for resolution.

This post will show examples of embedding interactive maps produced using [Folium](https://github.com/python-visualization/folium).

## Total Zoning Appeals Decisions

The large majority of past ZBA decisions ultimately resulted in some form of approval. These approvals, however, are often accompanied by some "proviso," obligating the developer to agree to some concession to reap the benefit of the ZBA's decision. These provisos can be as simple as mandating that the appellant install central air conditioning or as burdensome as requiring the appellant to seek an entirely separate approval from another municipal agency.

<div id="folium-chart-1"></div>

## Percentage of Households without Internet

<div id="folium-chart-2"></div>

See the [lecture 9B slides](https://musa-550-fall-2020.github.io/slides/lecture-9B.html) and the [lecture 10A slides](https://musa-550-fall-2020.github.io/slides/lecture-10A.html) for the code that produced these plots.
