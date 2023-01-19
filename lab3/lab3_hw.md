---
title: "Lab 3 Homework"
author: "Sidney Rang"
date: "2023-01-18"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions

Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!

## Load the tidyverse


```r
library(tidyverse)
```

## Mammals Sleep

1.  For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.


```r
help(msleep)
```

2.  Store these data into a new data frame `sleep`.


```r
sleep <-msleep
```

3.  What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.


```r
dim(sleep)
```

```
## [1] 83 11
```

There are 83 variables and 11 observations

4.  Are there any NAs in the data? How did you determine this? Please show your code.\
    There are a total of 136 NAs in the data frame.


```r
sum(is.na(sleep))
```

```
## [1] 136
```

5.  Show a list of the column names is this data frame.


```r
colnames(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

6.  How many herbivores are represented in the data?


```r
table(sleep$vore)
```

```
## 
##   carni   herbi insecti    omni 
##      19      32       5      20
```

There are 32 herbivores.

7.  We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.


```r
small_mammals <-filter(sleep, bodywt<=1)
small_mammals
```

```
## # A tibble: 36 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  2 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  3 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  4 Guin… Cavis herbi Rode… domest…     9.4     0.8   0.217  14.6  0.0055   0.728
##  5 Chin… Chin… herbi Rode… domest…    12.5     1.5   0.117  11.5  0.0064   0.42 
##  6 Star… Cond… omni  Sori… lc         10.3     2.2  NA      13.7  0.001    0.06 
##  7 Afri… Cric… omni  Rode… <NA>        8.3     2    NA      15.7  0.0066   1    
##  8 Less… Cryp… omni  Sori… lc          9.1     1.4   0.15   14.9  0.00014  0.005
##  9 Big … Epte… inse… Chir… lc         19.7     3.9   0.117   4.3  0.0003   0.023
## 10 Euro… Erin… omni  Erin… lc         10.1     3.5   0.283  13.9  0.0035   0.77 
## # … with 26 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```


```r
large_mammals <-filter(sleep, bodywt<=200)
large_mammals
```

```
## # A tibble: 76 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Chee… Acin… carni Carn… lc         12.1    NA    NA      11.9 NA       50    
##  2 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  3 Moun… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA        1.35 
##  4 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  5 Thre… Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA        3.85 
##  6 Nort… Call… carni Carn… vu          8.7     1.4   0.383  15.3 NA       20.5  
##  7 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  8 Dog   Canis carni Carn… domest…    10.1     2.9   0.333  13.9  0.07    14    
##  9 Roe … Capr… herbi Arti… lc          3      NA    NA      21    0.0982  14.8  
## 10 Goat  Capri herbi Arti… lc          5.3     0.6  NA      18.7  0.115   33.5  
## # … with 66 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

8.  What is the mean weight for both the small and large mammals?


```r
sw <-small_mammals$bodywt
sw
```

```
##  [1] 0.480 0.019 0.045 0.728 0.420 0.060 1.000 0.005 0.023 0.770 0.071 0.200
## [13] 0.370 0.053 0.120 0.035 0.022 0.010 0.266 0.210 0.028 0.550 0.021 0.320
## [25] 0.044 0.743 0.075 0.148 0.122 0.920 0.101 0.205 0.048 0.112 0.900 0.104
```


```r
mean(sw)
```

```
## [1] 0.2596667
```


```r
lw <-large_mammals$bodywt
lw
```

```
##  [1]  50.000   0.480   1.350   0.019   3.850  20.490   0.045  14.000  14.800
## [10]  33.500   0.728   4.750   0.420   0.060   1.000   0.005   3.500   2.950
## [19]   1.700   0.023 187.000   0.770  10.000   0.071   3.300   0.200  85.000
## [28]   2.625  62.000   1.670   0.370   6.800   0.053   0.120   0.035   0.022
## [37]   0.010   0.266   1.400   0.210   0.028   2.500  55.500  52.200 162.564
## [46] 100.000 161.499  25.235   0.550   1.100   0.021   1.620  86.000  53.180
## [55]   1.100  60.000   3.600   0.320   0.044   0.743   0.075   0.148   0.122
## [64]   0.920   0.101   0.205   0.048  86.250   4.500   0.112   0.900   0.104
## [73] 173.330   2.000   3.380   4.230
```


```r
mean(lw)
```

```
## [1] 20.52396
```

9.  Using a similar approach as above, do large or small animals sleep longer on average?

    Small mammals sleep longer on average compared to large mammals.


```r
sleep_small <-small_mammals$sleep_total
sleep_small
```

```
##  [1] 17.0 14.9  7.0  9.4 12.5 10.3  8.3  9.1 19.7 10.1 14.9  9.8 19.4 14.2 14.3
## [16] 12.8 12.5 19.9 14.6  7.7 14.5 10.3 11.5 13.0  8.7  9.6  8.4 11.3 10.6 16.6
## [31] 13.8 15.9 12.8 15.8 15.6  8.9
```


```r
mean(sleep_small)
```

```
## [1] 12.65833
```


```r
sleep_large <-large_mammals$sleep_total
sleep_large
```

```
##  [1] 12.1 17.0 14.4 14.9 14.4  8.7  7.0 10.1  3.0  5.3  9.4 10.0 12.5 10.3  8.3
## [16]  9.1 17.4  5.3 18.0 19.7  3.1 10.1 10.9 14.9 12.5  9.8  6.2  6.3  8.0  9.5
## [31] 19.4 10.1 14.2 14.3 12.8 12.5 19.9 14.6 11.0  7.7 14.5  8.4  3.8  9.7 15.8
## [46] 10.4 13.5  9.4 10.3 11.0 11.5 13.7  3.5  5.6 11.1 18.1  5.4 13.0  8.7  9.6
## [61]  8.4 11.3 10.6 16.6 13.8 15.9 12.8  9.1  8.6 15.8 15.6  8.9  5.2  6.3 12.5
## [76]  9.8
```


```r
mean(sleep_large)
```

```
## [1] 11.09079
```

10. Which animal is the sleepiest among the entire dataframe? Little brown rat sleeps the longest


```r
max(sleep$sleep_total)
```

```
## [1] 19.9
```

## Push your final code to GitHub!

Please be sure that you check the `keep md` file in the knit preferences.
