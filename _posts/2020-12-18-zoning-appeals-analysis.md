---
title: "Zoning Appeals in Philadelphia"
date: 2020-12-18
published: true
tags: [dataviz, hvplot]
excerpt: "Analyzing and mapping zoning appeals decisions in Philadelphia."
hv-loader:
  hv-chart-1: ["charts/total_neighborhood_appeals_approvals.html"]
  hv-chart-2: ["charts/total_neighborhood_appeals_denials.html"]
toc: true
toc_sticky: true
---

A property owner who is denied a zoning or use permit by the Department of Licenses and Inspections (L&I) is entitled to appeal that decision to the Zoning Board of Adjustment (ZBA), an administrative committee that will review within 30 days any decision by L&I that the property owner believes to be improper or that L&I has directed for ZBA's consideration. Relative to the total number of zoning permits issued by L&I as described in the previous post, appeals are not very common, but they are nonetheless significant. Appeals represent the edge cases of land use: a creative office space in a former industrial tract, or a multi-family residential building that has upset the neighbors. An appeal usually signals some form of underlying conflict for which the appellant is turning to ZBA for resolution.

## Total Zoning Appeals Decisions

The large majority of past ZBA decisions ultimately resulted in approval. These approvals, however, are often accompanied by a "proviso," obligating the developer to agree to some concession to reap the benefit of the ZBA's decision. These provisos can be as simple as mandating that the appellant install central air conditioning or as burdensome as requiring the appellant to seek an entirely separate approval from another municipal agency.

![total_appeals_decisions_bar_chart]({{ site.url }}{{ site.baseurl }}/assets/images/total_appeals_decisions_bar_chart.png

## ZBA Approvals and Denials by Neighborhood

The properties at issue in the ZBA appeals can be located on the map. By using a choropleth map, we can visualize which neighborhoods in Philadelphia contain higher numbers of properties subject to appeals before the ZBA. Because appeals often signify that a proposed zoning permit does not fall within the ordinary exemptions that L&I will grant as a matter of course, the fact that a given neighborhood has experienced a large number of appeals relative to others can be revealing. It can be a signal of proportionally greater or more ambitious development activity, neighborhood change, or even a neighborhood's relative appetite for new development.

The two choropleth maps below show, respectively, ZBA approvals and denials by neighborhood. The majority of appeals are clustered in (1) South Philadelphia in the Point Breeze and Graduate Hospital neighborhoods, (2) Fishtown, and (3) North Central.

<div id="hv-chart-1"></div>

<div id="hv-chart-2"></div>
