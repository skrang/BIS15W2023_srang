---
title: "Lab 8 Homework"
author: "Sidney Rang"
date: "2023-02-09"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
```

## Install `here`
The package `here` is a nice option for keeping directories clear when loading files. I will demonstrate below and let you decide if it is something you want to use.  

```r
#install.packages("here")
```

## Data
For this homework, we will use a data set compiled by the Office of Environment and Heritage in New South Whales, Australia. It contains the enterococci counts in water samples obtained from Sydney beaches as part of the Beachwatch Water Quality Program. Enterococci are bacteria common in the intestines of mammals; they are rarely present in clean water. So, enterococci values are a measurement of pollution. `cfu` stands for colony forming units and measures the number of viable bacteria in a sample [cfu](https://en.wikipedia.org/wiki/Colony-forming_unit).   

This homework loosely follows the tutorial of [R Ladies Sydney](https://rladiessydney.org/). If you get stuck, check it out!  

1. Start by loading the data `sydneybeaches`. Do some exploratory analysis to get an idea of the data structure.

```r
sydneybeaches <-read_csv("data/sydneybeaches.csv")
```

```
## Rows: 3690 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Region, Council, Site, Date
## dbl (4): BeachId, Longitude, Latitude, Enterococci (cfu/100ml)
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
summary(sydneybeaches)
```

```
##     BeachId         Region            Council              Site          
##  Min.   :22.00   Length:3690        Length:3690        Length:3690       
##  1st Qu.:24.00   Class :character   Class :character   Class :character  
##  Median :26.00   Mode  :character   Mode  :character   Mode  :character  
##  Mean   :25.87                                                           
##  3rd Qu.:27.40                                                           
##  Max.   :29.00                                                           
##                                                                          
##    Longitude        Latitude          Date           Enterococci (cfu/100ml)
##  Min.   :151.3   Min.   :-33.98   Length:3690        Min.   :   0.00        
##  1st Qu.:151.3   1st Qu.:-33.95   Class :character   1st Qu.:   1.00        
##  Median :151.3   Median :-33.92   Mode  :character   Median :   5.00        
##  Mean   :151.3   Mean   :-33.93                      Mean   :  33.92        
##  3rd Qu.:151.3   3rd Qu.:-33.90                      3rd Qu.:  17.00        
##  Max.   :151.3   Max.   :-33.89                      Max.   :4900.00        
##                                                      NA's   :29
```

If you want to try `here`, first notice the output when you load the `here` library. It gives you information on the current working directory. You can then use it to easily and intuitively load files.

```r
library(here)
```

```
## here() starts at /Users/sidneyrang/Desktop/BIS15W2023_srang-main/lab8
```

The quotes show the folder structure from the root directory.

```r
sydneybeaches <-read_csv(here( "data", "sydneybeaches.csv")) %>% janitor::clean_names()
```

```
## Rows: 3690 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Region, Council, Site, Date
## dbl (4): BeachId, Longitude, Latitude, Enterococci (cfu/100ml)
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

2. Are these data "tidy" per the definitions of the tidyverse? How do you know? Are they in wide or long format?

```r
sydneybeaches #not tidydata;by defintion the site variable should each have their own column  the data is in long format 
```

```
## # A tibble: 3,690 × 8
##    beach_id region                   council site  longi…¹ latit…² date  enter…³
##       <dbl> <chr>                    <chr>   <chr>   <dbl>   <dbl> <chr>   <dbl>
##  1       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 02/0…      19
##  2       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 06/0…       3
##  3       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 12/0…       2
##  4       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 18/0…      13
##  5       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 30/0…       8
##  6       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 05/0…       7
##  7       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 11/0…      11
##  8       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 23/0…      97
##  9       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 07/0…       3
## 10       25 Sydney City Ocean Beach… Randwi… Clov…    151.   -33.9 25/0…       0
## # … with 3,680 more rows, and abbreviated variable names ¹​longitude, ²​latitude,
## #   ³​enterococci_cfu_100ml
```


3. We are only interested in the variables site, date, and enterococci_cfu_100ml. Make a new object focused on these variables only. Name the object `sydneybeaches_long`


```r
sydneybeaches_long <-sydneybeaches %>% 
  select("site", "date", "enterococci_cfu_100ml")
sydneybeaches_long
```

```
## # A tibble: 3,690 × 3
##    site           date       enterococci_cfu_100ml
##    <chr>          <chr>                      <dbl>
##  1 Clovelly Beach 02/01/2013                    19
##  2 Clovelly Beach 06/01/2013                     3
##  3 Clovelly Beach 12/01/2013                     2
##  4 Clovelly Beach 18/01/2013                    13
##  5 Clovelly Beach 30/01/2013                     8
##  6 Clovelly Beach 05/02/2013                     7
##  7 Clovelly Beach 11/02/2013                    11
##  8 Clovelly Beach 23/02/2013                    97
##  9 Clovelly Beach 07/03/2013                     3
## 10 Clovelly Beach 25/03/2013                     0
## # … with 3,680 more rows
```

4. Pivot the data such that the dates are column names and each beach only appears once. Name the object `sydneybeaches_wide`

```r
sydneybeaches_wide <- sydneybeaches %>%
  select("site", "date", "enterococci_cfu_100ml") %>% 
  pivot_wider(names_from = "site",
              values_from = "enterococci_cfu_100ml")
sydneybeaches_wide
```

```
## # A tibble: 344 × 12
##    date  Clove…¹ Cooge…² Gordo…³ Littl…⁴ Malab…⁵ Marou…⁶ South…⁷ South…⁸ Bondi…⁹
##    <chr>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1 02/0…      19      15      NA       9       2       1       1      12       3
##  2 06/0…       3       4      NA       3       4       1       0       2       1
##  3 12/0…       2      17      NA      72     390      20      33     110       2
##  4 18/0…      13      18      NA       1      15       2       2      13       1
##  5 30/0…       8      22      NA      44      13      11      13     100       6
##  6 05/0…       7       2      NA       7      13       0       0     630       5
##  7 11/0…      11     110      NA     150     140       4      30      79     600
##  8 23/0…      97     630      NA     330     390      60      92     570      67
##  9 07/0…       3      11      NA      31       6       1      13      69       1
## 10 25/0…       0      82       4     420      28      33      17      37       0
## # … with 334 more rows, 2 more variables: `Bronte Beach` <dbl>,
## #   `Tamarama Beach` <dbl>, and abbreviated variable names ¹​`Clovelly Beach`,
## #   ²​`Coogee Beach`, ³​`Gordons Bay (East)`, ⁴​`Little Bay Beach`,
## #   ⁵​`Malabar Beach`, ⁶​`Maroubra Beach`, ⁷​`South Maroubra Beach`,
## #   ⁸​`South Maroubra Rockpool`, ⁹​`Bondi Beach`
```


5. Pivot the data back so that the dates are data and not column names.

```r
sydneybeaches_wide %>% 
  pivot_longer(-date,
               names_to = "site",
               values_to = "enterococci_cfu_100ml")
```

```
## # A tibble: 3,784 × 3
##    date       site                    enterococci_cfu_100ml
##    <chr>      <chr>                                   <dbl>
##  1 02/01/2013 Clovelly Beach                             19
##  2 02/01/2013 Coogee Beach                               15
##  3 02/01/2013 Gordons Bay (East)                         NA
##  4 02/01/2013 Little Bay Beach                            9
##  5 02/01/2013 Malabar Beach                               2
##  6 02/01/2013 Maroubra Beach                              1
##  7 02/01/2013 South Maroubra Beach                        1
##  8 02/01/2013 South Maroubra Rockpool                    12
##  9 02/01/2013 Bondi Beach                                 3
## 10 02/01/2013 Bronte Beach                                4
## # … with 3,774 more rows
```


6. We haven't dealt much with dates yet, but separate the date into columns day, month, and year. Do this on the `sydneybeaches_long` data.

```r
sydneybeaches_long_dates <-sydneybeaches_long %>% 
  separate(date, into = c("day", "month", "year"),sep = "/")
sydneybeaches_long_dates
```

```
## # A tibble: 3,690 × 5
##    site           day   month year  enterococci_cfu_100ml
##    <chr>          <chr> <chr> <chr>                 <dbl>
##  1 Clovelly Beach 02    01    2013                     19
##  2 Clovelly Beach 06    01    2013                      3
##  3 Clovelly Beach 12    01    2013                      2
##  4 Clovelly Beach 18    01    2013                     13
##  5 Clovelly Beach 30    01    2013                      8
##  6 Clovelly Beach 05    02    2013                      7
##  7 Clovelly Beach 11    02    2013                     11
##  8 Clovelly Beach 23    02    2013                     97
##  9 Clovelly Beach 07    03    2013                      3
## 10 Clovelly Beach 25    03    2013                      0
## # … with 3,680 more rows
```


7. What is the average `enterococci_cfu_100ml` by year for each beach. Think about which data you will use- long or wide.

```r
mean_en <-sydneybeaches_long_dates %>% 
  group_by(site,year) %>% 
  summarize(mean_enterococci_cfu_100ml = mean(enterococci_cfu_100ml, na.rm=T))
```

```
## `summarise()` has grouped output by 'site'. You can override using the
## `.groups` argument.
```

```r
mean_en
```

```
## # A tibble: 66 × 3
## # Groups:   site [11]
##    site         year  mean_enterococci_cfu_100ml
##    <chr>        <chr>                      <dbl>
##  1 Bondi Beach  2013                        32.2
##  2 Bondi Beach  2014                        11.1
##  3 Bondi Beach  2015                        14.3
##  4 Bondi Beach  2016                        19.4
##  5 Bondi Beach  2017                        13.2
##  6 Bondi Beach  2018                        22.9
##  7 Bronte Beach 2013                        26.8
##  8 Bronte Beach 2014                        17.5
##  9 Bronte Beach 2015                        23.6
## 10 Bronte Beach 2016                        61.3
## # … with 56 more rows
```


8. Make the output from question 7 easier to read by pivoting it to wide format.

```r
mean_en %>% 
  pivot_wider(names_from = "site",
              values_from = "mean_enterococci_cfu_100ml")
```

```
## # A tibble: 6 × 12
##   year  Bondi …¹ Bront…² Clove…³ Cooge…⁴ Gordo…⁵ Littl…⁶ Malab…⁷ Marou…⁸ South…⁹
##   <chr>    <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
## 1 2013      32.2    26.8    9.28    39.7    24.8   122.    101.    47.1    39.3 
## 2 2014      11.1    17.5   13.8     52.6    16.7    19.5    54.5    9.23   14.9 
## 3 2015      14.3    23.6    8.82    40.3    36.2    25.5    66.9   14.5     8.25
## 4 2016      19.4    61.3   11.3     59.5    39.0    31.2    91.0   26.6    10.7 
## 5 2017      13.2    16.8    7.93    20.7    13.7    18.2    49.8   11.6     8.26
## 6 2018      22.9    43.4   10.6     21.6    17.6    59.1    38.0    9.21   12.5 
## # … with 2 more variables: `South Maroubra Rockpool` <dbl>,
## #   `Tamarama Beach` <dbl>, and abbreviated variable names ¹​`Bondi Beach`,
## #   ²​`Bronte Beach`, ³​`Clovelly Beach`, ⁴​`Coogee Beach`, ⁵​`Gordons Bay (East)`,
## #   ⁶​`Little Bay Beach`, ⁷​`Malabar Beach`, ⁸​`Maroubra Beach`,
## #   ⁹​`South Maroubra Beach`
```


9. What was the most polluted beach in 2018?

```r
sydneybeaches_long_dates %>% 
  group_by(site) %>% 
  filter(year == 2018) %>% 
  summarize(max_enterocci = max(enterococci_cfu_100ml, na.rm=T)) %>% 
  arrange(desc(max_enterocci))
```

```
## # A tibble: 11 × 2
##    site                    max_enterocci
##    <chr>                           <dbl>
##  1 Little Bay Beach                 2100
##  2 South Maroubra Rockpool          1700
##  3 Bronte Beach                     1400
##  4 Coogee Beach                      360
##  5 Gordons Bay (East)                340
##  6 Malabar Beach                     320
##  7 South Maroubra Beach              300
##  8 Bondi Beach                       250
##  9 Tamarama Beach                    140
## 10 Maroubra Beach                    110
## 11 Clovelly Beach                     71
```


10. Please complete the class project survey at: [BIS 15L Group Project](https://forms.gle/H2j69Z3ZtbLH3efW6)


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
