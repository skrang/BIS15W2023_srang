---
title: "BIS 15L Midterm 2"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. To receive full credit, all plots must have clearly labeled axes, a title, and consistent aesthetics. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library("tidyverse")
library("janitor")
library("naniar")
```

## Data
These data are from a study on surgical residents. The study was originally published by Sessier et al. “Operation Timing and 30-Day Mortality After Elective General Surgery”. Anesth Analg 2011; 113: 1423-8. The data were cleaned for instructional use by Amy S. Nowacki, “Surgery Timing Dataset”, TSHS Resources Portal (2016). Available at https://www.causeweb.org/tshs/surgery-timing/.

Descriptions of the variables and the study are included as pdf's in the data folder.  

Please run the following chunk to import the data.

```r
surgery <- read_csv("data/surgery.csv")
```

1. (2 points) Use the summary function(s) of your choice to explore the data and get an idea of its structure. Please also check for NA's.

```r
summary(surgery)
```

```
##    ahrq_ccs              age           gender              race          
##  Length:32001       Min.   : 1.00   Length:32001       Length:32001      
##  Class :character   1st Qu.:48.20   Class :character   Class :character  
##  Mode  :character   Median :58.60   Mode  :character   Mode  :character  
##                     Mean   :57.66                                        
##                     3rd Qu.:68.30                                        
##                     Max.   :90.00                                        
##                     NA's   :2                                            
##   asa_status             bmi        baseline_cancer    baseline_cvd      
##  Length:32001       Min.   : 2.15   Length:32001       Length:32001      
##  Class :character   1st Qu.:24.60   Class :character   Class :character  
##  Mode  :character   Median :28.19   Mode  :character   Mode  :character  
##                     Mean   :29.45                                        
##                     3rd Qu.:32.81                                        
##                     Max.   :92.59                                        
##                     NA's   :3290                                         
##  baseline_dementia  baseline_diabetes  baseline_digestive baseline_osteoart 
##  Length:32001       Length:32001       Length:32001       Length:32001      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  baseline_psych     baseline_pulmonary baseline_charlson mortality_rsi    
##  Length:32001       Length:32001       Min.   : 0.000    Min.   :-4.4000  
##  Class :character   Class :character   1st Qu.: 0.000    1st Qu.:-1.2400  
##  Mode  :character   Mode  :character   Median : 0.000    Median :-0.3000  
##                                        Mean   : 1.184    Mean   :-0.5316  
##                                        3rd Qu.: 2.000    3rd Qu.: 0.0000  
##                                        Max.   :13.000    Max.   : 4.8600  
##                                                                           
##  complication_rsi  ccsmort30rate      ccscomplicationrate      hour      
##  Min.   :-4.7200   Min.   :0.000000   Min.   :0.01612     Min.   : 6.00  
##  1st Qu.:-0.8400   1st Qu.:0.000789   1st Qu.:0.08198     1st Qu.: 7.65  
##  Median :-0.2700   Median :0.002764   Median :0.10937     Median : 9.65  
##  Mean   :-0.4091   Mean   :0.004312   Mean   :0.13325     Mean   :10.38  
##  3rd Qu.: 0.0000   3rd Qu.:0.007398   3rd Qu.:0.18337     3rd Qu.:12.72  
##  Max.   :13.3000   Max.   :0.016673   Max.   :0.46613     Max.   :19.00  
##                                                                          
##      dow               month            moonphase            mort30         
##  Length:32001       Length:32001       Length:32001       Length:32001      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  complication      
##  Length:32001      
##  Class :character  
##  Mode  :character  
##                    
##                    
##                    
## 
```

2. (3 points) Let's explore the participants in the study. Show a count of participants by race AND make a plot that visually represents your output.

```r
surgery %>% 
  group_by(race) %>% 
  count(race)
```

```
## # A tibble: 4 × 2
## # Groups:   race [4]
##   race                 n
##   <chr>            <int>
## 1 African American  3790
## 2 Caucasian        26488
## 3 Other             1243
## 4 <NA>               480
```

```r
surgery %>% 
  group_by(race) %>% 
  ggplot(aes(x=race, fill=race))+
  geom_bar()+
  labs(title = "Particpants by Race",
       x = "Race",
       y = "Number of Patients")
```

![](midterm_2_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

3. (2 points) What is the mean age of participants by gender? (hint: please provide a number for each) Since only three participants do not have gender indicated, remove these participants from the data.

```r
surgery %>% 
  filter(!is.na(gender)) %>% 
  group_by(gender) %>% 
  summarize(avg_age = mean(age,na.rm=T))
```

```
## # A tibble: 2 × 2
##   gender avg_age
##   <chr>    <dbl>
## 1 F         56.7
## 2 M         58.8
```


4. (3 points) Make a plot that shows the range of age associated with gender.

```r
surgery %>% 
  filter(!is.na(gender)) %>% 
  group_by(gender) %>% 
  ggplot(aes(x=age, y=gender, fill=gender))+
  geom_boxplot()+
  labs(title = "Average Age Among Gender",
       x = "Age",
       y = "Gender")
```

```
## Warning: Removed 2 rows containing non-finite values (`stat_boxplot()`).
```

![](midterm_2_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

5. (2 points) How healthy are the participants? The variable `asa_status` is an evaluation of patient physical status prior to surgery. Lower numbers indicate fewer comorbidities (presence of two or more diseases or medical conditions in a patient). Make a plot that compares the number of `asa_status` I-II, III, and IV-V.

```r
surgery %>% 
  filter(!is.na(asa_status)) %>%
  group_by(asa_status) %>% 
  ggplot(aes(x=asa_status,  fill=asa_status))+
  geom_bar()+
  labs(title = "Patient Evaluation Prior to Surgery",
       x = "Status",
       y = "Number of Patients")
```

![](midterm_2_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

6. (3 points) Create a plot that displays the distribution of body mass index for each `asa_status` as a probability distribution- not a histogram. (hint: use faceting!)

```r
surgery %>% 
  filter(!is.na(asa_status)) %>%
  ggplot(aes(x=bmi, fill=asa_status)) +
  geom_density()+
  facet_wrap(.~asa_status)+
  labs(title = "Distribution of BMI in each ASA Status",
       x = "Body Mass Index",
       y = "Density")
```

```
## Warning: Removed 3289 rows containing non-finite values (`stat_density()`).
```

![](midterm_2_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

The variable `ccsmort30rate` is a measure of the overall 30-day mortality rate associated with each type of operation. The variable `ccscomplicationrate` is a measure of the 30-day in-hospital complication rate. The variable `ahrq_ccs` lists each type of operation.  

7. (4 points) What are the 5 procedures associated with highest risk of 30-day mortality AND how do they compare with the 5 procedures with highest risk of complication? (hint: no need for a plot here)

```r
surgery %>% 
  group_by(ahrq_ccs) %>% 
  summarize(mortality_mean=mean(mortality_rsi)) %>% 
  top_n(5, mortality_mean) %>% 
  arrange(desc(mortality_mean))
```

```
## # A tibble: 5 × 2
##   ahrq_ccs                               mortality_mean
##   <chr>                                           <dbl>
## 1 Gastrectomy; partial and total                 0.533 
## 2 Small bowel resection                          0.398 
## 3 Colorectal resection                           0.114 
## 4 Oophorectomy; unilateral and bilateral         0.0235
## 5 Other hernia repair                           -0.0224
```


```r
surgery %>% 
  group_by(ahrq_ccs) %>% 
  summarize(complication_mean=mean(complication_rsi)) %>% 
  top_n(5, complication_mean) %>% 
  arrange(desc(complication_mean))
```

```
## # A tibble: 5 × 2
##   ahrq_ccs                               complication_mean
##   <chr>                                              <dbl>
## 1 Small bowel resection                             0.686 
## 2 Colorectal resection                              0.275 
## 3 Nephrectomy; partial or complete                 -0.0212
## 4 Oophorectomy; unilateral and bilateral           -0.0455
## 5 Gastrectomy; partial and total                   -0.0605
```


8. (3 points) Make a plot that compares the `ccsmort30rate` for all listed `ahrq_ccs` procedures.

```r
surgery %>% 
  ggplot(aes(x=ahrq_ccs, y=ccsmort30rate))+
  geom_col()+ 
  theme(axis.title = element_text(size = 10),
        axis.text.x = element_text(angle=75, hjust = 1, size=4))+
  labs(title = "30 Day Mortality Rate in Each Procedure",
       x = NULL,
       y = "Rate")
```

![](midterm_2_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


9. (4 points) When is the best month to have surgery? Make a chart that shows the 30-day mortality and complications for the patients by month. `mort30` is the variable that shows whether or not a patient survived 30 days post-operation.


```r
surgery %>% 
  tabyl(mort30, month)
```

```
##  mort30  Apr  Aug  Dec  Feb  Jan  Jul  Jun  Mar  May  Nov  Oct  Sep
##      No 2686 3168 1835 2489 2651 2313 2980 2685 2644 2539 2681 3192
##     Yes   12    9    4   17   19   12   14   12   10    5    8   16
```


```r
surgery %>% 
  tabyl(complication, month)
```

```
##  complication  Apr  Aug  Dec  Feb  Jan  Jul  Jun  Mar  May  Nov  Oct  Sep
##            No 2377 2715 1602 2163 2263 2024 2584 2373 2321 2219 2312 2784
##           Yes  321  462  237  343  407  301  410  324  333  325  377  424
```

10. (4 points) Make a plot that visualizes the chart from question #9. Make sure that the months are on the x-axis. Do a search online and figure out how to order the months Jan-Dec.
surgery %>% 

```r
surgery %>% 
  group_by(month) %>% 
  ggplot(aes(x=mort30, fill=month))+
  geom_bar()+
  labs(title = "30 Day Mortality in Each Month",
       x = NULL,
       y = "Mortality")
```

![](midterm_2_files/figure-html/unnamed-chunk-15-1.png)<!-- -->
 

```r
surgery %>% 
  group_by(month) %>% 
  ggplot(aes(x=complication, fill=month))+
  geom_bar()+
  labs(title = "Complications in Month",
       x = NULL,
       y = "Complications")
```

![](midterm_2_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

Please provide the names of the students you have worked with with during the exam:

```r
#Group5
```

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
