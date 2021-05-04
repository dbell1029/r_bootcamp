---
title: "Getting Started with R"
author: "David Bell"
output: 
  html_document:
    keep_md: TRUE
    code_folding: show
    theme: readable
---

### R Script vs. R Markdown

Data scientist traditionally use two files while in RStudio: R scripts (.R) and R Markdown documents (.rmd). When we're exploring, cleaning, and visualizing data, we usually work in an R script where we don't have to worry about making our work neat or presentable. But when it comes time to present our findings, R Markdown becomes a great tool to write to and make an HTML document where we can create a more cohesive analysis. You can create either of these by selecing `File`, `New File`, then select whichever format you need (notice the numerous coding language options available to you in RStudio).

### Loading Libraries

First things first, we must load the libraries we're going to need for our work. Click `Insert`, `R` to add an R chunk. A good standard is always loading the `tidyverse` package as it contains many of the tools and functions we'll need to wrangle and visualize data. We do this by typing `library(tidyverse)`.


```r
library(tidyverse)
```

If a library you're wishing to use hasn't yet been installed, you will need to run `install.packages()` with whichever library you're loading in quotes. The function I usually use is `pacman::p_load()` which loads the library, and if it hasn't yet been installed, attempts to install it. A bit of a combination of `install.packages()` and `library()`.

### Exploring Data

To view a data frame in another tab, run `View(data)`. Let's take a look at the `mtcars` dataset:


```r
# View(mtcars)
```

This is a good way to sort explore the data, where you can sort the data by individual columns. Another good command is `summary(data)`:


```r
summary(mtcars)
```

```
##       mpg             cyl             disp             hp       
##  Min.   :10.40   Min.   :4.000   Min.   : 71.1   Min.   : 52.0  
##  1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8   1st Qu.: 96.5  
##  Median :19.20   Median :6.000   Median :196.3   Median :123.0  
##  Mean   :20.09   Mean   :6.188   Mean   :230.7   Mean   :146.7  
##  3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0   3rd Qu.:180.0  
##  Max.   :33.90   Max.   :8.000   Max.   :472.0   Max.   :335.0  
##       drat             wt             qsec             vs        
##  Min.   :2.760   Min.   :1.513   Min.   :14.50   Min.   :0.0000  
##  1st Qu.:3.080   1st Qu.:2.581   1st Qu.:16.89   1st Qu.:0.0000  
##  Median :3.695   Median :3.325   Median :17.71   Median :0.0000  
##  Mean   :3.597   Mean   :3.217   Mean   :17.85   Mean   :0.4375  
##  3rd Qu.:3.920   3rd Qu.:3.610   3rd Qu.:18.90   3rd Qu.:1.0000  
##  Max.   :4.930   Max.   :5.424   Max.   :22.90   Max.   :1.0000  
##        am              gear            carb      
##  Min.   :0.0000   Min.   :3.000   Min.   :1.000  
##  1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:2.000  
##  Median :0.0000   Median :4.000   Median :2.000  
##  Mean   :0.4062   Mean   :3.688   Mean   :2.812  
##  3rd Qu.:1.0000   3rd Qu.:4.000   3rd Qu.:4.000  
##  Max.   :1.0000   Max.   :5.000   Max.   :8.000
```
If your data is quantitative, this outputs a six-number summary for each variable. If you want a brief glance of your data, try `head(data, 10)` which displays the first ten rows of your data frame:


```r
head(mtcars, 10)
```

```
##                    mpg cyl  disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
## Duster 360        14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
## Merc 240D         24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
## Merc 230          22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
## Merc 280          19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
```
`str(data)` will list the structure of your data frame:


```r
str(mtcars)
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num  160 160 108 258 360 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

It's our job as data scientists to be literate about our/our client's data and this means exploring and getting familiar with the data. Checking for missing values is part of that. We can check by running `is.na(data)` and `sum(is.na(data))`:


```r
is.na(mtcars)
```

```
##                       mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear
## Mazda RX4           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Mazda RX4 Wag       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Datsun 710          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Hornet 4 Drive      FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Hornet Sportabout   FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Valiant             FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Duster 360          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 240D           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 230            FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 280            FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 280C           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 450SE          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 450SL          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Merc 450SLC         FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Cadillac Fleetwood  FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Lincoln Continental FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Chrysler Imperial   FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Fiat 128            FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Honda Civic         FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Toyota Corolla      FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Toyota Corona       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Dodge Challenger    FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## AMC Javelin         FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Camaro Z28          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Pontiac Firebird    FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Fiat X1-9           FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Porsche 914-2       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Lotus Europa        FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Ford Pantera L      FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Ferrari Dino        FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Maserati Bora       FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## Volvo 142E          FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##                      carb
## Mazda RX4           FALSE
## Mazda RX4 Wag       FALSE
## Datsun 710          FALSE
## Hornet 4 Drive      FALSE
## Hornet Sportabout   FALSE
## Valiant             FALSE
## Duster 360          FALSE
## Merc 240D           FALSE
## Merc 230            FALSE
## Merc 280            FALSE
## Merc 280C           FALSE
## Merc 450SE          FALSE
## Merc 450SL          FALSE
## Merc 450SLC         FALSE
## Cadillac Fleetwood  FALSE
## Lincoln Continental FALSE
## Chrysler Imperial   FALSE
## Fiat 128            FALSE
## Honda Civic         FALSE
## Toyota Corolla      FALSE
## Toyota Corona       FALSE
## Dodge Challenger    FALSE
## AMC Javelin         FALSE
## Camaro Z28          FALSE
## Pontiac Firebird    FALSE
## Fiat X1-9           FALSE
## Porsche 914-2       FALSE
## Lotus Europa        FALSE
## Ford Pantera L      FALSE
## Ferrari Dino        FALSE
## Maserati Bora       FALSE
## Volvo 142E          FALSE
```

```r
sum(is.na(mtcars))
```

```
## [1] 0
```

`is.na(data)` isn't always the best option if you're working with large data, but the `sum(is.na(data))` can give you an idea of how much you're missing. 









