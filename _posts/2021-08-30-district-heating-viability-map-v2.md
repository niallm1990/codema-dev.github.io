---
title: "District Heating Viability v2"
date: 2021-08-12
categories:
  - map
tags:
  - Bokeh
  - Buildings
  - Heat
layout: splash
read_time: false
---
These maps were created using SEAI's small-level BER data (`05/2021`) & the Valuation Office's floor areas (`2021`).  The code used to generate them is open-source and available [here](https://github.com/codema-dev/projects), however, as the data is closed-access they are not reproducible without access to the underlying data.

{% assign benchmarks_csv="https://codema-dev.s3.eu-west-1.amazonaws.com/benchmarks.csv" %}

**Download:** [dublin_small_area_heat_demand.zip](https://codema-dev.s3.eu-west-1.amazonaws.com/dublin_small_area_heat_demand.zip)

## Overview by Building Type 

### Non-Residential

{% include 2021-08-30-district-heating-viability-map-v2/non_residential_pie_mwh_per_y.html %}

> See [benchmarks.csv]({{ benchmarks_csv }}) for benchmark properties

### Residential

| period_built |  description  | 
| -------------|---------------|
|     PRE19    |  Before 1919  |
|     19_45    |  1919 - 19_45 |
|     ...      |      ...      |
|     11L      | 2011 or Later |

{% include 2021-08-30-district-heating-viability-map-v2/residential_pie_mwh_per_y.html %}


## Dublin City

{% include 2021-08-30-district-heating-viability-map-v2/Glossary-Dublin-City.html %}

{% include 2021-08-30-district-heating-viability-map-v2/Map-Dublin-City.html %}

[Dublin-City.zip](/assets/images/2021-08-30-district-heating-viability-map-v2/Dublin-City.zip)

## Dún Laoghaire-Rathdown

{% include 2021-08-30-district-heating-viability-map-v2/Glossary-Dun-Laoghaire-Rathdown.html %}

{% include 2021-08-30-district-heating-viability-map-v2/Map-Dun-Laoghaire-Rathdown.html %}

[Dun-Laoghaire-Rathdown.zip](/assets/images/2021-08-30-district-heating-viability-map-v2/Dun-Laoghaire-Rathdown.zip)

## Fingal

{% include 2021-08-30-district-heating-viability-map-v2/Glossary-Fingal.html %}

{% include 2021-08-30-district-heating-viability-map-v2/Map-Fingal.html %}

[Fingal.zip](/assets/images/2021-08-30-district-heating-viability-map-v2/Fingal.zip)

## South Dublin

{% include 2021-08-30-district-heating-viability-map-v2/Glossary-South-Dublin.html %}

{% include 2021-08-30-district-heating-viability-map-v2/Map-South-Dublin.html %}

[South-Dublin.zip](/assets/images/2021-08-30-district-heating-viability-map-v2/South-Dublin.zip)

## Caveats

- Public Sector Building demand isn't included as it currently isn't possible to locate all buildings within Small Areas as the data is at postcode level
- Buildings with floor areas much larger than expected for the use type were removed.  See [benchmarks.csv]({{ benchmarks_csv }}) for benchmark properties.

## Assumptions

```
Commercial heat demand
= fossil fuel energy benchmark [kWh/year.m^2]
* assumed boiler efficiency of 85%
* floor area [m^2]
+ industrial space heat energy benchmark [kWh/year.m^2]
* assumed boiler efficiency of 85%
* floor area [m^2]
```
- Buildings with 0 fossil fuel demand are assumed to have no heat demand.
- `CIBSE TM46` & `CIBSE Guide F` floor area energy benchmarks are reflective of current Dublin commercial building demands
- All buildings within each energy benchmark category are well represented by this category.  See [benchmarks.zip](https://codema-dev.s3.eu-west-1.amazonaws.com/benchmarks.zip) for use categories linked to benchmarks and [benchmarks.csv]({{ benchmarks_csv }}) for benchmark properties


```
Residential heat demand = SUM(Main & Supplementary Space & Hot Water Demand [kWh/year])
```
- SEAI's DEAP model is representative of actual heat demands.  In reality, DEAP tends to overestimate demands in older buildings it  and underestimate it in newer.
- Unknown buildings are well represented by archetypes. These archetypes were created by filling unknown buildings iteratively with a sample of nearby, known buildings with a sample size of greater than 30.  So if there is enough buildings of the same `Small Area` and `Period Built` this average is used, otherwise `Electoral District`, then `Postcode`, and finally `Period Built`.