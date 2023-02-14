---
title: "Lab 9 Homework"
author: "Sidney Rang"
date: "2023-02-14"
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
library(here)
library(naniar)
```

For this homework, we will take a departure from biological data and use data about California colleges. These data are a subset of the national college scorecard (https://collegescorecard.ed.gov/data/). Load the `ca_college_data.csv` as a new object called `colleges`.

```r
colleges <-readr::read_csv("data/ca_college_data.csv")
```

```
## Rows: 341 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): INSTNM, CITY, STABBR, ZIP
## dbl (6): ADM_RATE, SAT_AVG, PCIP26, COSTT4_A, C150_4_POOLED, PFTFTUG1_EF
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

The variables are a bit hard to decipher, here is a key:  

INSTNM: Institution name  
CITY: California city  
STABBR: Location state  
ZIP: Zip code  
ADM_RATE: Admission rate  
SAT_AVG: SAT average score  
PCIP26: Percentage of degrees awarded in Biological And Biomedical Sciences  
COSTT4_A: Annual cost of attendance  
C150_4_POOLED: 4-year completion rate  
PFTFTUG1_EF: Percentage of undergraduate students who are first-time, full-time degree/certificate-seeking undergraduate students  

1. Use your preferred function(s) to have a look at the data and get an idea of its structure. Make sure you summarize NA's and determine whether or not the data are tidy. You may also consider dealing with any naming issues.

```r
summary(colleges)
```

```
##     INSTNM              CITY              STABBR              ZIP           
##  Length:341         Length:341         Length:341         Length:341        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     ADM_RATE         SAT_AVG         PCIP26           COSTT4_A    
##  Min.   :0.0807   Min.   : 870   Min.   :0.00000   Min.   : 7956  
##  1st Qu.:0.4581   1st Qu.: 985   1st Qu.:0.00000   1st Qu.:12578  
##  Median :0.6370   Median :1078   Median :0.00000   Median :16591  
##  Mean   :0.5901   Mean   :1112   Mean   :0.01981   Mean   :26685  
##  3rd Qu.:0.7461   3rd Qu.:1237   3rd Qu.:0.02457   3rd Qu.:39289  
##  Max.   :1.0000   Max.   :1555   Max.   :0.21650   Max.   :69355  
##  NA's   :240      NA's   :276    NA's   :35        NA's   :124    
##  C150_4_POOLED     PFTFTUG1_EF    
##  Min.   :0.0625   Min.   :0.0064  
##  1st Qu.:0.4265   1st Qu.:0.3212  
##  Median :0.5845   Median :0.5016  
##  Mean   :0.5705   Mean   :0.5577  
##  3rd Qu.:0.7162   3rd Qu.:0.8117  
##  Max.   :0.9569   Max.   :1.0000  
##  NA's   :221      NA's   :53
```


```r
colleges <-clean_names(colleges)
```


2. Which cities in California have the highest number of colleges?

```r
colleges_city <-colleges %>% 
  count(city) %>% 
  arrange(-n) %>% 
  slice_head(n=10) 
colleges_city
```

```
## # A tibble: 10 × 2
##    city              n
##    <chr>         <int>
##  1 Los Angeles      24
##  2 San Diego        18
##  3 San Francisco    15
##  4 Sacramento       10
##  5 Berkeley          9
##  6 Oakland           9
##  7 Claremont         7
##  8 Pasadena          6
##  9 Fresno            5
## 10 Irvine            5
```

3. Based on your answer to #2, make a plot that shows the number of colleges in the top 10 cities.

```r
colleges_city%>% 
  ggplot(aes(x=city, y=n))+geom_col()+coord_flip()
```

![](lab9_hw_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

4. The column `COSTT4_A` is the annual cost of each institution. Which city has the highest average cost? Where is it located?

```r
cost_of_college <-colleges %>% 
  group_by(city) %>% 
  summarise(mean_cost = mean(costt4_a,na.rm=T)) %>% 
  arrange(desc(mean_cost))
cost_of_college
```

```
## # A tibble: 161 × 2
##    city                mean_cost
##    <chr>                   <dbl>
##  1 Claremont               66498
##  2 Malibu                  66152
##  3 Valencia                64686
##  4 Orange                  64501
##  5 Redlands                61542
##  6 Moraga                  61095
##  7 Atherton                56035
##  8 Thousand Oaks           54373
##  9 Rancho Palos Verdes     50758
## 10 La Verne                50603
## # … with 151 more rows
```

5. Based on your answer to #4, make a plot that compares the cost of the individual colleges in the most expensive city. Bonus! Add UC Davis here to see how it compares :>).

```r
cost_of_college%>% 
  top_n(-10, mean_cost) %>% 
  ggplot(aes(x=city, y=mean_cost))+geom_col()+coord_flip()
```

![](lab9_hw_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

6. The column `ADM_RATE` is the admissions rate by college and `C150_4_POOLED` is the four-year completion rate. Use a scatterplot to show the relationship between these two variables. What do you think this means?

```r
colleges %>%
  select(adm_rate, c150_4_pooled) %>% 
  ggplot(aes(x=adm_rate, y=c150_4_pooled))+geom_point()#when admisson rate is higher, it takes less time to finish the institution, not all of the colleges listed are 4-year colleges
```

```
## Warning: Removed 251 rows containing missing values (`geom_point()`).
```

![](lab9_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

7. Is there a relationship between cost and four-year completion rate? (You don't need to do the stats, just produce a plot). What do you think this means?

```r
colleges %>%
  select(costt4_a, c150_4_pooled) %>% 
  ggplot(aes(x=c150_4_pooled, y=costt4_a))+geom_point()#there is a postive relationship between the two. It can suggest that the longer the time spent at the institution, the more price you pay
```

```
## Warning: Removed 225 rows containing missing values (`geom_point()`).
```

![](lab9_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

8. The column titled `INSTNM` is the institution name. We are only interested in the University of California colleges. Make a new data frame that is restricted to UC institutions. You can remove `Hastings College of Law` and `UC San Francisco` as we are only interested in undergraduate institutions.

```r
colleges %>% 
  filter_all(any_vars(str_detect(.,pattern="University of California")))
```

```
## # A tibble: 10 × 10
##    instnm      city  stabbr zip   adm_r…¹ sat_avg pcip26 costt…² c150_…³ pftft…⁴
##    <chr>       <chr> <chr>  <chr>   <dbl>   <dbl>  <dbl>   <dbl>   <dbl>   <dbl>
##  1 University… La J… CA     92093   0.357    1324  0.216   31043   0.872   0.662
##  2 University… Irvi… CA     92697   0.406    1206  0.107   31198   0.876   0.725
##  3 University… Rive… CA     92521   0.663    1078  0.149   31494   0.73    0.811
##  4 University… Los … CA     9009…   0.180    1334  0.155   33078   0.911   0.661
##  5 University… Davis CA     9561…   0.423    1218  0.198   33904   0.850   0.605
##  6 University… Sant… CA     9506…   0.578    1201  0.193   34608   0.776   0.786
##  7 University… Berk… CA     94720   0.169    1422  0.105   34924   0.916   0.709
##  8 University… Sant… CA     93106   0.358    1281  0.108   34998   0.816   0.708
##  9 University… San … CA     9410…  NA          NA NA          NA  NA      NA    
## 10 University… San … CA     9414…  NA          NA NA          NA  NA      NA    
## # … with abbreviated variable names ¹​adm_rate, ²​costt4_a, ³​c150_4_pooled,
## #   ⁴​pftftug1_ef
```

Remove `Hastings College of Law` and `UC San Francisco` and store the final data frame as a new object `univ_calif_final`.

```r
univ_calif_final <-colleges %>% 
  filter_all(any_vars(str_detect(.,pattern="University of California"))) %>% 
  filter(city != "San Francisco" )
univ_calif_final
```

```
## # A tibble: 8 × 10
##   instnm       city  stabbr zip   adm_r…¹ sat_avg pcip26 costt…² c150_…³ pftft…⁴
##   <chr>        <chr> <chr>  <chr>   <dbl>   <dbl>  <dbl>   <dbl>   <dbl>   <dbl>
## 1 University … La J… CA     92093   0.357    1324  0.216   31043   0.872   0.662
## 2 University … Irvi… CA     92697   0.406    1206  0.107   31198   0.876   0.725
## 3 University … Rive… CA     92521   0.663    1078  0.149   31494   0.73    0.811
## 4 University … Los … CA     9009…   0.180    1334  0.155   33078   0.911   0.661
## 5 University … Davis CA     9561…   0.423    1218  0.198   33904   0.850   0.605
## 6 University … Sant… CA     9506…   0.578    1201  0.193   34608   0.776   0.786
## 7 University … Berk… CA     94720   0.169    1422  0.105   34924   0.916   0.709
## 8 University … Sant… CA     93106   0.358    1281  0.108   34998   0.816   0.708
## # … with abbreviated variable names ¹​adm_rate, ²​costt4_a, ³​c150_4_pooled,
## #   ⁴​pftftug1_ef
```

Use `separate()` to separate institution name into two new columns "UNIV" and "CAMPUS".

```r
univ_calif_final %>% 
  separate(instnm, into= c("UNIV", "CAMPUS"), sep = "-") 
```

```
## # A tibble: 8 × 11
##   UNIV  CAMPUS city  stabbr zip   adm_r…¹ sat_avg pcip26 costt…² c150_…³ pftft…⁴
##   <chr> <chr>  <chr> <chr>  <chr>   <dbl>   <dbl>  <dbl>   <dbl>   <dbl>   <dbl>
## 1 Univ… San D… La J… CA     92093   0.357    1324  0.216   31043   0.872   0.662
## 2 Univ… Irvine Irvi… CA     92697   0.406    1206  0.107   31198   0.876   0.725
## 3 Univ… River… Rive… CA     92521   0.663    1078  0.149   31494   0.73    0.811
## 4 Univ… Los A… Los … CA     9009…   0.180    1334  0.155   33078   0.911   0.661
## 5 Univ… Davis  Davis CA     9561…   0.423    1218  0.198   33904   0.850   0.605
## 6 Univ… Santa… Sant… CA     9506…   0.578    1201  0.193   34608   0.776   0.786
## 7 Univ… Berke… Berk… CA     94720   0.169    1422  0.105   34924   0.916   0.709
## 8 Univ… Santa… Sant… CA     93106   0.358    1281  0.108   34998   0.816   0.708
## # … with abbreviated variable names ¹​adm_rate, ²​costt4_a, ³​c150_4_pooled,
## #   ⁴​pftftug1_ef
```

9. The column `ADM_RATE` is the admissions rate by campus. Which UC has the lowest and highest admissions rates? Produce a numerical summary and an appropriate plot.

```r
univ_calif_final %>% 
  select(instnm, adm_rate) %>% 
  group_by(instnm) %>% 
  arrange(desc(adm_rate))
```

```
## # A tibble: 8 × 2
## # Groups:   instnm [8]
##   instnm                                 adm_rate
##   <chr>                                     <dbl>
## 1 University of California-Riverside        0.663
## 2 University of California-Santa Cruz       0.578
## 3 University of California-Davis            0.423
## 4 University of California-Irvine           0.406
## 5 University of California-Santa Barbara    0.358
## 6 University of California-San Diego        0.357
## 7 University of California-Los Angeles      0.180
## 8 University of California-Berkeley         0.169
```


```r
univ_calif_final %>% 
  select(instnm, adm_rate) %>% 
  group_by(instnm) %>% 
  arrange(desc(adm_rate)) %>% 
  ggplot(aes(x=instnm, y=adm_rate)) + 
  geom_col()+
  coord_flip()
```

![](lab9_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

10. If you wanted to get a degree in biological or biomedical sciences, which campus confers the majority of these degrees? Produce a numerical summary and an appropriate plot.

```r
univ_calif_final %>% 
  select(instnm, pcip26) %>% 
  group_by(instnm) %>% 
  arrange(desc(pcip26))
```

```
## # A tibble: 8 × 2
## # Groups:   instnm [8]
##   instnm                                 pcip26
##   <chr>                                   <dbl>
## 1 University of California-San Diego      0.216
## 2 University of California-Davis          0.198
## 3 University of California-Santa Cruz     0.193
## 4 University of California-Los Angeles    0.155
## 5 University of California-Riverside      0.149
## 6 University of California-Santa Barbara  0.108
## 7 University of California-Irvine         0.107
## 8 University of California-Berkeley       0.105
```


```r
univ_calif_final %>% 
  select(instnm, pcip26) %>% 
  group_by(instnm) %>% 
  arrange(desc(pcip26)) %>% 
  ggplot(aes(x=instnm, y=pcip26)) + 
  geom_col()+
  coord_flip()
```

![](lab9_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

## Knit Your Output and Post to [GitHub](https://github.com/FRS417-DataScienceBiologists)
