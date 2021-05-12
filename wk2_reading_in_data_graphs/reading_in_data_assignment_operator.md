---
title: "Reading in Data and Using the Assignment Operator"
author: "David Bell"
output: 
  html_document:
    keep_md: TRUE
    code_folding: show
    theme: readable
---

# Reading in Data

Before we start working with a dataset, we need to import it into our R Studio environment. The format your data is in will determine the manner in which you read it in. Today we'll be working with the `Iris` data set. Before we do anything, we need to read in our required libraries.


```r
library(tidyverse)
```

Here's a link to the Iris .csv dataset: `https://gist.githubusercontent.com/curran/a08a1080b88344b0c8a7/raw/0e7a9b0a5d22642a06d3d5b9bcbad9890c8ee534/iris.csv` Let's go ahead and import it using the `read_csv()` function in `readr`. We do this by typing `read_csv()` and then the file path to the dataset - in this case, the url above. Don't forget to put the file path in quotes!


```r
read_csv("https://gist.githubusercontent.com/curran/a08a1080b88344b0c8a7/raw/0e7a9b0a5d22642a06d3d5b9bcbad9890c8ee534/iris.csv")
```

```
## # A tibble: 150 x 5
##    sepal_length sepal_width petal_length petal_width species
##           <dbl>       <dbl>        <dbl>       <dbl> <chr>  
##  1          5.1         3.5          1.4         0.2 setosa 
##  2          4.9         3            1.4         0.2 setosa 
##  3          4.7         3.2          1.3         0.2 setosa 
##  4          4.6         3.1          1.5         0.2 setosa 
##  5          5           3.6          1.4         0.2 setosa 
##  6          5.4         3.9          1.7         0.4 setosa 
##  7          4.6         3.4          1.4         0.3 setosa 
##  8          5           3.4          1.5         0.2 setosa 
##  9          4.4         2.9          1.4         0.2 setosa 
## 10          4.9         3.1          1.5         0.1 setosa 
## # … with 140 more rows
```

We see that `read_csv()` did the trick in reading in our data, but we aren't yet able to manipulate it. First we need save it as tibble (an R data frame). We do this using the assignment operator. 

## Using the Assignment Operator

In other programming languages such as Java and Python, if we want to assign something to an object name, we use the `=` assignment operator. But in R, the assignment operator is `<-`. The shortcut is `Option + -` on Mac and `Alt + -` on PC. Let's call our dataset `dat_iris` using the assignment operator.


```r
dat_iris <- read_csv("https://gist.githubusercontent.com/curran/a08a1080b88344b0c8a7/raw/0e7a9b0a5d22642a06d3d5b9bcbad9890c8ee534/iris.csv")
```

Now our data is in an R tibble that we can manipulate as we please.

## Exploring the Data

Remember what we learned last time. As soon as we start working with a dataset, we should explore and get familiar with the data. Go ahead and run some exploratory commands (hint: `head()`, `str()`, `summary()`).


```r
head(dat_iris)
```

```
## # A tibble: 6 x 5
##   sepal_length sepal_width petal_length petal_width species
##          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
## 1          5.1         3.5          1.4         0.2 setosa 
## 2          4.9         3            1.4         0.2 setosa 
## 3          4.7         3.2          1.3         0.2 setosa 
## 4          4.6         3.1          1.5         0.2 setosa 
## 5          5           3.6          1.4         0.2 setosa 
## 6          5.4         3.9          1.7         0.4 setosa
```

```r
summary(dat_iris)
```

```
##   sepal_length    sepal_width     petal_length    petal_width   
##  Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
##  1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
##  Median :5.800   Median :3.000   Median :4.350   Median :1.300  
##  Mean   :5.843   Mean   :3.054   Mean   :3.759   Mean   :1.199  
##  3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
##  Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
##    species         
##  Length:150        
##  Class :character  
##  Mode  :character  
##                    
##                    
## 
```

```r
str(dat_iris)
```

```
## spec_tbl_df[,5] [150 × 5] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ sepal_length: num [1:150] 5.1 4.9 4.7 4.6 5 5.4 4.6 5 4.4 4.9 ...
##  $ sepal_width : num [1:150] 3.5 3 3.2 3.1 3.6 3.9 3.4 3.4 2.9 3.1 ...
##  $ petal_length: num [1:150] 1.4 1.4 1.3 1.5 1.4 1.7 1.4 1.5 1.4 1.5 ...
##  $ petal_width : num [1:150] 0.2 0.2 0.2 0.2 0.2 0.4 0.3 0.2 0.2 0.1 ...
##  $ species     : chr [1:150] "setosa" "setosa" "setosa" "setosa" ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   sepal_length = col_double(),
##   ..   sepal_width = col_double(),
##   ..   petal_length = col_double(),
##   ..   petal_width = col_double(),
##   ..   species = col_character()
##   .. )
```


## Next Time

Next time we'll work on creating some visualizations using tools in the `GGPlot2` library. 

 








