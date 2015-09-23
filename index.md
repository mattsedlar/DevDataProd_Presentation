---
title       : Commuting Methods by State, Income
subtitle    : Creating an interactive Shiny app using 2014 ACS data
author      : Matthew Sedlar
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap, mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Why Look at Commuting Methods by Income Groups?

* The data set comes from the American Community Survey and is available to the public at [Data.Gov](http://www.data.gov/).

* I was particularly interested in the [Means of Transportation to Work by Selected Characteristics for Workplace Geography](http://factfinder.census.gov/bkmk/table/1.0/en/ACS/14_1YR/S0804/0100000US.04000) 2014 American Community Survey 1-Year Estimates from the U.S. Census Bureau.

* Since owning a vehicle is often considered a luxury item, I was curious about whether workers 16 years and over in lower income groups relied more on public transportation and carpooling while workers in higher income groups drove alone to work. But obviously it varies state by state, because some states have better public transportation options than others.

* Why not build an app that helps conduct an exploratory analysis of the data?

---

## What the Data Looks Like (After Some Cleaning)



Below is a data frame (transposed with margins of error excluded to fit the slide) of the state of Alabama and the estimated percentage of people who drove alone by income levels. The data also includes carpool and public transportation methods (not shown here).


|                   |Observation |
|:------------------|:-----------|
|State              |Alabama     |
|Total Drove Alone  |1681608     |
|1 to 9,999 or loss |0.133       |
|10,000 to.14.999   |0.084       |
|15,000 to 24,999   |0.176       |
|25,000 to 34,999   |0.155       |
|35,000 to 49,999   |0.169       |
|50,000 to 64,999   |0.111       |
|65,000 to 74,999   |0.041       |
|75,000 or more     |0.131       |

---

## How the App Works

The user inputs state and income group and the app calculates the following:

* T = Estimated total of workers 16 years and older for commuting method and income group.
* I = Percentage (in decimals) of workers in selected income group
* N = Number of estimated workers for commuting method.
* d = drive alone, c = carpooled, p = public transportation.
* S = Overall sample of workers

Example of workers who drove alone:
$T_d=N_d(I_d)$

Upper and Lower Margins: $N_d(I_d \pm Margin)$

$S=T_d+T_c+T_p$

Each bar in the chart represents: $\frac{T_d}{S},\frac{T_c}{S},\frac{T_p}{S}$

---

## What the App Displays

The app uses ggplot2's geom_bar and geom_errorbar to plot a results dataframe based on the calculations (see example below: Alabama and \\$1 to \\$9,999 or loss group). It also uses googleVis' gvisGeoChart to plot the state, mostly because it looks cool.


|Method                  | Percentage| Upper.Margin| Lower.Margin|
|:-----------------------|----------:|------------:|------------:|
|Drive Alone*            |  0.8644020|    0.8968983|    0.8319057|
|Carpool                 |  0.1258317|    0.1357138|    0.1159496|
|Public Transportation** |  0.0097663|    0.0120998|    0.0074327|

![alt text][id]
[id]: assets/img/screenshot.png "Screenshot"
