---
title: "Data Manipulation Using `dplyr`"
author: "David Bell"
output: 
  html_document:
    keep_md: TRUE
    code_folding: show
    theme: readable
---

## What is `dplyr`?

`dplyr` is  package within the `tidyverse` which contains some handy data manipulation functions. We'll spend our time this week learning about and using some of these functions. Here's some `dplyr` [documentation](https://dplyr.tidyverse.org/) if you'd like to do some more reading. 

## `select()`

The first function we'll look at is `select()`. This function allows us to grab a particular column (or columns) a data frame. Here's a few ways we could use `select()`.

Say we want to get a five-number summary from only the `mpg` and `disp` columns in the `mtcars` dataset. 


```r
library(tidyverse)
```


```r
mtcars %>%
  select(c(mpg, disp)) %>% 
  summary()
```

```
##       mpg             disp      
##  Min.   :10.40   Min.   : 71.1  
##  1st Qu.:15.43   1st Qu.:120.8  
##  Median :19.20   Median :196.3  
##  Mean   :20.09   Mean   :230.7  
##  3rd Qu.:22.80   3rd Qu.:326.0  
##  Max.   :33.90   Max.   :472.0
```

`select()` allowed me to grab only the columns I wanted to run the `summary()` function on. Also notice that since I'm selecting multiple columns, I need to use the `c()` command which indicates I'm passing a list into the function.

Another instance where we often use `select()` is when creating a new data frame that's a subset of our data. Say I want a new data frame that's only the `mpg`, `disp`, and `cyl` columns.


```r
mtcars_subset <- mtcars %>% 
  select(c(mpg, disp, cyl))
```

I now have a new data frame that's only those three columns. I can now do other operations and commands on that data frame the same way I could with `mtcars`.

## `filter()`

The `filter()` function selects instances within a data frame based on certain criteria. This criteria is usually given using logical expressions. Let's look at some examples. 

Say I wanted to get a five-number summary for the `disp` column, but only for cars that have six cylinders. 


```r
mtcars %>% 
  filter(cyl == 6) %>% 
  select(disp) %>% 
  summary()
```

```
##       disp      
##  Min.   :145.0  
##  1st Qu.:160.0  
##  Median :167.6  
##  Mean   :183.3  
##  3rd Qu.:196.3  
##  Max.   :258.0
```

The conditional statment `==` is one of equality. Say I wanted to get the same summary, but for all cars *except* those with six cylinders.


```r
mtcars %>% 
  filter(cyl != 6) %>% 
  select(disp) %>% 
  summary()
```

```
##       disp      
##  Min.   : 71.1  
##  1st Qu.:120.1  
##  Median :275.8  
##  Mean   :244.0  
##  3rd Qu.:351.0  
##  Max.   :472.0
```

`!=` is saying select every row, but leave out the ones where `cyl = 6`. `filter()` also accepts greater than (`>`), less than (`<`), greater than or equal to (`>=`), less than or equal to (`<=`), within a given range (`between()`), or near a certain value (`near()`).

## `mutate()`

If I wanted to create a new column in my data frame, I would use `mutate()`. This allows new columns to be created based on existing columns. Say I wanted a new column which is the ratio of `mpg` and `hp`.


```r
mtcars <- mtcars %>% 
  mutate(mpg_hp_ratio = mpg / hp)

colnames(mtcars)
```

```
##  [1] "mpg"          "cyl"          "disp"         "hp"           "drat"        
##  [6] "wt"           "qsec"         "vs"           "am"           "gear"        
## [11] "carb"         "mpg_hp_ratio"
```

I now have a new column called `mpg_hp_ratio` which is just `mpg` divided by `hp`. I can do all sorts of operations in `mutate()`.


```r
mtcars <- mtcars %>% 
  mutate(average_disp = mean(disp))

colnames(mtcars)
```

```
##  [1] "mpg"          "cyl"          "disp"         "hp"           "drat"        
##  [6] "wt"           "qsec"         "vs"           "am"           "gear"        
## [11] "carb"         "mpg_hp_ratio" "average_disp"
```

```r
summary(mtcars$average_disp)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   230.7   230.7   230.7   230.7   230.7   230.7
```

The sky's the limit with `mutate()`.

## `arrange()`

If you're ever looking to sort or order your data by a certain column, use `arrange()`.


```r
mtcars %>% 
  arrange(disp) %>% 
  head()
```

```
##                 mpg cyl  disp  hp drat    wt  qsec vs am gear carb mpg_hp_ratio
## Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1    0.5215385
## Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2    0.5846154
## Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1    0.4909091
## Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1    0.4136364
## Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2    0.2690265
## Datsun 710     22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1    0.2451613
##                average_disp
## Toyota Corolla     230.7219
## Honda Civic        230.7219
## Fiat 128           230.7219
## Fiat X1-9          230.7219
## Lotus Europa       230.7219
## Datsun 710         230.7219
```

This returns the first six rows of `mtcars`, in ascending order of the `disp` column (least to greatest). If you wanted the data displayed in *descending* order (greatest to least), you can use the `desc()` function.


```r
mtcars %>% 
  arrange(desc(disp)) %>% 
  head()
```

```
##                      mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Cadillac Fleetwood  10.4   8  472 205 2.93 5.250 17.98  0  0    3    4
## Lincoln Continental 10.4   8  460 215 3.00 5.424 17.82  0  0    3    4
## Chrysler Imperial   14.7   8  440 230 3.23 5.345 17.42  0  0    3    4
## Pontiac Firebird    19.2   8  400 175 3.08 3.845 17.05  0  0    3    2
## Hornet Sportabout   18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Duster 360          14.3   8  360 245 3.21 3.570 15.84  0  0    3    4
##                     mpg_hp_ratio average_disp
## Cadillac Fleetwood    0.05073171     230.7219
## Lincoln Continental   0.04837209     230.7219
## Chrysler Imperial     0.06391304     230.7219
## Pontiac Firebird      0.10971429     230.7219
## Hornet Sportabout     0.10685714     230.7219
## Duster 360            0.05836735     230.7219
```





