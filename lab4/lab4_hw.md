---
title: "Lab 4 Homework"
author: "Sidney Rang"
date: "2023-01-23"
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

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <-readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```


```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
class(homerange)
```

```
## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"
```


```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon <-as.factor(homerange$taxon)
```


```r
homerange$order <-as.factor(homerange$order)
```



```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```


```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tetraodontiformes\xa0" "tinamiformes"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  


```r
taxa <-select(homerange,taxon, common.name, class, order, family, genus, species )
taxa
```

```
## # A tibble: 569 × 7
##    taxon         common.name             class        order family genus species
##    <fct>         <chr>                   <chr>        <fct> <chr>  <chr> <chr>  
##  1 lake fishes   american eel            actinoptery… angu… angui… angu… rostra…
##  2 river fishes  blacktail redhorse      actinoptery… cypr… catos… moxo… poecil…
##  3 river fishes  central stoneroller     actinoptery… cypr… cypri… camp… anomal…
##  4 river fishes  rosyside dace           actinoptery… cypr… cypri… clin… fundul…
##  5 river fishes  longnose dace           actinoptery… cypr… cypri… rhin… catara…
##  6 river fishes  muskellunge             actinoptery… esoc… esoci… esox  masqui…
##  7 marine fishes pollack                 actinoptery… gadi… gadid… poll… pollac…
##  8 marine fishes saithe                  actinoptery… gadi… gadid… poll… virens 
##  9 marine fishes lined surgeonfish       actinoptery… perc… acant… acan… lineat…
## 10 marine fishes orangespine unicornfish actinoptery… perc… acant… naso  litura…
## # … with 559 more rows
```


**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
select(taxa,contains("taxon"))
```

```
## # A tibble: 569 × 1
##    taxon        
##    <fct>        
##  1 lake fishes  
##  2 river fishes 
##  3 river fishes 
##  4 river fishes 
##  5 river fishes 
##  6 river fishes 
##  7 marine fishes
##  8 marine fishes
##  9 marine fishes
## 10 marine fishes
## # … with 559 more rows
```


**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  


```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivores <-filter(homerange, trophic.guild !="herbivore")
```


```r
herbivores <-filter(homerange, trophic.guild !="carnivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
hra <--(carnivores$mean.hra.m2)
```


```r
mean(hra)
```

```
## [1] -13039918
```


```r
hra_h <-(herbivores$mean.hra.m2)
```


```r
na.omit(hra_h)
```

```
##   [1] 1.113000e+01 3.209286e+04 1.790000e+04 5.200000e-01 3.442300e+04
##   [6] 1.130000e+00 1.850000e+01 2.580000e+00 5.400000e-01 2.250000e+00
##  [11] 5.000000e-02 7.400000e+00 7.830000e+03 1.720000e+02 2.444278e+04
##  [16] 2.870000e+02 1.650000e+02 1.750000e+02 7.200000e+01 4.948214e+04
##  [21] 4.591200e+07 2.589980e+03 2.540000e+06 6.358500e+07 1.030000e+05
##  [26] 1.815822e+07 1.699677e+04 2.589984e+04 6.200000e+04 1.975000e+06
##  [31] 5.500000e+06 1.203000e+07 4.300000e+04 1.323320e+05 3.090000e+04
##  [36] 1.618740e+04 2.589984e+04 3.140000e+06 9.500000e+04 1.950000e+05
##  [41] 2.450000e+06 2.388000e+07 8.430000e+07 2.428110e+04 1.012535e+07
##  [46] 3.224482e+06 2.176858e+06 9.050030e+06 2.657786e+08 1.014051e+07
##  [51] 6.452827e+07 7.000032e+05 4.161693e+05 3.570015e+05 1.872837e+06
##  [56] 2.733317e+04 2.328574e+07 5.882474e+06 2.754482e+07 6.199976e+05
##  [61] 3.408003e+06 5.239984e+07 3.710906e+04 1.070040e+09 9.382531e+07
##  [66] 3.647707e+06 6.746368e+05 7.486520e+07 8.514909e+05 9.850086e+05
##  [71] 1.620541e+05 3.507276e+07 2.488342e+06 7.900053e+06 1.976651e+05
##  [76] 3.550831e+09 1.365369e+08 5.899973e+06 1.742007e+06 1.097994e+07
##  [81] 2.486223e+06 1.459990e+07 1.919995e+05 1.024991e+06 4.487040e+03
##  [86] 2.792480e+05 4.135043e+06 1.930012e+04 6.413277e+05 9.149977e+05
##  [91] 3.236533e+06 6.133382e+06 9.709123e+05 1.630009e+05 7.739983e+06
##  [96] 1.190008e+05 4.566674e+05 3.732759e+05 1.545468e+04 4.250010e+05
## [101] 3.566646e+04 1.385639e+05 1.527601e+05 5.013488e+04 2.500000e+05
## [106] 1.079991e+05 4.858810e+03 3.271674e+04 2.900013e+06 1.592759e+06
## [111] 5.300050e+05 2.866157e+05 1.389985e+04 4.532418e+05 6.299992e+04
## [116] 1.829995e+04 2.892011e+04 3.960044e+04 1.376000e+03 1.866340e+03
## [121] 2.229513e+07 1.591256e+07 4.206588e+07 4.499974e+04 1.099993e+08
## [126] 1.753759e+09 1.037410e+03 2.685840e+03 1.299990e+04 1.582010e+03
## [131] 2.720000e+02 1.720000e+02 5.400950e+03 9.769897e+05 1.000000e+04
## [136] 1.596980e+03 7.738910e+03 8.322040e+03 7.004200e+02 8.550000e+01
## [141] 1.516000e+02 6.744700e+02 4.117400e+02 3.667000e+01 4.192000e+02
## [146] 9.821300e+02 4.761678e+04 2.537000e+03 5.330000e+02 5.805500e+02
## [151] 5.995010e+03 2.132900e+03 4.549990e+03 3.127810e+03 5.788150e+03
## [156] 1.038510e+03 1.866680e+05 3.615014e+05 7.114000e+01 1.093000e+05
## [161] 4.369990e+03 4.317000e+02 7.374800e+03 1.769987e+04 3.008500e+03
## [166] 1.480440e+03 1.689779e+06 1.411985e+06 1.511785e+05 7.574950e+03
## [171] 1.305209e+04 1.327000e+02 6.300000e+02 3.500016e+04 9.499920e+03
## [176] 5.000000e+03 4.030000e+01 1.932810e+03 1.799990e+03 7.900053e+04
## [181] 2.919577e+04 5.696394e+04 1.653903e+05 2.749983e+04 1.308881e+05
## [186] 4.900040e+03 1.708205e+05 1.282655e+05 7.490831e+04 5.188400e+02
## [191] 5.355000e+02 1.684380e+05 3.010925e+04 1.504181e+04 1.559983e+04
## [196] 4.250500e+04 8.163190e+03 1.490219e+04 5.325005e+04 3.246011e+04
## [201] 4.753350e+03 1.239995e+05 1.176068e+04 8.594300e+03 7.066000e+04
## [206] 1.280000e+05 3.477778e+04 2.350000e+03 5.656000e+03 5.850000e+02
## [211] 5.750000e+01 1.350000e+02 1.464800e+04 8.727000e+03 3.418000e+04
## [216] 1.384160e+06 1.685000e+05 5.200000e+03 7.200000e+04 1.900000e+04
## [221] 9.640000e+04 3.197000e+05 2.050000e+06 1.710000e+04 3.790000e+04
## [226] 5.700000e+05 1.417000e+05
```


```r
mean(hra_h)
```

```
## [1] 34137012
```


**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  


```r
deer <-select(homerange, "mean.mass.g", "log10.mass","genus","family","species")
```

```r
filter(deer, family == "cervidae")
```

```
## # A tibble: 12 × 5
##    mean.mass.g log10.mass genus      family   species    
##          <dbl>      <dbl> <chr>      <chr>    <chr>      
##  1     307227.       5.49 alces      cervidae alces      
##  2      62823.       4.80 axis       cervidae axis       
##  3      24050.       4.38 capreolus  cervidae capreolus  
##  4     234758.       5.37 cervus     cervidae elaphus    
##  5      29450.       4.47 cervus     cervidae nippon     
##  6      71450.       4.85 dama       cervidae dama       
##  7      13500.       4.13 muntiacus  cervidae reevesi    
##  8      53864.       4.73 odocoileus cervidae hemionus   
##  9      87884.       4.94 odocoileus cervidae virginianus
## 10      35000.       4.54 ozotoceros cervidae bezoarticus
## 11       7500.       3.88 pudu       cervidae puda       
## 12     102059.       5.01 rangifer   cervidae tarandus
```

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**   

```r
snake <-filter(homerange, taxon=="snakes")
```


```r
min(snake$mean.hra.m2)
```

```
## [1] 200
```
schneideri species has the smallest homerange, searched in table I made for snakes

```r
summary(snake)
```

```
##            taxon    common.name           class                       order   
##  snakes       :41   Length:41          Length:41          squamata       :41  
##  birds        : 0   Class :character   Class :character   accipitriformes: 0  
##  lake fishes  : 0   Mode  :character   Mode  :character   afrosoricida   : 0  
##  lizards      : 0                                         anguilliformes : 0  
##  mammals      : 0                                         anseriformes   : 0  
##  marine fishes: 0                                         apterygiformes : 0  
##  (Other)      : 0                                         (Other)        : 0  
##     family             genus             species          primarymethod     
##  Length:41          Length:41          Length:41          Length:41         
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass    
##  Length:41          Min.   :   3.46   Min.   :0.5391  
##  Class :character   1st Qu.: 106.70   1st Qu.:2.0282  
##  Mode  :character   Median : 234.10   Median :2.3694  
##                     Mean   : 303.62   Mean   :2.2261  
##                     3rd Qu.: 375.00   3rd Qu.:2.5740  
##                     Max.   :1226.85   Max.   :3.0888  
##                                                       
##  alternative.mass.reference  mean.hra.m2        log10.hra    
##  Length:41                  Min.   :    200   Min.   :2.301  
##  Class :character           1st Qu.:  22900   1st Qu.:4.360  
##  Mode  :character           Median :  77400   Median :4.889  
##                             Mean   : 258416   Mean   :4.715  
##                             3rd Qu.: 240400   3rd Qu.:5.381  
##                             Max.   :2579600   Max.   :6.412  
##                                                              
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:41          Length:41          Length:41          Length:41         
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension    preymass       log10.preymass  
##  Length:41          Min.   :2   Min.   :   8.97   Min.   :0.9528  
##  Class :character   1st Qu.:2   1st Qu.:  27.39   1st Qu.:1.3783  
##  Mode  :character   Median :2   Median :  51.93   Median :1.7154  
##                     Mean   :2   Mean   : 272.72   Mean   :1.8180  
##                     3rd Qu.:2   3rd Qu.: 129.14   3rd Qu.:2.0978  
##                     Max.   :2   Max.   :2684.21   Max.   :3.4288  
##                                 NA's   :26        NA's   :26      
##       PPMR        prey.size.reference
##  Min.   : 0.380   Length:41          
##  1st Qu.: 3.155   Class :character   
##  Median : 5.740   Mode  :character   
##  Mean   : 8.283                      
##  3rd Qu.:12.460                      
##  Max.   :25.000                      
##  NA's   :26
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
