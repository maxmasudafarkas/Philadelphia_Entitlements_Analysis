---
title: "Part I: Zoning Permits in Philadelphia"
date: 2020-12-21
published: true
tags: [dataviz, matplotlib]
excerpt: "Exploring data from Philadelphia's Department of Licenses and Inspections on zoning permits."
toc: true
toc_sticky: true
---

## Zoning as a Percentage of Total Permits Issued

Since 2007, the City of Philadelphia's [Department of Licenses and Inspections][Department of Licenses and Inspections] has issued close to 700,000 total permits. These permits range in kind: Electrical, plumbing, and building alteration permits are among the most commonly issued permit types. Of these nearly 700,000 permits, zoning and use permits make up a substantial portion, representing approximately 14% of the total. 

![total_permits_pie_chart]({{ site.url }}{{ site.baseurl }}/assets/images/total_permits_pie_chart.png)

## Zoning Permits Issued over Time, 2007-2020

The number of zoning permits that are issued in a given year can serve as a proxy for the amount of development activity that took place in that year. Unlike alteration or electrical permits that may only signify modest changes to existing properties, a zoning permit often indicates that a property owner or developer is seeking to build something entirely new and which falls outside the ambit of the local land use code.

Zoning permits can therefore function as a measure not only of a city's development activity, but of its economic health overall. Real estate development, especially of the scale that requires special land use permissions, ebbs and flows in concert with the surrounding economic conditions.

This dynamic is demonstrated clearly in the below chart, which represents total zoning permits issued in Philadelphia over time. One first notices a slight dip in the years following the Great Recession, succeeded by a steady rise until 2019. Most notably, there is a dramatic dropoff in the year 2020, likely a product of the economic shock caused by the coronavirus pandemic.

![zoning_permits_bar_chart]({{ site.url }}{{ site.baseurl }}/assets/images/zoning_permits_bar_chart.png)

[Department of Licenses and Inspections]: https://www.phila.gov/departments/department-of-licenses-and-inspections/
