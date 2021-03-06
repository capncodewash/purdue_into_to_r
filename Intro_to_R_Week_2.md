Introduction to R for Data Science (FutureLearn) - Week 2
================

By Graeme West

This notebook covers the material in Week 2 of [Introduction to R for
Data Science](https://www.futurelearn.com/courses/data-science/5) by
Purdue University on FutureLearn.

The subject matter of the data is airline flight data from the United
States. Week 1 covers basic setup, exploratory data analysis, selecting
data, and basic plotting.

## Preparatory steps

Read in the basic 2008 data (this takes a couple of minutes):

``` r
myDF <- read.csv("./datasets/2008.csv.bz2")
```
