---
title: "Lab 6 Homework"
author: "Joel Ledford"
date: "2023-02-02"
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
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
summary(fisheries)
```

```
##    Country          Common name        ISSCAAP group#  ISSCAAP taxonomic group
##  Length:17692       Length:17692       Min.   :11.00   Length:17692           
##  Class :character   Class :character   1st Qu.:33.00   Class :character       
##  Mode  :character   Mode  :character   Median :36.00   Mode  :character       
##                                        Mean   :37.38                          
##                                        3rd Qu.:38.00                          
##                                        Max.   :77.00                          
##  ASFIS species#     ASFIS species name FAO major fishing area
##  Length:17692       Length:17692       Min.   :18.00         
##  Class :character   Class :character   1st Qu.:31.00         
##  Mode  :character   Mode  :character   Median :37.00         
##                                        Mean   :45.34         
##                                        3rd Qu.:57.00         
##                                        Max.   :88.00         
##    Measure              1950               1951               1952          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1953               1954               1955               1956          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1957               1958               1959               1960          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1961               1962               1963               1964          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1965               1966               1967               1968          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1969               1970               1971               1972          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1973               1974               1975               1976          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1977               1978               1979               1980          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1981               1982               1983               1984          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1985               1986               1987               1988          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1989               1990               1991               1992          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1993               1994               1995               1996          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1997               1998               1999               2000          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2001               2002               2003               2004          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2005               2006               2007               2008          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2009               2010               2011               2012          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
## 
```

```r
names(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

```r
dim(fisheries)
```

```
## [1] 17692    71
```

```r
is.na(fisheries)
```

```
##          Country Common name ISSCAAP group# ISSCAAP taxonomic group
##     [1,]   FALSE       FALSE          FALSE                   FALSE
##     [2,]   FALSE       FALSE          FALSE                   FALSE
##     [3,]   FALSE       FALSE          FALSE                   FALSE
##     [4,]   FALSE       FALSE          FALSE                   FALSE
##     [5,]   FALSE       FALSE          FALSE                   FALSE
##     [6,]   FALSE       FALSE          FALSE                   FALSE
##     [7,]   FALSE       FALSE          FALSE                   FALSE
##     [8,]   FALSE       FALSE          FALSE                   FALSE
##     [9,]   FALSE       FALSE          FALSE                   FALSE
##    [10,]   FALSE       FALSE          FALSE                   FALSE
##    [11,]   FALSE       FALSE          FALSE                   FALSE
##    [12,]   FALSE       FALSE          FALSE                   FALSE
##    [13,]   FALSE       FALSE          FALSE                   FALSE
##    [14,]   FALSE       FALSE          FALSE                   FALSE
##    [15,]   FALSE       FALSE          FALSE                   FALSE
##    [16,]   FALSE       FALSE          FALSE                   FALSE
##    [17,]   FALSE       FALSE          FALSE                   FALSE
##    [18,]   FALSE       FALSE          FALSE                   FALSE
##    [19,]   FALSE       FALSE          FALSE                   FALSE
##    [20,]   FALSE       FALSE          FALSE                   FALSE
##    [21,]   FALSE       FALSE          FALSE                   FALSE
##    [22,]   FALSE       FALSE          FALSE                   FALSE
##    [23,]   FALSE       FALSE          FALSE                   FALSE
##    [24,]   FALSE       FALSE          FALSE                   FALSE
##    [25,]   FALSE       FALSE          FALSE                   FALSE
##    [26,]   FALSE       FALSE          FALSE                   FALSE
##    [27,]   FALSE       FALSE          FALSE                   FALSE
##    [28,]   FALSE       FALSE          FALSE                   FALSE
##    [29,]   FALSE       FALSE          FALSE                   FALSE
##    [30,]   FALSE       FALSE          FALSE                   FALSE
##    [31,]   FALSE       FALSE          FALSE                   FALSE
##    [32,]   FALSE       FALSE          FALSE                   FALSE
##    [33,]   FALSE       FALSE          FALSE                   FALSE
##    [34,]   FALSE       FALSE          FALSE                   FALSE
##    [35,]   FALSE       FALSE          FALSE                   FALSE
##    [36,]   FALSE       FALSE          FALSE                   FALSE
##    [37,]   FALSE       FALSE          FALSE                   FALSE
##    [38,]   FALSE       FALSE          FALSE                   FALSE
##    [39,]   FALSE       FALSE          FALSE                   FALSE
##    [40,]   FALSE       FALSE          FALSE                   FALSE
##    [41,]   FALSE       FALSE          FALSE                   FALSE
##    [42,]   FALSE       FALSE          FALSE                   FALSE
##    [43,]   FALSE       FALSE          FALSE                   FALSE
##    [44,]   FALSE       FALSE          FALSE                   FALSE
##    [45,]   FALSE       FALSE          FALSE                   FALSE
##    [46,]   FALSE       FALSE          FALSE                   FALSE
##    [47,]   FALSE       FALSE          FALSE                   FALSE
##    [48,]   FALSE       FALSE          FALSE                   FALSE
##    [49,]   FALSE       FALSE          FALSE                   FALSE
##    [50,]   FALSE       FALSE          FALSE                   FALSE
##    [51,]   FALSE       FALSE          FALSE                   FALSE
##    [52,]   FALSE       FALSE          FALSE                   FALSE
##    [53,]   FALSE       FALSE          FALSE                   FALSE
##    [54,]   FALSE       FALSE          FALSE                   FALSE
##    [55,]   FALSE       FALSE          FALSE                   FALSE
##    [56,]   FALSE       FALSE          FALSE                   FALSE
##    [57,]   FALSE       FALSE          FALSE                   FALSE
##    [58,]   FALSE       FALSE          FALSE                   FALSE
##    [59,]   FALSE       FALSE          FALSE                   FALSE
##    [60,]   FALSE       FALSE          FALSE                   FALSE
##    [61,]   FALSE       FALSE          FALSE                   FALSE
##    [62,]   FALSE       FALSE          FALSE                   FALSE
##    [63,]   FALSE       FALSE          FALSE                   FALSE
##    [64,]   FALSE       FALSE          FALSE                   FALSE
##    [65,]   FALSE       FALSE          FALSE                   FALSE
##    [66,]   FALSE       FALSE          FALSE                   FALSE
##    [67,]   FALSE       FALSE          FALSE                   FALSE
##    [68,]   FALSE       FALSE          FALSE                   FALSE
##    [69,]   FALSE       FALSE          FALSE                   FALSE
##    [70,]   FALSE       FALSE          FALSE                   FALSE
##    [71,]   FALSE       FALSE          FALSE                   FALSE
##    [72,]   FALSE       FALSE          FALSE                   FALSE
##    [73,]   FALSE       FALSE          FALSE                   FALSE
##    [74,]   FALSE       FALSE          FALSE                   FALSE
##    [75,]   FALSE       FALSE          FALSE                   FALSE
##    [76,]   FALSE       FALSE          FALSE                   FALSE
##    [77,]   FALSE       FALSE          FALSE                   FALSE
##    [78,]   FALSE       FALSE          FALSE                   FALSE
##    [79,]   FALSE       FALSE          FALSE                   FALSE
##    [80,]   FALSE       FALSE          FALSE                   FALSE
##    [81,]   FALSE       FALSE          FALSE                   FALSE
##    [82,]   FALSE       FALSE          FALSE                   FALSE
##    [83,]   FALSE       FALSE          FALSE                   FALSE
##    [84,]   FALSE       FALSE          FALSE                   FALSE
##    [85,]   FALSE       FALSE          FALSE                   FALSE
##    [86,]   FALSE       FALSE          FALSE                   FALSE
##    [87,]   FALSE       FALSE          FALSE                   FALSE
##    [88,]   FALSE       FALSE          FALSE                   FALSE
##    [89,]   FALSE       FALSE          FALSE                   FALSE
##    [90,]   FALSE       FALSE          FALSE                   FALSE
##    [91,]   FALSE       FALSE          FALSE                   FALSE
##    [92,]   FALSE       FALSE          FALSE                   FALSE
##    [93,]   FALSE       FALSE          FALSE                   FALSE
##    [94,]   FALSE       FALSE          FALSE                   FALSE
##    [95,]   FALSE       FALSE          FALSE                   FALSE
##    [96,]   FALSE       FALSE          FALSE                   FALSE
##    [97,]   FALSE       FALSE          FALSE                   FALSE
##    [98,]   FALSE       FALSE          FALSE                   FALSE
##    [99,]   FALSE       FALSE          FALSE                   FALSE
##   [100,]   FALSE       FALSE          FALSE                   FALSE
##   [101,]   FALSE       FALSE          FALSE                   FALSE
##   [102,]   FALSE       FALSE          FALSE                   FALSE
##   [103,]   FALSE       FALSE          FALSE                   FALSE
##   [104,]   FALSE       FALSE          FALSE                   FALSE
##   [105,]   FALSE       FALSE          FALSE                   FALSE
##   [106,]   FALSE       FALSE          FALSE                   FALSE
##   [107,]   FALSE       FALSE          FALSE                   FALSE
##   [108,]   FALSE       FALSE          FALSE                   FALSE
##   [109,]   FALSE       FALSE          FALSE                   FALSE
##   [110,]   FALSE       FALSE          FALSE                   FALSE
##   [111,]   FALSE       FALSE          FALSE                   FALSE
##   [112,]   FALSE       FALSE          FALSE                   FALSE
##   [113,]   FALSE       FALSE          FALSE                   FALSE
##   [114,]   FALSE       FALSE          FALSE                   FALSE
##   [115,]   FALSE       FALSE          FALSE                   FALSE
##   [116,]   FALSE       FALSE          FALSE                   FALSE
##   [117,]   FALSE       FALSE          FALSE                   FALSE
##   [118,]   FALSE       FALSE          FALSE                   FALSE
##   [119,]   FALSE       FALSE          FALSE                   FALSE
##   [120,]   FALSE       FALSE          FALSE                   FALSE
##   [121,]   FALSE       FALSE          FALSE                   FALSE
##   [122,]   FALSE       FALSE          FALSE                   FALSE
##   [123,]   FALSE       FALSE          FALSE                   FALSE
##   [124,]   FALSE       FALSE          FALSE                   FALSE
##   [125,]   FALSE       FALSE          FALSE                   FALSE
##   [126,]   FALSE       FALSE          FALSE                   FALSE
##   [127,]   FALSE       FALSE          FALSE                   FALSE
##   [128,]   FALSE       FALSE          FALSE                   FALSE
##   [129,]   FALSE       FALSE          FALSE                   FALSE
##   [130,]   FALSE       FALSE          FALSE                   FALSE
##   [131,]   FALSE       FALSE          FALSE                   FALSE
##   [132,]   FALSE       FALSE          FALSE                   FALSE
##   [133,]   FALSE       FALSE          FALSE                   FALSE
##   [134,]   FALSE       FALSE          FALSE                   FALSE
##   [135,]   FALSE       FALSE          FALSE                   FALSE
##   [136,]   FALSE       FALSE          FALSE                   FALSE
##   [137,]   FALSE       FALSE          FALSE                   FALSE
##   [138,]   FALSE       FALSE          FALSE                   FALSE
##   [139,]   FALSE       FALSE          FALSE                   FALSE
##   [140,]   FALSE       FALSE          FALSE                   FALSE
##   [141,]   FALSE       FALSE          FALSE                   FALSE
##   [142,]   FALSE       FALSE          FALSE                   FALSE
##   [143,]   FALSE       FALSE          FALSE                   FALSE
##   [144,]   FALSE       FALSE          FALSE                   FALSE
##   [145,]   FALSE       FALSE          FALSE                   FALSE
##   [146,]   FALSE       FALSE          FALSE                   FALSE
##   [147,]   FALSE       FALSE          FALSE                   FALSE
##   [148,]   FALSE       FALSE          FALSE                   FALSE
##   [149,]   FALSE       FALSE          FALSE                   FALSE
##   [150,]   FALSE       FALSE          FALSE                   FALSE
##   [151,]   FALSE       FALSE          FALSE                   FALSE
##   [152,]   FALSE       FALSE          FALSE                   FALSE
##   [153,]   FALSE       FALSE          FALSE                   FALSE
##   [154,]   FALSE       FALSE          FALSE                   FALSE
##   [155,]   FALSE       FALSE          FALSE                   FALSE
##   [156,]   FALSE       FALSE          FALSE                   FALSE
##   [157,]   FALSE       FALSE          FALSE                   FALSE
##   [158,]   FALSE       FALSE          FALSE                   FALSE
##   [159,]   FALSE       FALSE          FALSE                   FALSE
##   [160,]   FALSE       FALSE          FALSE                   FALSE
##   [161,]   FALSE       FALSE          FALSE                   FALSE
##   [162,]   FALSE       FALSE          FALSE                   FALSE
##   [163,]   FALSE       FALSE          FALSE                   FALSE
##   [164,]   FALSE       FALSE          FALSE                   FALSE
##   [165,]   FALSE       FALSE          FALSE                   FALSE
##   [166,]   FALSE       FALSE          FALSE                   FALSE
##   [167,]   FALSE       FALSE          FALSE                   FALSE
##   [168,]   FALSE       FALSE          FALSE                   FALSE
##   [169,]   FALSE       FALSE          FALSE                   FALSE
##   [170,]   FALSE       FALSE          FALSE                   FALSE
##   [171,]   FALSE       FALSE          FALSE                   FALSE
##   [172,]   FALSE       FALSE          FALSE                   FALSE
##   [173,]   FALSE       FALSE          FALSE                   FALSE
##   [174,]   FALSE       FALSE          FALSE                   FALSE
##   [175,]   FALSE       FALSE          FALSE                   FALSE
##   [176,]   FALSE       FALSE          FALSE                   FALSE
##   [177,]   FALSE       FALSE          FALSE                   FALSE
##   [178,]   FALSE       FALSE          FALSE                   FALSE
##   [179,]   FALSE       FALSE          FALSE                   FALSE
##   [180,]   FALSE       FALSE          FALSE                   FALSE
##   [181,]   FALSE       FALSE          FALSE                   FALSE
##   [182,]   FALSE       FALSE          FALSE                   FALSE
##   [183,]   FALSE       FALSE          FALSE                   FALSE
##   [184,]   FALSE       FALSE          FALSE                   FALSE
##   [185,]   FALSE       FALSE          FALSE                   FALSE
##   [186,]   FALSE       FALSE          FALSE                   FALSE
##   [187,]   FALSE       FALSE          FALSE                   FALSE
##   [188,]   FALSE       FALSE          FALSE                   FALSE
##   [189,]   FALSE       FALSE          FALSE                   FALSE
##   [190,]   FALSE       FALSE          FALSE                   FALSE
##   [191,]   FALSE       FALSE          FALSE                   FALSE
##   [192,]   FALSE       FALSE          FALSE                   FALSE
##   [193,]   FALSE       FALSE          FALSE                   FALSE
##   [194,]   FALSE       FALSE          FALSE                   FALSE
##   [195,]   FALSE       FALSE          FALSE                   FALSE
##   [196,]   FALSE       FALSE          FALSE                   FALSE
##   [197,]   FALSE       FALSE          FALSE                   FALSE
##   [198,]   FALSE       FALSE          FALSE                   FALSE
##   [199,]   FALSE       FALSE          FALSE                   FALSE
##   [200,]   FALSE       FALSE          FALSE                   FALSE
##   [201,]   FALSE       FALSE          FALSE                   FALSE
##   [202,]   FALSE       FALSE          FALSE                   FALSE
##   [203,]   FALSE       FALSE          FALSE                   FALSE
##   [204,]   FALSE       FALSE          FALSE                   FALSE
##   [205,]   FALSE       FALSE          FALSE                   FALSE
##   [206,]   FALSE       FALSE          FALSE                   FALSE
##   [207,]   FALSE       FALSE          FALSE                   FALSE
##   [208,]   FALSE       FALSE          FALSE                   FALSE
##   [209,]   FALSE       FALSE          FALSE                   FALSE
##   [210,]   FALSE       FALSE          FALSE                   FALSE
##   [211,]   FALSE       FALSE          FALSE                   FALSE
##   [212,]   FALSE       FALSE          FALSE                   FALSE
##   [213,]   FALSE       FALSE          FALSE                   FALSE
##   [214,]   FALSE       FALSE          FALSE                   FALSE
##   [215,]   FALSE       FALSE          FALSE                   FALSE
##   [216,]   FALSE       FALSE          FALSE                   FALSE
##   [217,]   FALSE       FALSE          FALSE                   FALSE
##   [218,]   FALSE       FALSE          FALSE                   FALSE
##   [219,]   FALSE       FALSE          FALSE                   FALSE
##   [220,]   FALSE       FALSE          FALSE                   FALSE
##   [221,]   FALSE       FALSE          FALSE                   FALSE
##   [222,]   FALSE       FALSE          FALSE                   FALSE
##   [223,]   FALSE       FALSE          FALSE                   FALSE
##   [224,]   FALSE       FALSE          FALSE                   FALSE
##   [225,]   FALSE       FALSE          FALSE                   FALSE
##   [226,]   FALSE       FALSE          FALSE                   FALSE
##   [227,]   FALSE       FALSE          FALSE                   FALSE
##   [228,]   FALSE       FALSE          FALSE                   FALSE
##   [229,]   FALSE       FALSE          FALSE                   FALSE
##   [230,]   FALSE       FALSE          FALSE                   FALSE
##   [231,]   FALSE       FALSE          FALSE                   FALSE
##   [232,]   FALSE       FALSE          FALSE                   FALSE
##   [233,]   FALSE       FALSE          FALSE                   FALSE
##   [234,]   FALSE       FALSE          FALSE                   FALSE
##   [235,]   FALSE       FALSE          FALSE                   FALSE
##   [236,]   FALSE       FALSE          FALSE                   FALSE
##   [237,]   FALSE       FALSE          FALSE                   FALSE
##   [238,]   FALSE       FALSE          FALSE                   FALSE
##   [239,]   FALSE       FALSE          FALSE                   FALSE
##   [240,]   FALSE       FALSE          FALSE                   FALSE
##   [241,]   FALSE       FALSE          FALSE                   FALSE
##   [242,]   FALSE       FALSE          FALSE                   FALSE
##   [243,]   FALSE       FALSE          FALSE                   FALSE
##   [244,]   FALSE       FALSE          FALSE                   FALSE
##   [245,]   FALSE       FALSE          FALSE                   FALSE
##   [246,]   FALSE       FALSE          FALSE                   FALSE
##   [247,]   FALSE       FALSE          FALSE                   FALSE
##   [248,]   FALSE       FALSE          FALSE                   FALSE
##   [249,]   FALSE       FALSE          FALSE                   FALSE
##   [250,]   FALSE       FALSE          FALSE                   FALSE
##   [251,]   FALSE       FALSE          FALSE                   FALSE
##   [252,]   FALSE       FALSE          FALSE                   FALSE
##   [253,]   FALSE       FALSE          FALSE                   FALSE
##   [254,]   FALSE       FALSE          FALSE                   FALSE
##   [255,]   FALSE       FALSE          FALSE                   FALSE
##   [256,]   FALSE       FALSE          FALSE                   FALSE
##   [257,]   FALSE       FALSE          FALSE                   FALSE
##   [258,]   FALSE       FALSE          FALSE                   FALSE
##   [259,]   FALSE       FALSE          FALSE                   FALSE
##   [260,]   FALSE       FALSE          FALSE                   FALSE
##   [261,]   FALSE       FALSE          FALSE                   FALSE
##   [262,]   FALSE       FALSE          FALSE                   FALSE
##   [263,]   FALSE       FALSE          FALSE                   FALSE
##   [264,]   FALSE       FALSE          FALSE                   FALSE
##   [265,]   FALSE       FALSE          FALSE                   FALSE
##   [266,]   FALSE       FALSE          FALSE                   FALSE
##   [267,]   FALSE       FALSE          FALSE                   FALSE
##   [268,]   FALSE       FALSE          FALSE                   FALSE
##   [269,]   FALSE       FALSE          FALSE                   FALSE
##   [270,]   FALSE       FALSE          FALSE                   FALSE
##   [271,]   FALSE       FALSE          FALSE                   FALSE
##   [272,]   FALSE       FALSE          FALSE                   FALSE
##   [273,]   FALSE       FALSE          FALSE                   FALSE
##   [274,]   FALSE       FALSE          FALSE                   FALSE
##   [275,]   FALSE       FALSE          FALSE                   FALSE
##   [276,]   FALSE       FALSE          FALSE                   FALSE
##   [277,]   FALSE       FALSE          FALSE                   FALSE
##   [278,]   FALSE       FALSE          FALSE                   FALSE
##   [279,]   FALSE       FALSE          FALSE                   FALSE
##   [280,]   FALSE       FALSE          FALSE                   FALSE
##   [281,]   FALSE       FALSE          FALSE                   FALSE
##   [282,]   FALSE       FALSE          FALSE                   FALSE
##   [283,]   FALSE       FALSE          FALSE                   FALSE
##   [284,]   FALSE       FALSE          FALSE                   FALSE
##   [285,]   FALSE       FALSE          FALSE                   FALSE
##   [286,]   FALSE       FALSE          FALSE                   FALSE
##   [287,]   FALSE       FALSE          FALSE                   FALSE
##   [288,]   FALSE       FALSE          FALSE                   FALSE
##   [289,]   FALSE       FALSE          FALSE                   FALSE
##   [290,]   FALSE       FALSE          FALSE                   FALSE
##   [291,]   FALSE       FALSE          FALSE                   FALSE
##   [292,]   FALSE       FALSE          FALSE                   FALSE
##   [293,]   FALSE       FALSE          FALSE                   FALSE
##   [294,]   FALSE       FALSE          FALSE                   FALSE
##   [295,]   FALSE       FALSE          FALSE                   FALSE
##   [296,]   FALSE       FALSE          FALSE                   FALSE
##   [297,]   FALSE       FALSE          FALSE                   FALSE
##   [298,]   FALSE       FALSE          FALSE                   FALSE
##   [299,]   FALSE       FALSE          FALSE                   FALSE
##   [300,]   FALSE       FALSE          FALSE                   FALSE
##   [301,]   FALSE       FALSE          FALSE                   FALSE
##   [302,]   FALSE       FALSE          FALSE                   FALSE
##   [303,]   FALSE       FALSE          FALSE                   FALSE
##   [304,]   FALSE       FALSE          FALSE                   FALSE
##   [305,]   FALSE       FALSE          FALSE                   FALSE
##   [306,]   FALSE       FALSE          FALSE                   FALSE
##   [307,]   FALSE       FALSE          FALSE                   FALSE
##   [308,]   FALSE       FALSE          FALSE                   FALSE
##   [309,]   FALSE       FALSE          FALSE                   FALSE
##   [310,]   FALSE       FALSE          FALSE                   FALSE
##   [311,]   FALSE       FALSE          FALSE                   FALSE
##   [312,]   FALSE       FALSE          FALSE                   FALSE
##   [313,]   FALSE       FALSE          FALSE                   FALSE
##   [314,]   FALSE       FALSE          FALSE                   FALSE
##   [315,]   FALSE       FALSE          FALSE                   FALSE
##   [316,]   FALSE       FALSE          FALSE                   FALSE
##   [317,]   FALSE       FALSE          FALSE                   FALSE
##   [318,]   FALSE       FALSE          FALSE                   FALSE
##   [319,]   FALSE       FALSE          FALSE                   FALSE
##   [320,]   FALSE       FALSE          FALSE                   FALSE
##   [321,]   FALSE       FALSE          FALSE                   FALSE
##   [322,]   FALSE       FALSE          FALSE                   FALSE
##   [323,]   FALSE       FALSE          FALSE                   FALSE
##   [324,]   FALSE       FALSE          FALSE                   FALSE
##   [325,]   FALSE       FALSE          FALSE                   FALSE
##   [326,]   FALSE       FALSE          FALSE                   FALSE
##   [327,]   FALSE       FALSE          FALSE                   FALSE
##   [328,]   FALSE       FALSE          FALSE                   FALSE
##   [329,]   FALSE       FALSE          FALSE                   FALSE
##   [330,]   FALSE       FALSE          FALSE                   FALSE
##   [331,]   FALSE       FALSE          FALSE                   FALSE
##   [332,]   FALSE       FALSE          FALSE                   FALSE
##   [333,]   FALSE       FALSE          FALSE                   FALSE
##   [334,]   FALSE       FALSE          FALSE                   FALSE
##   [335,]   FALSE       FALSE          FALSE                   FALSE
##   [336,]   FALSE       FALSE          FALSE                   FALSE
##   [337,]   FALSE       FALSE          FALSE                   FALSE
##   [338,]   FALSE       FALSE          FALSE                   FALSE
##   [339,]   FALSE       FALSE          FALSE                   FALSE
##   [340,]   FALSE       FALSE          FALSE                   FALSE
##   [341,]   FALSE       FALSE          FALSE                   FALSE
##   [342,]   FALSE       FALSE          FALSE                   FALSE
##   [343,]   FALSE       FALSE          FALSE                   FALSE
##   [344,]   FALSE       FALSE          FALSE                   FALSE
##   [345,]   FALSE       FALSE          FALSE                   FALSE
##   [346,]   FALSE       FALSE          FALSE                   FALSE
##   [347,]   FALSE       FALSE          FALSE                   FALSE
##   [348,]   FALSE       FALSE          FALSE                   FALSE
##   [349,]   FALSE       FALSE          FALSE                   FALSE
##   [350,]   FALSE       FALSE          FALSE                   FALSE
##   [351,]   FALSE       FALSE          FALSE                   FALSE
##   [352,]   FALSE       FALSE          FALSE                   FALSE
##   [353,]   FALSE       FALSE          FALSE                   FALSE
##   [354,]   FALSE       FALSE          FALSE                   FALSE
##   [355,]   FALSE       FALSE          FALSE                   FALSE
##   [356,]   FALSE       FALSE          FALSE                   FALSE
##   [357,]   FALSE       FALSE          FALSE                   FALSE
##   [358,]   FALSE       FALSE          FALSE                   FALSE
##   [359,]   FALSE       FALSE          FALSE                   FALSE
##   [360,]   FALSE       FALSE          FALSE                   FALSE
##   [361,]   FALSE       FALSE          FALSE                   FALSE
##   [362,]   FALSE       FALSE          FALSE                   FALSE
##   [363,]   FALSE       FALSE          FALSE                   FALSE
##   [364,]   FALSE       FALSE          FALSE                   FALSE
##   [365,]   FALSE       FALSE          FALSE                   FALSE
##   [366,]   FALSE       FALSE          FALSE                   FALSE
##   [367,]   FALSE       FALSE          FALSE                   FALSE
##   [368,]   FALSE       FALSE          FALSE                   FALSE
##   [369,]   FALSE       FALSE          FALSE                   FALSE
##   [370,]   FALSE       FALSE          FALSE                   FALSE
##   [371,]   FALSE       FALSE          FALSE                   FALSE
##   [372,]   FALSE       FALSE          FALSE                   FALSE
##   [373,]   FALSE       FALSE          FALSE                   FALSE
##   [374,]   FALSE       FALSE          FALSE                   FALSE
##   [375,]   FALSE       FALSE          FALSE                   FALSE
##   [376,]   FALSE       FALSE          FALSE                   FALSE
##   [377,]   FALSE       FALSE          FALSE                   FALSE
##   [378,]   FALSE       FALSE          FALSE                   FALSE
##   [379,]   FALSE       FALSE          FALSE                   FALSE
##   [380,]   FALSE       FALSE          FALSE                   FALSE
##   [381,]   FALSE       FALSE          FALSE                   FALSE
##   [382,]   FALSE       FALSE          FALSE                   FALSE
##   [383,]   FALSE       FALSE          FALSE                   FALSE
##   [384,]   FALSE       FALSE          FALSE                   FALSE
##   [385,]   FALSE       FALSE          FALSE                   FALSE
##   [386,]   FALSE       FALSE          FALSE                   FALSE
##   [387,]   FALSE       FALSE          FALSE                   FALSE
##   [388,]   FALSE       FALSE          FALSE                   FALSE
##   [389,]   FALSE       FALSE          FALSE                   FALSE
##   [390,]   FALSE       FALSE          FALSE                   FALSE
##   [391,]   FALSE       FALSE          FALSE                   FALSE
##   [392,]   FALSE       FALSE          FALSE                   FALSE
##   [393,]   FALSE       FALSE          FALSE                   FALSE
##   [394,]   FALSE       FALSE          FALSE                   FALSE
##   [395,]   FALSE       FALSE          FALSE                   FALSE
##   [396,]   FALSE       FALSE          FALSE                   FALSE
##   [397,]   FALSE       FALSE          FALSE                   FALSE
##   [398,]   FALSE       FALSE          FALSE                   FALSE
##   [399,]   FALSE       FALSE          FALSE                   FALSE
##   [400,]   FALSE       FALSE          FALSE                   FALSE
##   [401,]   FALSE       FALSE          FALSE                   FALSE
##   [402,]   FALSE       FALSE          FALSE                   FALSE
##   [403,]   FALSE       FALSE          FALSE                   FALSE
##   [404,]   FALSE       FALSE          FALSE                   FALSE
##   [405,]   FALSE       FALSE          FALSE                   FALSE
##   [406,]   FALSE       FALSE          FALSE                   FALSE
##   [407,]   FALSE       FALSE          FALSE                   FALSE
##   [408,]   FALSE       FALSE          FALSE                   FALSE
##   [409,]   FALSE       FALSE          FALSE                   FALSE
##   [410,]   FALSE       FALSE          FALSE                   FALSE
##   [411,]   FALSE       FALSE          FALSE                   FALSE
##   [412,]   FALSE       FALSE          FALSE                   FALSE
##   [413,]   FALSE       FALSE          FALSE                   FALSE
##   [414,]   FALSE       FALSE          FALSE                   FALSE
##   [415,]   FALSE       FALSE          FALSE                   FALSE
##   [416,]   FALSE       FALSE          FALSE                   FALSE
##   [417,]   FALSE       FALSE          FALSE                   FALSE
##   [418,]   FALSE       FALSE          FALSE                   FALSE
##   [419,]   FALSE       FALSE          FALSE                   FALSE
##   [420,]   FALSE       FALSE          FALSE                   FALSE
##   [421,]   FALSE       FALSE          FALSE                   FALSE
##   [422,]   FALSE       FALSE          FALSE                   FALSE
##   [423,]   FALSE       FALSE          FALSE                   FALSE
##   [424,]   FALSE       FALSE          FALSE                   FALSE
##   [425,]   FALSE       FALSE          FALSE                   FALSE
##   [426,]   FALSE       FALSE          FALSE                   FALSE
##   [427,]   FALSE       FALSE          FALSE                   FALSE
##   [428,]   FALSE       FALSE          FALSE                   FALSE
##   [429,]   FALSE       FALSE          FALSE                   FALSE
##   [430,]   FALSE       FALSE          FALSE                   FALSE
##   [431,]   FALSE       FALSE          FALSE                   FALSE
##   [432,]   FALSE       FALSE          FALSE                   FALSE
##   [433,]   FALSE       FALSE          FALSE                   FALSE
##   [434,]   FALSE       FALSE          FALSE                   FALSE
##   [435,]   FALSE       FALSE          FALSE                   FALSE
##   [436,]   FALSE       FALSE          FALSE                   FALSE
##   [437,]   FALSE       FALSE          FALSE                   FALSE
##   [438,]   FALSE       FALSE          FALSE                   FALSE
##   [439,]   FALSE       FALSE          FALSE                   FALSE
##   [440,]   FALSE       FALSE          FALSE                   FALSE
##   [441,]   FALSE       FALSE          FALSE                   FALSE
##   [442,]   FALSE       FALSE          FALSE                   FALSE
##   [443,]   FALSE       FALSE          FALSE                   FALSE
##   [444,]   FALSE       FALSE          FALSE                   FALSE
##   [445,]   FALSE       FALSE          FALSE                   FALSE
##   [446,]   FALSE       FALSE          FALSE                   FALSE
##   [447,]   FALSE       FALSE          FALSE                   FALSE
##   [448,]   FALSE       FALSE          FALSE                   FALSE
##   [449,]   FALSE       FALSE          FALSE                   FALSE
##   [450,]   FALSE       FALSE          FALSE                   FALSE
##   [451,]   FALSE       FALSE          FALSE                   FALSE
##   [452,]   FALSE       FALSE          FALSE                   FALSE
##   [453,]   FALSE       FALSE          FALSE                   FALSE
##   [454,]   FALSE       FALSE          FALSE                   FALSE
##   [455,]   FALSE       FALSE          FALSE                   FALSE
##   [456,]   FALSE       FALSE          FALSE                   FALSE
##   [457,]   FALSE       FALSE          FALSE                   FALSE
##   [458,]   FALSE       FALSE          FALSE                   FALSE
##   [459,]   FALSE       FALSE          FALSE                   FALSE
##   [460,]   FALSE       FALSE          FALSE                   FALSE
##   [461,]   FALSE       FALSE          FALSE                   FALSE
##   [462,]   FALSE       FALSE          FALSE                   FALSE
##   [463,]   FALSE       FALSE          FALSE                   FALSE
##   [464,]   FALSE       FALSE          FALSE                   FALSE
##   [465,]   FALSE       FALSE          FALSE                   FALSE
##   [466,]   FALSE       FALSE          FALSE                   FALSE
##   [467,]   FALSE       FALSE          FALSE                   FALSE
##   [468,]   FALSE       FALSE          FALSE                   FALSE
##   [469,]   FALSE       FALSE          FALSE                   FALSE
##   [470,]   FALSE       FALSE          FALSE                   FALSE
##   [471,]   FALSE       FALSE          FALSE                   FALSE
##   [472,]   FALSE       FALSE          FALSE                   FALSE
##   [473,]   FALSE       FALSE          FALSE                   FALSE
##   [474,]   FALSE       FALSE          FALSE                   FALSE
##   [475,]   FALSE       FALSE          FALSE                   FALSE
##   [476,]   FALSE       FALSE          FALSE                   FALSE
##   [477,]   FALSE       FALSE          FALSE                   FALSE
##   [478,]   FALSE       FALSE          FALSE                   FALSE
##   [479,]   FALSE       FALSE          FALSE                   FALSE
##   [480,]   FALSE       FALSE          FALSE                   FALSE
##   [481,]   FALSE       FALSE          FALSE                   FALSE
##   [482,]   FALSE       FALSE          FALSE                   FALSE
##   [483,]   FALSE       FALSE          FALSE                   FALSE
##   [484,]   FALSE       FALSE          FALSE                   FALSE
##   [485,]   FALSE       FALSE          FALSE                   FALSE
##   [486,]   FALSE       FALSE          FALSE                   FALSE
##   [487,]   FALSE       FALSE          FALSE                   FALSE
##   [488,]   FALSE       FALSE          FALSE                   FALSE
##   [489,]   FALSE       FALSE          FALSE                   FALSE
##   [490,]   FALSE       FALSE          FALSE                   FALSE
##   [491,]   FALSE       FALSE          FALSE                   FALSE
##   [492,]   FALSE       FALSE          FALSE                   FALSE
##   [493,]   FALSE       FALSE          FALSE                   FALSE
##   [494,]   FALSE       FALSE          FALSE                   FALSE
##   [495,]   FALSE       FALSE          FALSE                   FALSE
##   [496,]   FALSE       FALSE          FALSE                   FALSE
##   [497,]   FALSE       FALSE          FALSE                   FALSE
##   [498,]   FALSE       FALSE          FALSE                   FALSE
##   [499,]   FALSE       FALSE          FALSE                   FALSE
##   [500,]   FALSE       FALSE          FALSE                   FALSE
##   [501,]   FALSE       FALSE          FALSE                   FALSE
##   [502,]   FALSE       FALSE          FALSE                   FALSE
##   [503,]   FALSE       FALSE          FALSE                   FALSE
##   [504,]   FALSE       FALSE          FALSE                   FALSE
##   [505,]   FALSE       FALSE          FALSE                   FALSE
##   [506,]   FALSE       FALSE          FALSE                   FALSE
##   [507,]   FALSE       FALSE          FALSE                   FALSE
##   [508,]   FALSE       FALSE          FALSE                   FALSE
##   [509,]   FALSE       FALSE          FALSE                   FALSE
##   [510,]   FALSE       FALSE          FALSE                   FALSE
##   [511,]   FALSE       FALSE          FALSE                   FALSE
##   [512,]   FALSE       FALSE          FALSE                   FALSE
##   [513,]   FALSE       FALSE          FALSE                   FALSE
##   [514,]   FALSE       FALSE          FALSE                   FALSE
##   [515,]   FALSE       FALSE          FALSE                   FALSE
##   [516,]   FALSE       FALSE          FALSE                   FALSE
##   [517,]   FALSE       FALSE          FALSE                   FALSE
##   [518,]   FALSE       FALSE          FALSE                   FALSE
##   [519,]   FALSE       FALSE          FALSE                   FALSE
##   [520,]   FALSE       FALSE          FALSE                   FALSE
##   [521,]   FALSE       FALSE          FALSE                   FALSE
##   [522,]   FALSE       FALSE          FALSE                   FALSE
##   [523,]   FALSE       FALSE          FALSE                   FALSE
##   [524,]   FALSE       FALSE          FALSE                   FALSE
##   [525,]   FALSE       FALSE          FALSE                   FALSE
##   [526,]   FALSE       FALSE          FALSE                   FALSE
##   [527,]   FALSE       FALSE          FALSE                   FALSE
##   [528,]   FALSE       FALSE          FALSE                   FALSE
##   [529,]   FALSE       FALSE          FALSE                   FALSE
##   [530,]   FALSE       FALSE          FALSE                   FALSE
##   [531,]   FALSE       FALSE          FALSE                   FALSE
##   [532,]   FALSE       FALSE          FALSE                   FALSE
##   [533,]   FALSE       FALSE          FALSE                   FALSE
##   [534,]   FALSE       FALSE          FALSE                   FALSE
##   [535,]   FALSE       FALSE          FALSE                   FALSE
##   [536,]   FALSE       FALSE          FALSE                   FALSE
##   [537,]   FALSE       FALSE          FALSE                   FALSE
##   [538,]   FALSE       FALSE          FALSE                   FALSE
##   [539,]   FALSE       FALSE          FALSE                   FALSE
##   [540,]   FALSE       FALSE          FALSE                   FALSE
##   [541,]   FALSE       FALSE          FALSE                   FALSE
##   [542,]   FALSE       FALSE          FALSE                   FALSE
##   [543,]   FALSE       FALSE          FALSE                   FALSE
##   [544,]   FALSE       FALSE          FALSE                   FALSE
##   [545,]   FALSE       FALSE          FALSE                   FALSE
##   [546,]   FALSE       FALSE          FALSE                   FALSE
##   [547,]   FALSE       FALSE          FALSE                   FALSE
##   [548,]   FALSE       FALSE          FALSE                   FALSE
##   [549,]   FALSE       FALSE          FALSE                   FALSE
##   [550,]   FALSE       FALSE          FALSE                   FALSE
##   [551,]   FALSE       FALSE          FALSE                   FALSE
##   [552,]   FALSE       FALSE          FALSE                   FALSE
##   [553,]   FALSE       FALSE          FALSE                   FALSE
##   [554,]   FALSE       FALSE          FALSE                   FALSE
##   [555,]   FALSE       FALSE          FALSE                   FALSE
##   [556,]   FALSE       FALSE          FALSE                   FALSE
##   [557,]   FALSE       FALSE          FALSE                   FALSE
##   [558,]   FALSE       FALSE          FALSE                   FALSE
##   [559,]   FALSE       FALSE          FALSE                   FALSE
##   [560,]   FALSE       FALSE          FALSE                   FALSE
##   [561,]   FALSE       FALSE          FALSE                   FALSE
##   [562,]   FALSE       FALSE          FALSE                   FALSE
##   [563,]   FALSE       FALSE          FALSE                   FALSE
##   [564,]   FALSE       FALSE          FALSE                   FALSE
##   [565,]   FALSE       FALSE          FALSE                   FALSE
##   [566,]   FALSE       FALSE          FALSE                   FALSE
##   [567,]   FALSE       FALSE          FALSE                   FALSE
##   [568,]   FALSE       FALSE          FALSE                   FALSE
##   [569,]   FALSE       FALSE          FALSE                   FALSE
##   [570,]   FALSE       FALSE          FALSE                   FALSE
##   [571,]   FALSE       FALSE          FALSE                   FALSE
##   [572,]   FALSE       FALSE          FALSE                   FALSE
##   [573,]   FALSE       FALSE          FALSE                   FALSE
##   [574,]   FALSE       FALSE          FALSE                   FALSE
##   [575,]   FALSE       FALSE          FALSE                   FALSE
##   [576,]   FALSE       FALSE          FALSE                   FALSE
##   [577,]   FALSE       FALSE          FALSE                   FALSE
##   [578,]   FALSE       FALSE          FALSE                   FALSE
##   [579,]   FALSE       FALSE          FALSE                   FALSE
##   [580,]   FALSE       FALSE          FALSE                   FALSE
##   [581,]   FALSE       FALSE          FALSE                   FALSE
##   [582,]   FALSE       FALSE          FALSE                   FALSE
##   [583,]   FALSE       FALSE          FALSE                   FALSE
##   [584,]   FALSE       FALSE          FALSE                   FALSE
##   [585,]   FALSE       FALSE          FALSE                   FALSE
##   [586,]   FALSE       FALSE          FALSE                   FALSE
##   [587,]   FALSE       FALSE          FALSE                   FALSE
##   [588,]   FALSE       FALSE          FALSE                   FALSE
##   [589,]   FALSE       FALSE          FALSE                   FALSE
##   [590,]   FALSE       FALSE          FALSE                   FALSE
##   [591,]   FALSE       FALSE          FALSE                   FALSE
##   [592,]   FALSE       FALSE          FALSE                   FALSE
##   [593,]   FALSE       FALSE          FALSE                   FALSE
##   [594,]   FALSE       FALSE          FALSE                   FALSE
##   [595,]   FALSE       FALSE          FALSE                   FALSE
##   [596,]   FALSE       FALSE          FALSE                   FALSE
##   [597,]   FALSE       FALSE          FALSE                   FALSE
##   [598,]   FALSE       FALSE          FALSE                   FALSE
##   [599,]   FALSE       FALSE          FALSE                   FALSE
##   [600,]   FALSE       FALSE          FALSE                   FALSE
##   [601,]   FALSE       FALSE          FALSE                   FALSE
##   [602,]   FALSE       FALSE          FALSE                   FALSE
##   [603,]   FALSE       FALSE          FALSE                   FALSE
##   [604,]   FALSE       FALSE          FALSE                   FALSE
##   [605,]   FALSE       FALSE          FALSE                   FALSE
##   [606,]   FALSE       FALSE          FALSE                   FALSE
##   [607,]   FALSE       FALSE          FALSE                   FALSE
##   [608,]   FALSE       FALSE          FALSE                   FALSE
##   [609,]   FALSE       FALSE          FALSE                   FALSE
##   [610,]   FALSE       FALSE          FALSE                   FALSE
##   [611,]   FALSE       FALSE          FALSE                   FALSE
##   [612,]   FALSE       FALSE          FALSE                   FALSE
##   [613,]   FALSE       FALSE          FALSE                   FALSE
##   [614,]   FALSE       FALSE          FALSE                   FALSE
##   [615,]   FALSE       FALSE          FALSE                   FALSE
##   [616,]   FALSE       FALSE          FALSE                   FALSE
##   [617,]   FALSE       FALSE          FALSE                   FALSE
##   [618,]   FALSE       FALSE          FALSE                   FALSE
##   [619,]   FALSE       FALSE          FALSE                   FALSE
##   [620,]   FALSE       FALSE          FALSE                   FALSE
##   [621,]   FALSE       FALSE          FALSE                   FALSE
##   [622,]   FALSE       FALSE          FALSE                   FALSE
##   [623,]   FALSE       FALSE          FALSE                   FALSE
##   [624,]   FALSE       FALSE          FALSE                   FALSE
##   [625,]   FALSE       FALSE          FALSE                   FALSE
##   [626,]   FALSE       FALSE          FALSE                   FALSE
##   [627,]   FALSE       FALSE          FALSE                   FALSE
##   [628,]   FALSE       FALSE          FALSE                   FALSE
##   [629,]   FALSE       FALSE          FALSE                   FALSE
##   [630,]   FALSE       FALSE          FALSE                   FALSE
##   [631,]   FALSE       FALSE          FALSE                   FALSE
##   [632,]   FALSE       FALSE          FALSE                   FALSE
##   [633,]   FALSE       FALSE          FALSE                   FALSE
##   [634,]   FALSE       FALSE          FALSE                   FALSE
##   [635,]   FALSE       FALSE          FALSE                   FALSE
##   [636,]   FALSE       FALSE          FALSE                   FALSE
##   [637,]   FALSE       FALSE          FALSE                   FALSE
##   [638,]   FALSE       FALSE          FALSE                   FALSE
##   [639,]   FALSE       FALSE          FALSE                   FALSE
##   [640,]   FALSE       FALSE          FALSE                   FALSE
##   [641,]   FALSE       FALSE          FALSE                   FALSE
##   [642,]   FALSE       FALSE          FALSE                   FALSE
##   [643,]   FALSE       FALSE          FALSE                   FALSE
##   [644,]   FALSE       FALSE          FALSE                   FALSE
##   [645,]   FALSE       FALSE          FALSE                   FALSE
##   [646,]   FALSE       FALSE          FALSE                   FALSE
##   [647,]   FALSE       FALSE          FALSE                   FALSE
##   [648,]   FALSE       FALSE          FALSE                   FALSE
##   [649,]   FALSE       FALSE          FALSE                   FALSE
##   [650,]   FALSE       FALSE          FALSE                   FALSE
##   [651,]   FALSE       FALSE          FALSE                   FALSE
##   [652,]   FALSE       FALSE          FALSE                   FALSE
##   [653,]   FALSE       FALSE          FALSE                   FALSE
##   [654,]   FALSE       FALSE          FALSE                   FALSE
##   [655,]   FALSE       FALSE          FALSE                   FALSE
##   [656,]   FALSE       FALSE          FALSE                   FALSE
##   [657,]   FALSE       FALSE          FALSE                   FALSE
##   [658,]   FALSE       FALSE          FALSE                   FALSE
##   [659,]   FALSE       FALSE          FALSE                   FALSE
##   [660,]   FALSE       FALSE          FALSE                   FALSE
##   [661,]   FALSE       FALSE          FALSE                   FALSE
##   [662,]   FALSE       FALSE          FALSE                   FALSE
##   [663,]   FALSE       FALSE          FALSE                   FALSE
##   [664,]   FALSE       FALSE          FALSE                   FALSE
##   [665,]   FALSE       FALSE          FALSE                   FALSE
##   [666,]   FALSE       FALSE          FALSE                   FALSE
##   [667,]   FALSE       FALSE          FALSE                   FALSE
##   [668,]   FALSE       FALSE          FALSE                   FALSE
##   [669,]   FALSE       FALSE          FALSE                   FALSE
##   [670,]   FALSE       FALSE          FALSE                   FALSE
##   [671,]   FALSE       FALSE          FALSE                   FALSE
##   [672,]   FALSE       FALSE          FALSE                   FALSE
##   [673,]   FALSE       FALSE          FALSE                   FALSE
##   [674,]   FALSE       FALSE          FALSE                   FALSE
##   [675,]   FALSE       FALSE          FALSE                   FALSE
##   [676,]   FALSE       FALSE          FALSE                   FALSE
##   [677,]   FALSE       FALSE          FALSE                   FALSE
##   [678,]   FALSE       FALSE          FALSE                   FALSE
##   [679,]   FALSE       FALSE          FALSE                   FALSE
##   [680,]   FALSE       FALSE          FALSE                   FALSE
##   [681,]   FALSE       FALSE          FALSE                   FALSE
##   [682,]   FALSE       FALSE          FALSE                   FALSE
##   [683,]   FALSE       FALSE          FALSE                   FALSE
##   [684,]   FALSE       FALSE          FALSE                   FALSE
##   [685,]   FALSE       FALSE          FALSE                   FALSE
##   [686,]   FALSE       FALSE          FALSE                   FALSE
##   [687,]   FALSE       FALSE          FALSE                   FALSE
##   [688,]   FALSE       FALSE          FALSE                   FALSE
##   [689,]   FALSE       FALSE          FALSE                   FALSE
##   [690,]   FALSE       FALSE          FALSE                   FALSE
##   [691,]   FALSE       FALSE          FALSE                   FALSE
##   [692,]   FALSE       FALSE          FALSE                   FALSE
##   [693,]   FALSE       FALSE          FALSE                   FALSE
##   [694,]   FALSE       FALSE          FALSE                   FALSE
##   [695,]   FALSE       FALSE          FALSE                   FALSE
##   [696,]   FALSE       FALSE          FALSE                   FALSE
##   [697,]   FALSE       FALSE          FALSE                   FALSE
##   [698,]   FALSE       FALSE          FALSE                   FALSE
##   [699,]   FALSE       FALSE          FALSE                   FALSE
##   [700,]   FALSE       FALSE          FALSE                   FALSE
##   [701,]   FALSE       FALSE          FALSE                   FALSE
##   [702,]   FALSE       FALSE          FALSE                   FALSE
##   [703,]   FALSE       FALSE          FALSE                   FALSE
##   [704,]   FALSE       FALSE          FALSE                   FALSE
##   [705,]   FALSE       FALSE          FALSE                   FALSE
##   [706,]   FALSE       FALSE          FALSE                   FALSE
##   [707,]   FALSE       FALSE          FALSE                   FALSE
##   [708,]   FALSE       FALSE          FALSE                   FALSE
##   [709,]   FALSE       FALSE          FALSE                   FALSE
##   [710,]   FALSE       FALSE          FALSE                   FALSE
##   [711,]   FALSE       FALSE          FALSE                   FALSE
##   [712,]   FALSE       FALSE          FALSE                   FALSE
##   [713,]   FALSE       FALSE          FALSE                   FALSE
##   [714,]   FALSE       FALSE          FALSE                   FALSE
##   [715,]   FALSE       FALSE          FALSE                   FALSE
##   [716,]   FALSE       FALSE          FALSE                   FALSE
##   [717,]   FALSE       FALSE          FALSE                   FALSE
##   [718,]   FALSE       FALSE          FALSE                   FALSE
##   [719,]   FALSE       FALSE          FALSE                   FALSE
##   [720,]   FALSE       FALSE          FALSE                   FALSE
##   [721,]   FALSE       FALSE          FALSE                   FALSE
##   [722,]   FALSE       FALSE          FALSE                   FALSE
##   [723,]   FALSE       FALSE          FALSE                   FALSE
##   [724,]   FALSE       FALSE          FALSE                   FALSE
##   [725,]   FALSE       FALSE          FALSE                   FALSE
##   [726,]   FALSE       FALSE          FALSE                   FALSE
##   [727,]   FALSE       FALSE          FALSE                   FALSE
##   [728,]   FALSE       FALSE          FALSE                   FALSE
##   [729,]   FALSE       FALSE          FALSE                   FALSE
##   [730,]   FALSE       FALSE          FALSE                   FALSE
##   [731,]   FALSE       FALSE          FALSE                   FALSE
##   [732,]   FALSE       FALSE          FALSE                   FALSE
##   [733,]   FALSE       FALSE          FALSE                   FALSE
##   [734,]   FALSE       FALSE          FALSE                   FALSE
##   [735,]   FALSE       FALSE          FALSE                   FALSE
##   [736,]   FALSE       FALSE          FALSE                   FALSE
##   [737,]   FALSE       FALSE          FALSE                   FALSE
##   [738,]   FALSE       FALSE          FALSE                   FALSE
##   [739,]   FALSE       FALSE          FALSE                   FALSE
##   [740,]   FALSE       FALSE          FALSE                   FALSE
##   [741,]   FALSE       FALSE          FALSE                   FALSE
##   [742,]   FALSE       FALSE          FALSE                   FALSE
##   [743,]   FALSE       FALSE          FALSE                   FALSE
##   [744,]   FALSE       FALSE          FALSE                   FALSE
##   [745,]   FALSE       FALSE          FALSE                   FALSE
##   [746,]   FALSE       FALSE          FALSE                   FALSE
##   [747,]   FALSE       FALSE          FALSE                   FALSE
##   [748,]   FALSE       FALSE          FALSE                   FALSE
##   [749,]   FALSE       FALSE          FALSE                   FALSE
##   [750,]   FALSE       FALSE          FALSE                   FALSE
##   [751,]   FALSE       FALSE          FALSE                   FALSE
##   [752,]   FALSE       FALSE          FALSE                   FALSE
##   [753,]   FALSE       FALSE          FALSE                   FALSE
##   [754,]   FALSE       FALSE          FALSE                   FALSE
##   [755,]   FALSE       FALSE          FALSE                   FALSE
##   [756,]   FALSE       FALSE          FALSE                   FALSE
##   [757,]   FALSE       FALSE          FALSE                   FALSE
##   [758,]   FALSE       FALSE          FALSE                   FALSE
##   [759,]   FALSE       FALSE          FALSE                   FALSE
##   [760,]   FALSE       FALSE          FALSE                   FALSE
##   [761,]   FALSE       FALSE          FALSE                   FALSE
##   [762,]   FALSE       FALSE          FALSE                   FALSE
##   [763,]   FALSE       FALSE          FALSE                   FALSE
##   [764,]   FALSE       FALSE          FALSE                   FALSE
##   [765,]   FALSE       FALSE          FALSE                   FALSE
##   [766,]   FALSE       FALSE          FALSE                   FALSE
##   [767,]   FALSE       FALSE          FALSE                   FALSE
##   [768,]   FALSE       FALSE          FALSE                   FALSE
##   [769,]   FALSE       FALSE          FALSE                   FALSE
##   [770,]   FALSE       FALSE          FALSE                   FALSE
##   [771,]   FALSE       FALSE          FALSE                   FALSE
##   [772,]   FALSE       FALSE          FALSE                   FALSE
##   [773,]   FALSE       FALSE          FALSE                   FALSE
##   [774,]   FALSE       FALSE          FALSE                   FALSE
##   [775,]   FALSE       FALSE          FALSE                   FALSE
##   [776,]   FALSE       FALSE          FALSE                   FALSE
##   [777,]   FALSE       FALSE          FALSE                   FALSE
##   [778,]   FALSE       FALSE          FALSE                   FALSE
##   [779,]   FALSE       FALSE          FALSE                   FALSE
##   [780,]   FALSE       FALSE          FALSE                   FALSE
##   [781,]   FALSE       FALSE          FALSE                   FALSE
##   [782,]   FALSE       FALSE          FALSE                   FALSE
##   [783,]   FALSE       FALSE          FALSE                   FALSE
##   [784,]   FALSE       FALSE          FALSE                   FALSE
##   [785,]   FALSE       FALSE          FALSE                   FALSE
##   [786,]   FALSE       FALSE          FALSE                   FALSE
##   [787,]   FALSE       FALSE          FALSE                   FALSE
##   [788,]   FALSE       FALSE          FALSE                   FALSE
##   [789,]   FALSE       FALSE          FALSE                   FALSE
##   [790,]   FALSE       FALSE          FALSE                   FALSE
##   [791,]   FALSE       FALSE          FALSE                   FALSE
##   [792,]   FALSE       FALSE          FALSE                   FALSE
##   [793,]   FALSE       FALSE          FALSE                   FALSE
##   [794,]   FALSE       FALSE          FALSE                   FALSE
##   [795,]   FALSE       FALSE          FALSE                   FALSE
##   [796,]   FALSE       FALSE          FALSE                   FALSE
##   [797,]   FALSE       FALSE          FALSE                   FALSE
##   [798,]   FALSE       FALSE          FALSE                   FALSE
##   [799,]   FALSE       FALSE          FALSE                   FALSE
##   [800,]   FALSE       FALSE          FALSE                   FALSE
##   [801,]   FALSE       FALSE          FALSE                   FALSE
##   [802,]   FALSE       FALSE          FALSE                   FALSE
##   [803,]   FALSE       FALSE          FALSE                   FALSE
##   [804,]   FALSE       FALSE          FALSE                   FALSE
##   [805,]   FALSE       FALSE          FALSE                   FALSE
##   [806,]   FALSE       FALSE          FALSE                   FALSE
##   [807,]   FALSE       FALSE          FALSE                   FALSE
##   [808,]   FALSE       FALSE          FALSE                   FALSE
##   [809,]   FALSE       FALSE          FALSE                   FALSE
##   [810,]   FALSE       FALSE          FALSE                   FALSE
##   [811,]   FALSE       FALSE          FALSE                   FALSE
##   [812,]   FALSE       FALSE          FALSE                   FALSE
##   [813,]   FALSE       FALSE          FALSE                   FALSE
##   [814,]   FALSE       FALSE          FALSE                   FALSE
##   [815,]   FALSE       FALSE          FALSE                   FALSE
##   [816,]   FALSE       FALSE          FALSE                   FALSE
##   [817,]   FALSE       FALSE          FALSE                   FALSE
##   [818,]   FALSE       FALSE          FALSE                   FALSE
##   [819,]   FALSE       FALSE          FALSE                   FALSE
##   [820,]   FALSE       FALSE          FALSE                   FALSE
##   [821,]   FALSE       FALSE          FALSE                   FALSE
##   [822,]   FALSE       FALSE          FALSE                   FALSE
##   [823,]   FALSE       FALSE          FALSE                   FALSE
##   [824,]   FALSE       FALSE          FALSE                   FALSE
##   [825,]   FALSE       FALSE          FALSE                   FALSE
##   [826,]   FALSE       FALSE          FALSE                   FALSE
##   [827,]   FALSE       FALSE          FALSE                   FALSE
##   [828,]   FALSE       FALSE          FALSE                   FALSE
##   [829,]   FALSE       FALSE          FALSE                   FALSE
##   [830,]   FALSE       FALSE          FALSE                   FALSE
##   [831,]   FALSE       FALSE          FALSE                   FALSE
##   [832,]   FALSE       FALSE          FALSE                   FALSE
##   [833,]   FALSE       FALSE          FALSE                   FALSE
##   [834,]   FALSE       FALSE          FALSE                   FALSE
##   [835,]   FALSE       FALSE          FALSE                   FALSE
##   [836,]   FALSE       FALSE          FALSE                   FALSE
##   [837,]   FALSE       FALSE          FALSE                   FALSE
##   [838,]   FALSE       FALSE          FALSE                   FALSE
##   [839,]   FALSE       FALSE          FALSE                   FALSE
##   [840,]   FALSE       FALSE          FALSE                   FALSE
##   [841,]   FALSE       FALSE          FALSE                   FALSE
##   [842,]   FALSE       FALSE          FALSE                   FALSE
##   [843,]   FALSE       FALSE          FALSE                   FALSE
##   [844,]   FALSE       FALSE          FALSE                   FALSE
##   [845,]   FALSE       FALSE          FALSE                   FALSE
##   [846,]   FALSE       FALSE          FALSE                   FALSE
##   [847,]   FALSE       FALSE          FALSE                   FALSE
##   [848,]   FALSE       FALSE          FALSE                   FALSE
##   [849,]   FALSE       FALSE          FALSE                   FALSE
##   [850,]   FALSE       FALSE          FALSE                   FALSE
##   [851,]   FALSE       FALSE          FALSE                   FALSE
##   [852,]   FALSE       FALSE          FALSE                   FALSE
##   [853,]   FALSE       FALSE          FALSE                   FALSE
##   [854,]   FALSE       FALSE          FALSE                   FALSE
##   [855,]   FALSE       FALSE          FALSE                   FALSE
##   [856,]   FALSE       FALSE          FALSE                   FALSE
##   [857,]   FALSE       FALSE          FALSE                   FALSE
##   [858,]   FALSE       FALSE          FALSE                   FALSE
##   [859,]   FALSE       FALSE          FALSE                   FALSE
##   [860,]   FALSE       FALSE          FALSE                   FALSE
##   [861,]   FALSE       FALSE          FALSE                   FALSE
##   [862,]   FALSE       FALSE          FALSE                   FALSE
##   [863,]   FALSE       FALSE          FALSE                   FALSE
##   [864,]   FALSE       FALSE          FALSE                   FALSE
##   [865,]   FALSE       FALSE          FALSE                   FALSE
##   [866,]   FALSE       FALSE          FALSE                   FALSE
##   [867,]   FALSE       FALSE          FALSE                   FALSE
##   [868,]   FALSE       FALSE          FALSE                   FALSE
##   [869,]   FALSE       FALSE          FALSE                   FALSE
##   [870,]   FALSE       FALSE          FALSE                   FALSE
##   [871,]   FALSE       FALSE          FALSE                   FALSE
##   [872,]   FALSE       FALSE          FALSE                   FALSE
##   [873,]   FALSE       FALSE          FALSE                   FALSE
##   [874,]   FALSE       FALSE          FALSE                   FALSE
##   [875,]   FALSE       FALSE          FALSE                   FALSE
##   [876,]   FALSE       FALSE          FALSE                   FALSE
##   [877,]   FALSE       FALSE          FALSE                   FALSE
##   [878,]   FALSE       FALSE          FALSE                   FALSE
##   [879,]   FALSE       FALSE          FALSE                   FALSE
##   [880,]   FALSE       FALSE          FALSE                   FALSE
##   [881,]   FALSE       FALSE          FALSE                   FALSE
##   [882,]   FALSE       FALSE          FALSE                   FALSE
##   [883,]   FALSE       FALSE          FALSE                   FALSE
##   [884,]   FALSE       FALSE          FALSE                   FALSE
##   [885,]   FALSE       FALSE          FALSE                   FALSE
##   [886,]   FALSE       FALSE          FALSE                   FALSE
##   [887,]   FALSE       FALSE          FALSE                   FALSE
##   [888,]   FALSE       FALSE          FALSE                   FALSE
##   [889,]   FALSE       FALSE          FALSE                   FALSE
##   [890,]   FALSE       FALSE          FALSE                   FALSE
##   [891,]   FALSE       FALSE          FALSE                   FALSE
##   [892,]   FALSE       FALSE          FALSE                   FALSE
##   [893,]   FALSE       FALSE          FALSE                   FALSE
##   [894,]   FALSE       FALSE          FALSE                   FALSE
##   [895,]   FALSE       FALSE          FALSE                   FALSE
##   [896,]   FALSE       FALSE          FALSE                   FALSE
##   [897,]   FALSE       FALSE          FALSE                   FALSE
##   [898,]   FALSE       FALSE          FALSE                   FALSE
##   [899,]   FALSE       FALSE          FALSE                   FALSE
##   [900,]   FALSE       FALSE          FALSE                   FALSE
##   [901,]   FALSE       FALSE          FALSE                   FALSE
##   [902,]   FALSE       FALSE          FALSE                   FALSE
##   [903,]   FALSE       FALSE          FALSE                   FALSE
##   [904,]   FALSE       FALSE          FALSE                   FALSE
##   [905,]   FALSE       FALSE          FALSE                   FALSE
##   [906,]   FALSE       FALSE          FALSE                   FALSE
##   [907,]   FALSE       FALSE          FALSE                   FALSE
##   [908,]   FALSE       FALSE          FALSE                   FALSE
##   [909,]   FALSE       FALSE          FALSE                   FALSE
##   [910,]   FALSE       FALSE          FALSE                   FALSE
##   [911,]   FALSE       FALSE          FALSE                   FALSE
##   [912,]   FALSE       FALSE          FALSE                   FALSE
##   [913,]   FALSE       FALSE          FALSE                   FALSE
##   [914,]   FALSE       FALSE          FALSE                   FALSE
##   [915,]   FALSE       FALSE          FALSE                   FALSE
##   [916,]   FALSE       FALSE          FALSE                   FALSE
##   [917,]   FALSE       FALSE          FALSE                   FALSE
##   [918,]   FALSE       FALSE          FALSE                   FALSE
##   [919,]   FALSE       FALSE          FALSE                   FALSE
##   [920,]   FALSE       FALSE          FALSE                   FALSE
##   [921,]   FALSE       FALSE          FALSE                   FALSE
##   [922,]   FALSE       FALSE          FALSE                   FALSE
##   [923,]   FALSE       FALSE          FALSE                   FALSE
##   [924,]   FALSE       FALSE          FALSE                   FALSE
##   [925,]   FALSE       FALSE          FALSE                   FALSE
##   [926,]   FALSE       FALSE          FALSE                   FALSE
##   [927,]   FALSE       FALSE          FALSE                   FALSE
##   [928,]   FALSE       FALSE          FALSE                   FALSE
##   [929,]   FALSE       FALSE          FALSE                   FALSE
##   [930,]   FALSE       FALSE          FALSE                   FALSE
##   [931,]   FALSE       FALSE          FALSE                   FALSE
##   [932,]   FALSE       FALSE          FALSE                   FALSE
##   [933,]   FALSE       FALSE          FALSE                   FALSE
##   [934,]   FALSE       FALSE          FALSE                   FALSE
##   [935,]   FALSE       FALSE          FALSE                   FALSE
##   [936,]   FALSE       FALSE          FALSE                   FALSE
##   [937,]   FALSE       FALSE          FALSE                   FALSE
##   [938,]   FALSE       FALSE          FALSE                   FALSE
##   [939,]   FALSE       FALSE          FALSE                   FALSE
##   [940,]   FALSE       FALSE          FALSE                   FALSE
##   [941,]   FALSE       FALSE          FALSE                   FALSE
##   [942,]   FALSE       FALSE          FALSE                   FALSE
##   [943,]   FALSE       FALSE          FALSE                   FALSE
##   [944,]   FALSE       FALSE          FALSE                   FALSE
##   [945,]   FALSE       FALSE          FALSE                   FALSE
##   [946,]   FALSE       FALSE          FALSE                   FALSE
##   [947,]   FALSE       FALSE          FALSE                   FALSE
##   [948,]   FALSE       FALSE          FALSE                   FALSE
##   [949,]   FALSE       FALSE          FALSE                   FALSE
##   [950,]   FALSE       FALSE          FALSE                   FALSE
##   [951,]   FALSE       FALSE          FALSE                   FALSE
##   [952,]   FALSE       FALSE          FALSE                   FALSE
##   [953,]   FALSE       FALSE          FALSE                   FALSE
##   [954,]   FALSE       FALSE          FALSE                   FALSE
##   [955,]   FALSE       FALSE          FALSE                   FALSE
##   [956,]   FALSE       FALSE          FALSE                   FALSE
##   [957,]   FALSE       FALSE          FALSE                   FALSE
##   [958,]   FALSE       FALSE          FALSE                   FALSE
##   [959,]   FALSE       FALSE          FALSE                   FALSE
##   [960,]   FALSE       FALSE          FALSE                   FALSE
##   [961,]   FALSE       FALSE          FALSE                   FALSE
##   [962,]   FALSE       FALSE          FALSE                   FALSE
##   [963,]   FALSE       FALSE          FALSE                   FALSE
##   [964,]   FALSE       FALSE          FALSE                   FALSE
##   [965,]   FALSE       FALSE          FALSE                   FALSE
##   [966,]   FALSE       FALSE          FALSE                   FALSE
##   [967,]   FALSE       FALSE          FALSE                   FALSE
##   [968,]   FALSE       FALSE          FALSE                   FALSE
##   [969,]   FALSE       FALSE          FALSE                   FALSE
##   [970,]   FALSE       FALSE          FALSE                   FALSE
##   [971,]   FALSE       FALSE          FALSE                   FALSE
##   [972,]   FALSE       FALSE          FALSE                   FALSE
##   [973,]   FALSE       FALSE          FALSE                   FALSE
##   [974,]   FALSE       FALSE          FALSE                   FALSE
##   [975,]   FALSE       FALSE          FALSE                   FALSE
##   [976,]   FALSE       FALSE          FALSE                   FALSE
##   [977,]   FALSE       FALSE          FALSE                   FALSE
##   [978,]   FALSE       FALSE          FALSE                   FALSE
##   [979,]   FALSE       FALSE          FALSE                   FALSE
##   [980,]   FALSE       FALSE          FALSE                   FALSE
##   [981,]   FALSE       FALSE          FALSE                   FALSE
##   [982,]   FALSE       FALSE          FALSE                   FALSE
##   [983,]   FALSE       FALSE          FALSE                   FALSE
##   [984,]   FALSE       FALSE          FALSE                   FALSE
##   [985,]   FALSE       FALSE          FALSE                   FALSE
##   [986,]   FALSE       FALSE          FALSE                   FALSE
##   [987,]   FALSE       FALSE          FALSE                   FALSE
##   [988,]   FALSE       FALSE          FALSE                   FALSE
##   [989,]   FALSE       FALSE          FALSE                   FALSE
##   [990,]   FALSE       FALSE          FALSE                   FALSE
##   [991,]   FALSE       FALSE          FALSE                   FALSE
##   [992,]   FALSE       FALSE          FALSE                   FALSE
##   [993,]   FALSE       FALSE          FALSE                   FALSE
##   [994,]   FALSE       FALSE          FALSE                   FALSE
##   [995,]   FALSE       FALSE          FALSE                   FALSE
##   [996,]   FALSE       FALSE          FALSE                   FALSE
##   [997,]   FALSE       FALSE          FALSE                   FALSE
##   [998,]   FALSE       FALSE          FALSE                   FALSE
##   [999,]   FALSE       FALSE          FALSE                   FALSE
##  [1000,]   FALSE       FALSE          FALSE                   FALSE
##  [1001,]   FALSE       FALSE          FALSE                   FALSE
##  [1002,]   FALSE       FALSE          FALSE                   FALSE
##  [1003,]   FALSE       FALSE          FALSE                   FALSE
##  [1004,]   FALSE       FALSE          FALSE                   FALSE
##  [1005,]   FALSE       FALSE          FALSE                   FALSE
##  [1006,]   FALSE       FALSE          FALSE                   FALSE
##  [1007,]   FALSE       FALSE          FALSE                   FALSE
##  [1008,]   FALSE       FALSE          FALSE                   FALSE
##  [1009,]   FALSE       FALSE          FALSE                   FALSE
##  [1010,]   FALSE       FALSE          FALSE                   FALSE
##  [1011,]   FALSE       FALSE          FALSE                   FALSE
##  [1012,]   FALSE       FALSE          FALSE                   FALSE
##  [1013,]   FALSE       FALSE          FALSE                   FALSE
##  [1014,]   FALSE       FALSE          FALSE                   FALSE
##  [1015,]   FALSE       FALSE          FALSE                   FALSE
##  [1016,]   FALSE       FALSE          FALSE                   FALSE
##  [1017,]   FALSE       FALSE          FALSE                   FALSE
##  [1018,]   FALSE       FALSE          FALSE                   FALSE
##  [1019,]   FALSE       FALSE          FALSE                   FALSE
##  [1020,]   FALSE       FALSE          FALSE                   FALSE
##  [1021,]   FALSE       FALSE          FALSE                   FALSE
##  [1022,]   FALSE       FALSE          FALSE                   FALSE
##  [1023,]   FALSE       FALSE          FALSE                   FALSE
##  [1024,]   FALSE       FALSE          FALSE                   FALSE
##  [1025,]   FALSE       FALSE          FALSE                   FALSE
##  [1026,]   FALSE       FALSE          FALSE                   FALSE
##  [1027,]   FALSE       FALSE          FALSE                   FALSE
##  [1028,]   FALSE       FALSE          FALSE                   FALSE
##  [1029,]   FALSE       FALSE          FALSE                   FALSE
##  [1030,]   FALSE       FALSE          FALSE                   FALSE
##  [1031,]   FALSE       FALSE          FALSE                   FALSE
##  [1032,]   FALSE       FALSE          FALSE                   FALSE
##  [1033,]   FALSE       FALSE          FALSE                   FALSE
##  [1034,]   FALSE       FALSE          FALSE                   FALSE
##  [1035,]   FALSE       FALSE          FALSE                   FALSE
##  [1036,]   FALSE       FALSE          FALSE                   FALSE
##  [1037,]   FALSE       FALSE          FALSE                   FALSE
##  [1038,]   FALSE       FALSE          FALSE                   FALSE
##  [1039,]   FALSE       FALSE          FALSE                   FALSE
##  [1040,]   FALSE       FALSE          FALSE                   FALSE
##  [1041,]   FALSE       FALSE          FALSE                   FALSE
##  [1042,]   FALSE       FALSE          FALSE                   FALSE
##  [1043,]   FALSE       FALSE          FALSE                   FALSE
##  [1044,]   FALSE       FALSE          FALSE                   FALSE
##  [1045,]   FALSE       FALSE          FALSE                   FALSE
##  [1046,]   FALSE       FALSE          FALSE                   FALSE
##  [1047,]   FALSE       FALSE          FALSE                   FALSE
##  [1048,]   FALSE       FALSE          FALSE                   FALSE
##  [1049,]   FALSE       FALSE          FALSE                   FALSE
##  [1050,]   FALSE       FALSE          FALSE                   FALSE
##  [1051,]   FALSE       FALSE          FALSE                   FALSE
##  [1052,]   FALSE       FALSE          FALSE                   FALSE
##  [1053,]   FALSE       FALSE          FALSE                   FALSE
##  [1054,]   FALSE       FALSE          FALSE                   FALSE
##  [1055,]   FALSE       FALSE          FALSE                   FALSE
##  [1056,]   FALSE       FALSE          FALSE                   FALSE
##  [1057,]   FALSE       FALSE          FALSE                   FALSE
##  [1058,]   FALSE       FALSE          FALSE                   FALSE
##  [1059,]   FALSE       FALSE          FALSE                   FALSE
##  [1060,]   FALSE       FALSE          FALSE                   FALSE
##  [1061,]   FALSE       FALSE          FALSE                   FALSE
##  [1062,]   FALSE       FALSE          FALSE                   FALSE
##  [1063,]   FALSE       FALSE          FALSE                   FALSE
##  [1064,]   FALSE       FALSE          FALSE                   FALSE
##  [1065,]   FALSE       FALSE          FALSE                   FALSE
##  [1066,]   FALSE       FALSE          FALSE                   FALSE
##  [1067,]   FALSE       FALSE          FALSE                   FALSE
##  [1068,]   FALSE       FALSE          FALSE                   FALSE
##  [1069,]   FALSE       FALSE          FALSE                   FALSE
##  [1070,]   FALSE       FALSE          FALSE                   FALSE
##  [1071,]   FALSE       FALSE          FALSE                   FALSE
##  [1072,]   FALSE       FALSE          FALSE                   FALSE
##  [1073,]   FALSE       FALSE          FALSE                   FALSE
##  [1074,]   FALSE       FALSE          FALSE                   FALSE
##  [1075,]   FALSE       FALSE          FALSE                   FALSE
##  [1076,]   FALSE       FALSE          FALSE                   FALSE
##  [1077,]   FALSE       FALSE          FALSE                   FALSE
##  [1078,]   FALSE       FALSE          FALSE                   FALSE
##  [1079,]   FALSE       FALSE          FALSE                   FALSE
##  [1080,]   FALSE       FALSE          FALSE                   FALSE
##  [1081,]   FALSE       FALSE          FALSE                   FALSE
##  [1082,]   FALSE       FALSE          FALSE                   FALSE
##  [1083,]   FALSE       FALSE          FALSE                   FALSE
##  [1084,]   FALSE       FALSE          FALSE                   FALSE
##  [1085,]   FALSE       FALSE          FALSE                   FALSE
##  [1086,]   FALSE       FALSE          FALSE                   FALSE
##  [1087,]   FALSE       FALSE          FALSE                   FALSE
##  [1088,]   FALSE       FALSE          FALSE                   FALSE
##  [1089,]   FALSE       FALSE          FALSE                   FALSE
##  [1090,]   FALSE       FALSE          FALSE                   FALSE
##  [1091,]   FALSE       FALSE          FALSE                   FALSE
##  [1092,]   FALSE       FALSE          FALSE                   FALSE
##  [1093,]   FALSE       FALSE          FALSE                   FALSE
##  [1094,]   FALSE       FALSE          FALSE                   FALSE
##  [1095,]   FALSE       FALSE          FALSE                   FALSE
##  [1096,]   FALSE       FALSE          FALSE                   FALSE
##  [1097,]   FALSE       FALSE          FALSE                   FALSE
##  [1098,]   FALSE       FALSE          FALSE                   FALSE
##  [1099,]   FALSE       FALSE          FALSE                   FALSE
##  [1100,]   FALSE       FALSE          FALSE                   FALSE
##  [1101,]   FALSE       FALSE          FALSE                   FALSE
##  [1102,]   FALSE       FALSE          FALSE                   FALSE
##  [1103,]   FALSE       FALSE          FALSE                   FALSE
##  [1104,]   FALSE       FALSE          FALSE                   FALSE
##  [1105,]   FALSE       FALSE          FALSE                   FALSE
##  [1106,]   FALSE       FALSE          FALSE                   FALSE
##  [1107,]   FALSE       FALSE          FALSE                   FALSE
##  [1108,]   FALSE       FALSE          FALSE                   FALSE
##  [1109,]   FALSE       FALSE          FALSE                   FALSE
##  [1110,]   FALSE       FALSE          FALSE                   FALSE
##  [1111,]   FALSE       FALSE          FALSE                   FALSE
##  [1112,]   FALSE       FALSE          FALSE                   FALSE
##  [1113,]   FALSE       FALSE          FALSE                   FALSE
##  [1114,]   FALSE       FALSE          FALSE                   FALSE
##  [1115,]   FALSE       FALSE          FALSE                   FALSE
##  [1116,]   FALSE       FALSE          FALSE                   FALSE
##  [1117,]   FALSE       FALSE          FALSE                   FALSE
##  [1118,]   FALSE       FALSE          FALSE                   FALSE
##  [1119,]   FALSE       FALSE          FALSE                   FALSE
##  [1120,]   FALSE       FALSE          FALSE                   FALSE
##  [1121,]   FALSE       FALSE          FALSE                   FALSE
##  [1122,]   FALSE       FALSE          FALSE                   FALSE
##  [1123,]   FALSE       FALSE          FALSE                   FALSE
##  [1124,]   FALSE       FALSE          FALSE                   FALSE
##  [1125,]   FALSE       FALSE          FALSE                   FALSE
##  [1126,]   FALSE       FALSE          FALSE                   FALSE
##  [1127,]   FALSE       FALSE          FALSE                   FALSE
##  [1128,]   FALSE       FALSE          FALSE                   FALSE
##  [1129,]   FALSE       FALSE          FALSE                   FALSE
##  [1130,]   FALSE       FALSE          FALSE                   FALSE
##  [1131,]   FALSE       FALSE          FALSE                   FALSE
##  [1132,]   FALSE       FALSE          FALSE                   FALSE
##  [1133,]   FALSE       FALSE          FALSE                   FALSE
##  [1134,]   FALSE       FALSE          FALSE                   FALSE
##  [1135,]   FALSE       FALSE          FALSE                   FALSE
##  [1136,]   FALSE       FALSE          FALSE                   FALSE
##  [1137,]   FALSE       FALSE          FALSE                   FALSE
##  [1138,]   FALSE       FALSE          FALSE                   FALSE
##  [1139,]   FALSE       FALSE          FALSE                   FALSE
##  [1140,]   FALSE       FALSE          FALSE                   FALSE
##  [1141,]   FALSE       FALSE          FALSE                   FALSE
##  [1142,]   FALSE       FALSE          FALSE                   FALSE
##  [1143,]   FALSE       FALSE          FALSE                   FALSE
##  [1144,]   FALSE       FALSE          FALSE                   FALSE
##  [1145,]   FALSE       FALSE          FALSE                   FALSE
##  [1146,]   FALSE       FALSE          FALSE                   FALSE
##  [1147,]   FALSE       FALSE          FALSE                   FALSE
##  [1148,]   FALSE       FALSE          FALSE                   FALSE
##  [1149,]   FALSE       FALSE          FALSE                   FALSE
##  [1150,]   FALSE       FALSE          FALSE                   FALSE
##  [1151,]   FALSE       FALSE          FALSE                   FALSE
##  [1152,]   FALSE       FALSE          FALSE                   FALSE
##  [1153,]   FALSE       FALSE          FALSE                   FALSE
##  [1154,]   FALSE       FALSE          FALSE                   FALSE
##  [1155,]   FALSE       FALSE          FALSE                   FALSE
##  [1156,]   FALSE       FALSE          FALSE                   FALSE
##  [1157,]   FALSE       FALSE          FALSE                   FALSE
##  [1158,]   FALSE       FALSE          FALSE                   FALSE
##  [1159,]   FALSE       FALSE          FALSE                   FALSE
##  [1160,]   FALSE       FALSE          FALSE                   FALSE
##  [1161,]   FALSE       FALSE          FALSE                   FALSE
##  [1162,]   FALSE       FALSE          FALSE                   FALSE
##  [1163,]   FALSE       FALSE          FALSE                   FALSE
##  [1164,]   FALSE       FALSE          FALSE                   FALSE
##  [1165,]   FALSE       FALSE          FALSE                   FALSE
##  [1166,]   FALSE       FALSE          FALSE                   FALSE
##  [1167,]   FALSE       FALSE          FALSE                   FALSE
##  [1168,]   FALSE       FALSE          FALSE                   FALSE
##  [1169,]   FALSE       FALSE          FALSE                   FALSE
##  [1170,]   FALSE       FALSE          FALSE                   FALSE
##  [1171,]   FALSE       FALSE          FALSE                   FALSE
##  [1172,]   FALSE       FALSE          FALSE                   FALSE
##  [1173,]   FALSE       FALSE          FALSE                   FALSE
##  [1174,]   FALSE       FALSE          FALSE                   FALSE
##  [1175,]   FALSE       FALSE          FALSE                   FALSE
##  [1176,]   FALSE       FALSE          FALSE                   FALSE
##  [1177,]   FALSE       FALSE          FALSE                   FALSE
##  [1178,]   FALSE       FALSE          FALSE                   FALSE
##  [1179,]   FALSE       FALSE          FALSE                   FALSE
##  [1180,]   FALSE       FALSE          FALSE                   FALSE
##  [1181,]   FALSE       FALSE          FALSE                   FALSE
##  [1182,]   FALSE       FALSE          FALSE                   FALSE
##  [1183,]   FALSE       FALSE          FALSE                   FALSE
##  [1184,]   FALSE       FALSE          FALSE                   FALSE
##  [1185,]   FALSE       FALSE          FALSE                   FALSE
##  [1186,]   FALSE       FALSE          FALSE                   FALSE
##  [1187,]   FALSE       FALSE          FALSE                   FALSE
##  [1188,]   FALSE       FALSE          FALSE                   FALSE
##  [1189,]   FALSE       FALSE          FALSE                   FALSE
##  [1190,]   FALSE       FALSE          FALSE                   FALSE
##  [1191,]   FALSE       FALSE          FALSE                   FALSE
##  [1192,]   FALSE       FALSE          FALSE                   FALSE
##  [1193,]   FALSE       FALSE          FALSE                   FALSE
##  [1194,]   FALSE       FALSE          FALSE                   FALSE
##  [1195,]   FALSE       FALSE          FALSE                   FALSE
##  [1196,]   FALSE       FALSE          FALSE                   FALSE
##  [1197,]   FALSE       FALSE          FALSE                   FALSE
##  [1198,]   FALSE       FALSE          FALSE                   FALSE
##  [1199,]   FALSE       FALSE          FALSE                   FALSE
##  [1200,]   FALSE       FALSE          FALSE                   FALSE
##  [1201,]   FALSE       FALSE          FALSE                   FALSE
##  [1202,]   FALSE       FALSE          FALSE                   FALSE
##  [1203,]   FALSE       FALSE          FALSE                   FALSE
##  [1204,]   FALSE       FALSE          FALSE                   FALSE
##  [1205,]   FALSE       FALSE          FALSE                   FALSE
##  [1206,]   FALSE       FALSE          FALSE                   FALSE
##  [1207,]   FALSE       FALSE          FALSE                   FALSE
##  [1208,]   FALSE       FALSE          FALSE                   FALSE
##  [1209,]   FALSE       FALSE          FALSE                   FALSE
##  [1210,]   FALSE       FALSE          FALSE                   FALSE
##  [1211,]   FALSE       FALSE          FALSE                   FALSE
##  [1212,]   FALSE       FALSE          FALSE                   FALSE
##  [1213,]   FALSE       FALSE          FALSE                   FALSE
##  [1214,]   FALSE       FALSE          FALSE                   FALSE
##  [1215,]   FALSE       FALSE          FALSE                   FALSE
##  [1216,]   FALSE       FALSE          FALSE                   FALSE
##  [1217,]   FALSE       FALSE          FALSE                   FALSE
##  [1218,]   FALSE       FALSE          FALSE                   FALSE
##  [1219,]   FALSE       FALSE          FALSE                   FALSE
##  [1220,]   FALSE       FALSE          FALSE                   FALSE
##  [1221,]   FALSE       FALSE          FALSE                   FALSE
##  [1222,]   FALSE       FALSE          FALSE                   FALSE
##  [1223,]   FALSE       FALSE          FALSE                   FALSE
##  [1224,]   FALSE       FALSE          FALSE                   FALSE
##  [1225,]   FALSE       FALSE          FALSE                   FALSE
##  [1226,]   FALSE       FALSE          FALSE                   FALSE
##  [1227,]   FALSE       FALSE          FALSE                   FALSE
##  [1228,]   FALSE       FALSE          FALSE                   FALSE
##  [1229,]   FALSE       FALSE          FALSE                   FALSE
##  [1230,]   FALSE       FALSE          FALSE                   FALSE
##  [1231,]   FALSE       FALSE          FALSE                   FALSE
##  [1232,]   FALSE       FALSE          FALSE                   FALSE
##  [1233,]   FALSE       FALSE          FALSE                   FALSE
##  [1234,]   FALSE       FALSE          FALSE                   FALSE
##  [1235,]   FALSE       FALSE          FALSE                   FALSE
##  [1236,]   FALSE       FALSE          FALSE                   FALSE
##  [1237,]   FALSE       FALSE          FALSE                   FALSE
##  [1238,]   FALSE       FALSE          FALSE                   FALSE
##  [1239,]   FALSE       FALSE          FALSE                   FALSE
##  [1240,]   FALSE       FALSE          FALSE                   FALSE
##  [1241,]   FALSE       FALSE          FALSE                   FALSE
##  [1242,]   FALSE       FALSE          FALSE                   FALSE
##  [1243,]   FALSE       FALSE          FALSE                   FALSE
##  [1244,]   FALSE       FALSE          FALSE                   FALSE
##  [1245,]   FALSE       FALSE          FALSE                   FALSE
##  [1246,]   FALSE       FALSE          FALSE                   FALSE
##  [1247,]   FALSE       FALSE          FALSE                   FALSE
##  [1248,]   FALSE       FALSE          FALSE                   FALSE
##  [1249,]   FALSE       FALSE          FALSE                   FALSE
##  [1250,]   FALSE       FALSE          FALSE                   FALSE
##  [1251,]   FALSE       FALSE          FALSE                   FALSE
##  [1252,]   FALSE       FALSE          FALSE                   FALSE
##  [1253,]   FALSE       FALSE          FALSE                   FALSE
##  [1254,]   FALSE       FALSE          FALSE                   FALSE
##  [1255,]   FALSE       FALSE          FALSE                   FALSE
##  [1256,]   FALSE       FALSE          FALSE                   FALSE
##  [1257,]   FALSE       FALSE          FALSE                   FALSE
##  [1258,]   FALSE       FALSE          FALSE                   FALSE
##  [1259,]   FALSE       FALSE          FALSE                   FALSE
##  [1260,]   FALSE       FALSE          FALSE                   FALSE
##  [1261,]   FALSE       FALSE          FALSE                   FALSE
##  [1262,]   FALSE       FALSE          FALSE                   FALSE
##  [1263,]   FALSE       FALSE          FALSE                   FALSE
##  [1264,]   FALSE       FALSE          FALSE                   FALSE
##  [1265,]   FALSE       FALSE          FALSE                   FALSE
##  [1266,]   FALSE       FALSE          FALSE                   FALSE
##  [1267,]   FALSE       FALSE          FALSE                   FALSE
##  [1268,]   FALSE       FALSE          FALSE                   FALSE
##  [1269,]   FALSE       FALSE          FALSE                   FALSE
##  [1270,]   FALSE       FALSE          FALSE                   FALSE
##  [1271,]   FALSE       FALSE          FALSE                   FALSE
##  [1272,]   FALSE       FALSE          FALSE                   FALSE
##  [1273,]   FALSE       FALSE          FALSE                   FALSE
##  [1274,]   FALSE       FALSE          FALSE                   FALSE
##  [1275,]   FALSE       FALSE          FALSE                   FALSE
##  [1276,]   FALSE       FALSE          FALSE                   FALSE
##  [1277,]   FALSE       FALSE          FALSE                   FALSE
##  [1278,]   FALSE       FALSE          FALSE                   FALSE
##  [1279,]   FALSE       FALSE          FALSE                   FALSE
##  [1280,]   FALSE       FALSE          FALSE                   FALSE
##  [1281,]   FALSE       FALSE          FALSE                   FALSE
##  [1282,]   FALSE       FALSE          FALSE                   FALSE
##  [1283,]   FALSE       FALSE          FALSE                   FALSE
##  [1284,]   FALSE       FALSE          FALSE                   FALSE
##  [1285,]   FALSE       FALSE          FALSE                   FALSE
##  [1286,]   FALSE       FALSE          FALSE                   FALSE
##  [1287,]   FALSE       FALSE          FALSE                   FALSE
##  [1288,]   FALSE       FALSE          FALSE                   FALSE
##  [1289,]   FALSE       FALSE          FALSE                   FALSE
##  [1290,]   FALSE       FALSE          FALSE                   FALSE
##  [1291,]   FALSE       FALSE          FALSE                   FALSE
##  [1292,]   FALSE       FALSE          FALSE                   FALSE
##  [1293,]   FALSE       FALSE          FALSE                   FALSE
##  [1294,]   FALSE       FALSE          FALSE                   FALSE
##  [1295,]   FALSE       FALSE          FALSE                   FALSE
##  [1296,]   FALSE       FALSE          FALSE                   FALSE
##  [1297,]   FALSE       FALSE          FALSE                   FALSE
##  [1298,]   FALSE       FALSE          FALSE                   FALSE
##  [1299,]   FALSE       FALSE          FALSE                   FALSE
##  [1300,]   FALSE       FALSE          FALSE                   FALSE
##  [1301,]   FALSE       FALSE          FALSE                   FALSE
##  [1302,]   FALSE       FALSE          FALSE                   FALSE
##  [1303,]   FALSE       FALSE          FALSE                   FALSE
##  [1304,]   FALSE       FALSE          FALSE                   FALSE
##  [1305,]   FALSE       FALSE          FALSE                   FALSE
##  [1306,]   FALSE       FALSE          FALSE                   FALSE
##  [1307,]   FALSE       FALSE          FALSE                   FALSE
##  [1308,]   FALSE       FALSE          FALSE                   FALSE
##  [1309,]   FALSE       FALSE          FALSE                   FALSE
##  [1310,]   FALSE       FALSE          FALSE                   FALSE
##  [1311,]   FALSE       FALSE          FALSE                   FALSE
##  [1312,]   FALSE       FALSE          FALSE                   FALSE
##  [1313,]   FALSE       FALSE          FALSE                   FALSE
##  [1314,]   FALSE       FALSE          FALSE                   FALSE
##  [1315,]   FALSE       FALSE          FALSE                   FALSE
##  [1316,]   FALSE       FALSE          FALSE                   FALSE
##  [1317,]   FALSE       FALSE          FALSE                   FALSE
##  [1318,]   FALSE       FALSE          FALSE                   FALSE
##  [1319,]   FALSE       FALSE          FALSE                   FALSE
##  [1320,]   FALSE       FALSE          FALSE                   FALSE
##  [1321,]   FALSE       FALSE          FALSE                   FALSE
##  [1322,]   FALSE       FALSE          FALSE                   FALSE
##  [1323,]   FALSE       FALSE          FALSE                   FALSE
##  [1324,]   FALSE       FALSE          FALSE                   FALSE
##  [1325,]   FALSE       FALSE          FALSE                   FALSE
##  [1326,]   FALSE       FALSE          FALSE                   FALSE
##  [1327,]   FALSE       FALSE          FALSE                   FALSE
##  [1328,]   FALSE       FALSE          FALSE                   FALSE
##  [1329,]   FALSE       FALSE          FALSE                   FALSE
##  [1330,]   FALSE       FALSE          FALSE                   FALSE
##  [1331,]   FALSE       FALSE          FALSE                   FALSE
##  [1332,]   FALSE       FALSE          FALSE                   FALSE
##  [1333,]   FALSE       FALSE          FALSE                   FALSE
##  [1334,]   FALSE       FALSE          FALSE                   FALSE
##  [1335,]   FALSE       FALSE          FALSE                   FALSE
##  [1336,]   FALSE       FALSE          FALSE                   FALSE
##  [1337,]   FALSE       FALSE          FALSE                   FALSE
##  [1338,]   FALSE       FALSE          FALSE                   FALSE
##  [1339,]   FALSE       FALSE          FALSE                   FALSE
##  [1340,]   FALSE       FALSE          FALSE                   FALSE
##  [1341,]   FALSE       FALSE          FALSE                   FALSE
##  [1342,]   FALSE       FALSE          FALSE                   FALSE
##  [1343,]   FALSE       FALSE          FALSE                   FALSE
##  [1344,]   FALSE       FALSE          FALSE                   FALSE
##  [1345,]   FALSE       FALSE          FALSE                   FALSE
##  [1346,]   FALSE       FALSE          FALSE                   FALSE
##  [1347,]   FALSE       FALSE          FALSE                   FALSE
##  [1348,]   FALSE       FALSE          FALSE                   FALSE
##  [1349,]   FALSE       FALSE          FALSE                   FALSE
##  [1350,]   FALSE       FALSE          FALSE                   FALSE
##  [1351,]   FALSE       FALSE          FALSE                   FALSE
##  [1352,]   FALSE       FALSE          FALSE                   FALSE
##  [1353,]   FALSE       FALSE          FALSE                   FALSE
##  [1354,]   FALSE       FALSE          FALSE                   FALSE
##  [1355,]   FALSE       FALSE          FALSE                   FALSE
##  [1356,]   FALSE       FALSE          FALSE                   FALSE
##  [1357,]   FALSE       FALSE          FALSE                   FALSE
##  [1358,]   FALSE       FALSE          FALSE                   FALSE
##  [1359,]   FALSE       FALSE          FALSE                   FALSE
##  [1360,]   FALSE       FALSE          FALSE                   FALSE
##  [1361,]   FALSE       FALSE          FALSE                   FALSE
##  [1362,]   FALSE       FALSE          FALSE                   FALSE
##  [1363,]   FALSE       FALSE          FALSE                   FALSE
##  [1364,]   FALSE       FALSE          FALSE                   FALSE
##  [1365,]   FALSE       FALSE          FALSE                   FALSE
##  [1366,]   FALSE       FALSE          FALSE                   FALSE
##  [1367,]   FALSE       FALSE          FALSE                   FALSE
##  [1368,]   FALSE       FALSE          FALSE                   FALSE
##  [1369,]   FALSE       FALSE          FALSE                   FALSE
##  [1370,]   FALSE       FALSE          FALSE                   FALSE
##  [1371,]   FALSE       FALSE          FALSE                   FALSE
##  [1372,]   FALSE       FALSE          FALSE                   FALSE
##  [1373,]   FALSE       FALSE          FALSE                   FALSE
##  [1374,]   FALSE       FALSE          FALSE                   FALSE
##  [1375,]   FALSE       FALSE          FALSE                   FALSE
##  [1376,]   FALSE       FALSE          FALSE                   FALSE
##  [1377,]   FALSE       FALSE          FALSE                   FALSE
##  [1378,]   FALSE       FALSE          FALSE                   FALSE
##  [1379,]   FALSE       FALSE          FALSE                   FALSE
##  [1380,]   FALSE       FALSE          FALSE                   FALSE
##  [1381,]   FALSE       FALSE          FALSE                   FALSE
##  [1382,]   FALSE       FALSE          FALSE                   FALSE
##  [1383,]   FALSE       FALSE          FALSE                   FALSE
##  [1384,]   FALSE       FALSE          FALSE                   FALSE
##  [1385,]   FALSE       FALSE          FALSE                   FALSE
##  [1386,]   FALSE       FALSE          FALSE                   FALSE
##  [1387,]   FALSE       FALSE          FALSE                   FALSE
##  [1388,]   FALSE       FALSE          FALSE                   FALSE
##  [1389,]   FALSE       FALSE          FALSE                   FALSE
##  [1390,]   FALSE       FALSE          FALSE                   FALSE
##  [1391,]   FALSE       FALSE          FALSE                   FALSE
##  [1392,]   FALSE       FALSE          FALSE                   FALSE
##  [1393,]   FALSE       FALSE          FALSE                   FALSE
##  [1394,]   FALSE       FALSE          FALSE                   FALSE
##  [1395,]   FALSE       FALSE          FALSE                   FALSE
##  [1396,]   FALSE       FALSE          FALSE                   FALSE
##  [1397,]   FALSE       FALSE          FALSE                   FALSE
##  [1398,]   FALSE       FALSE          FALSE                   FALSE
##  [1399,]   FALSE       FALSE          FALSE                   FALSE
##  [1400,]   FALSE       FALSE          FALSE                   FALSE
##  [1401,]   FALSE       FALSE          FALSE                   FALSE
##  [1402,]   FALSE       FALSE          FALSE                   FALSE
##  [1403,]   FALSE       FALSE          FALSE                   FALSE
##  [1404,]   FALSE       FALSE          FALSE                   FALSE
##  [1405,]   FALSE       FALSE          FALSE                   FALSE
##  [1406,]   FALSE       FALSE          FALSE                   FALSE
##  [1407,]   FALSE       FALSE          FALSE                   FALSE
##  [1408,]   FALSE       FALSE          FALSE                   FALSE
##          ASFIS species# ASFIS species name FAO major fishing area Measure  1950
##     [1,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [2,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [3,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [4,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [5,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [6,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [7,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [8,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##     [9,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [10,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [11,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [12,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [13,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [14,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [15,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [16,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [17,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [18,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [19,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [20,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [21,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [22,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [23,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [24,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [25,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [26,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [27,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [28,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [29,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [30,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [31,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [32,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [33,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [34,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [35,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [36,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [37,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [38,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [39,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [40,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [41,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [42,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [43,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [44,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [45,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [46,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [47,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [48,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [49,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [50,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [51,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [52,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [53,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [54,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [55,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [56,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [57,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [58,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [59,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [60,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [61,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [62,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [63,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [64,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [65,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [66,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [67,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [68,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [69,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [70,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [71,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [72,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [73,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [74,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [75,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [76,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [77,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [78,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [79,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [80,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [81,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [82,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [83,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [84,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [85,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [86,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [87,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [88,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [89,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [90,]          FALSE              FALSE                  FALSE   FALSE FALSE
##    [91,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [92,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [93,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [94,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [95,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [96,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [97,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [98,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##    [99,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [100,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [101,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [102,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [103,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [104,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [105,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [106,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [107,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [108,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [109,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [110,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [111,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [112,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [113,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [114,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [115,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [116,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [117,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [118,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [119,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [120,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [121,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [122,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [123,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [124,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [125,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [126,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [127,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [128,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [129,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [130,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [131,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [132,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [133,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [134,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [135,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [136,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [137,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [138,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [139,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [140,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [141,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [142,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [143,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [144,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [145,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [146,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [147,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [148,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [149,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [150,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [151,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [152,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [153,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [154,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [155,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [156,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [157,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [158,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [159,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [160,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [161,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [162,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [163,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [164,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [165,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [166,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [167,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [168,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [169,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [170,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [171,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [172,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [173,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [174,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [175,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [176,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [177,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [178,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [179,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [180,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [181,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [182,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [183,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [184,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [185,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [186,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [187,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [188,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [189,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [190,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [191,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [192,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [193,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [194,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [195,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [196,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [197,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [198,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [199,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [200,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [201,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [202,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [203,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [204,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [205,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [206,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [207,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [208,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [209,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [210,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [211,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [212,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [213,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [214,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [215,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [216,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [217,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [218,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [219,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [220,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [221,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [222,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [223,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [224,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [225,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [226,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [227,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [228,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [229,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [230,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [231,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [232,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [233,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [234,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [235,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [236,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [237,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [238,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [239,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [240,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [241,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [242,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [243,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [244,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [245,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [246,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [247,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [248,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [249,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [250,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [251,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [252,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [253,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [254,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [255,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [256,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [257,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [258,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [259,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [260,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [261,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [262,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [263,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [264,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [265,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [266,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [267,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [268,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [269,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [270,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [271,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [272,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [273,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [274,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [275,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [276,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [277,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [278,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [279,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [280,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [281,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [282,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [283,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [284,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [285,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [286,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [287,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [288,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [289,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [290,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [291,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [292,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [293,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [294,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [295,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [296,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [297,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [298,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [299,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [300,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [301,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [302,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [303,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [304,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [305,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [306,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [307,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [308,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [309,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [310,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [311,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [312,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [313,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [314,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [315,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [316,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [317,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [318,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [319,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [320,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [321,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [322,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [323,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [324,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [325,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [326,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [327,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [328,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [329,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [330,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [331,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [332,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [333,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [334,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [335,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [336,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [337,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [338,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [339,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [340,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [341,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [342,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [343,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [344,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [345,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [346,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [347,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [348,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [349,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [350,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [351,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [352,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [353,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [354,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [355,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [356,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [357,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [358,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [359,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [360,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [361,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [362,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [363,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [364,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [365,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [366,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [367,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [368,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [369,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [370,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [371,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [372,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [373,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [374,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [375,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [376,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [377,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [378,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [379,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [380,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [381,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [382,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [383,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [384,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [385,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [386,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [387,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [388,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [389,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [390,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [391,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [392,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [393,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [394,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [395,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [396,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [397,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [398,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [399,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [400,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [401,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [402,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [403,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [404,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [405,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [406,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [407,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [408,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [409,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [410,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [411,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [412,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [413,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [414,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [415,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [416,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [417,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [418,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [419,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [420,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [421,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [422,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [423,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [424,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [425,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [426,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [427,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [428,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [429,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [430,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [431,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [432,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [433,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [434,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [435,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [436,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [437,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [438,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [439,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [440,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [441,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [442,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [443,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [444,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [445,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [446,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [447,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [448,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [449,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [450,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [451,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [452,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [453,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [454,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [455,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [456,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [457,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [458,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [459,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [460,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [461,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [462,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [463,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [464,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [465,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [466,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [467,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [468,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [469,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [470,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [471,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [472,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [473,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [474,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [475,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [476,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [477,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [478,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [479,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [480,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [481,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [482,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [483,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [484,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [485,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [486,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [487,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [488,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [489,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [490,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [491,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [492,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [493,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [494,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [495,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [496,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [497,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [498,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [499,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [500,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [501,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [502,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [503,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [504,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [505,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [506,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [507,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [508,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [509,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [510,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [511,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [512,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [513,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [514,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [515,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [516,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [517,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [518,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [519,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [520,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [521,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [522,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [523,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [524,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [525,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [526,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [527,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [528,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [529,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [530,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [531,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [532,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [533,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [534,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [535,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [536,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [537,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [538,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [539,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [540,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [541,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [542,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [543,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [544,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [545,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [546,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [547,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [548,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [549,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [550,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [551,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [552,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [553,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [554,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [555,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [556,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [557,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [558,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [559,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [560,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [561,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [562,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [563,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [564,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [565,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [566,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [567,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [568,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [569,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [570,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [571,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [572,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [573,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [574,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [575,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [576,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [577,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [578,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [579,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [580,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [581,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [582,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [583,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [584,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [585,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [586,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [587,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [588,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [589,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [590,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [591,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [592,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [593,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [594,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [595,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [596,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [597,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [598,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [599,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [600,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [601,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [602,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [603,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [604,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [605,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [606,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [607,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [608,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [609,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [610,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [611,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [612,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [613,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [614,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [615,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [616,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [617,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [618,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [619,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [620,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [621,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [622,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [623,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [624,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [625,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [626,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [627,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [628,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [629,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [630,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [631,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [632,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [633,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [634,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [635,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [636,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [637,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [638,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [639,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [640,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [641,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [642,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [643,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [644,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [645,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [646,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [647,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [648,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [649,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [650,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [651,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [652,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [653,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [654,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [655,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [656,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [657,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [658,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [659,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [660,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [661,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [662,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [663,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [664,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [665,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [666,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [667,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [668,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [669,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [670,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [671,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [672,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [673,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [674,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [675,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [676,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [677,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [678,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [679,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [680,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [681,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [682,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [683,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [684,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [685,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [686,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [687,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [688,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [689,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [690,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [691,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [692,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [693,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [694,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [695,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [696,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [697,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [698,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [699,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [700,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [701,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [702,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [703,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [704,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [705,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [706,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [707,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [708,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [709,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [710,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [711,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [712,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [713,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [714,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [715,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [716,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [717,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [718,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [719,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [720,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [721,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [722,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [723,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [724,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [725,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [726,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [727,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [728,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [729,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [730,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [731,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [732,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [733,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [734,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [735,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [736,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [737,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [738,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [739,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [740,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [741,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [742,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [743,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [744,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [745,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [746,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [747,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [748,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [749,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [750,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [751,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [752,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [753,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [754,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [755,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [756,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [757,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [758,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [759,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [760,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [761,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [762,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [763,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [764,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [765,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [766,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [767,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [768,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [769,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [770,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [771,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [772,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [773,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [774,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [775,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [776,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [777,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [778,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [779,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [780,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [781,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [782,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [783,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [784,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [785,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [786,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [787,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [788,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [789,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [790,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [791,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [792,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [793,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [794,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [795,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [796,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [797,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [798,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [799,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [800,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [801,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [802,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [803,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [804,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [805,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [806,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [807,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [808,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [809,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [810,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [811,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [812,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [813,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [814,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [815,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [816,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [817,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [818,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [819,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [820,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [821,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [822,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [823,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [824,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [825,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [826,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [827,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [828,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [829,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [830,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [831,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [832,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [833,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [834,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [835,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [836,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [837,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [838,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [839,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [840,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [841,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [842,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [843,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [844,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [845,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [846,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [847,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [848,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [849,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [850,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [851,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [852,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [853,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [854,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [855,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [856,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [857,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [858,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [859,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [860,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [861,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [862,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [863,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [864,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [865,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [866,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [867,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [868,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [869,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [870,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [871,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [872,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [873,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [874,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [875,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [876,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [877,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [878,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [879,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [880,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [881,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [882,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [883,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [884,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [885,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [886,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [887,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [888,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [889,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [890,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [891,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [892,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [893,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [894,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [895,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [896,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [897,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [898,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [899,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [900,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [901,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [902,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [903,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [904,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [905,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [906,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [907,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [908,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [909,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [910,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [911,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [912,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [913,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [914,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [915,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [916,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [917,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [918,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [919,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [920,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [921,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [922,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [923,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [924,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [925,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [926,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [927,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [928,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [929,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [930,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [931,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [932,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [933,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [934,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [935,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [936,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [937,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [938,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [939,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [940,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [941,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [942,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [943,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [944,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [945,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [946,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [947,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [948,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [949,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [950,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [951,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [952,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [953,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [954,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [955,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [956,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [957,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [958,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [959,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [960,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [961,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [962,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [963,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [964,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [965,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [966,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [967,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [968,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [969,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [970,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [971,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [972,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [973,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [974,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [975,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [976,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [977,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [978,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [979,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [980,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [981,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [982,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [983,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [984,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [985,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [986,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [987,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [988,]          FALSE              FALSE                  FALSE   FALSE FALSE
##   [989,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [990,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [991,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [992,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [993,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [994,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [995,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [996,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [997,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [998,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##   [999,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1000,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1001,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1002,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1003,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1004,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1005,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1006,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1007,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1008,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1009,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1010,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1011,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1012,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1013,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1014,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1015,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1016,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1017,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1018,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1019,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1020,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1021,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1022,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1023,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1024,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1025,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1026,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1027,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1028,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1029,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1030,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1031,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1032,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1033,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1034,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1035,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1036,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1037,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1038,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1039,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1040,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1041,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1042,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1043,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1044,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1045,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1046,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1047,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1048,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1049,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1050,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1051,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1052,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1053,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1054,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1055,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1056,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1057,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1058,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1059,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1060,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1061,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1062,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1063,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1064,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1065,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1066,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1067,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1068,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1069,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1070,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1071,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1072,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1073,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1074,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1075,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1076,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1077,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1078,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1079,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1080,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1081,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1082,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1083,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1084,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1085,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1086,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1087,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1088,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1089,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1090,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1091,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1092,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1093,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1094,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1095,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1096,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1097,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1098,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1099,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1100,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1101,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1102,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1103,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1104,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1105,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1106,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1107,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1108,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1109,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1110,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1111,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1112,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1113,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1114,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1115,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1116,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1117,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1118,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1119,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1120,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1121,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1122,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1123,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1124,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1125,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1126,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1127,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1128,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1129,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1130,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1131,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1132,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1133,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1134,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1135,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1136,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1137,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1138,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1139,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1140,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1141,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1142,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1143,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1144,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1145,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1146,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1147,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1148,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1149,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1150,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1151,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1152,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1153,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1154,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1155,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1156,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1157,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1158,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1159,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1160,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1161,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1162,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1163,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1164,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1165,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1166,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1167,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1168,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1169,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1170,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1171,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1172,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1173,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1174,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1175,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1176,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1177,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1178,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1179,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1180,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1181,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1182,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1183,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1184,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1185,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1186,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1187,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1188,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1189,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1190,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1191,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1192,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1193,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1194,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1195,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1196,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1197,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1198,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1199,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1200,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1201,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1202,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1203,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1204,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1205,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1206,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1207,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1208,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1209,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1210,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1211,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1212,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1213,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1214,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1215,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1216,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1217,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1218,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1219,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1220,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1221,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1222,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1223,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1224,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1225,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1226,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1227,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1228,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1229,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1230,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1231,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1232,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1233,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1234,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1235,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1236,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1237,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1238,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1239,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1240,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1241,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1242,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1243,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1244,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1245,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1246,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1247,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1248,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1249,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1250,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1251,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1252,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1253,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1254,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1255,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1256,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1257,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1258,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1259,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1260,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1261,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1262,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1263,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1264,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1265,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1266,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1267,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1268,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1269,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1270,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1271,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1272,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1273,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1274,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1275,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1276,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1277,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1278,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1279,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1280,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1281,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1282,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1283,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1284,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1285,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1286,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1287,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1288,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1289,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1290,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1291,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1292,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1293,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1294,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1295,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1296,]          FALSE              FALSE                  FALSE   FALSE FALSE
##  [1297,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1298,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1299,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1300,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1301,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1302,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1303,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1304,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1305,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1306,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1307,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1308,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1309,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1310,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1311,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1312,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1313,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1314,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1315,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1316,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1317,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1318,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1319,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1320,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1321,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1322,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1323,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1324,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1325,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1326,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1327,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1328,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1329,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1330,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1331,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1332,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1333,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1334,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1335,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1336,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1337,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1338,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1339,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1340,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1341,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1342,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1343,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1344,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1345,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1346,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1347,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1348,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1349,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1350,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1351,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1352,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1353,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1354,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1355,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1356,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1357,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1358,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1359,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1360,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1361,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1362,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1363,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1364,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1365,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1366,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1367,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1368,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1369,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1370,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1371,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1372,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1373,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1374,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1375,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1376,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1377,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1378,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1379,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1380,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1381,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1382,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1383,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1384,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1385,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1386,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1387,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1388,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1389,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1390,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1391,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1392,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1393,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1394,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1395,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1396,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1397,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1398,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1399,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1400,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1401,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1402,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1403,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1404,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1405,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1406,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1407,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##  [1408,]          FALSE              FALSE                  FALSE   FALSE  TRUE
##           1951  1952  1953  1954  1955  1956  1957  1958  1959  1960  1961
##     [1,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [2,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [3,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [4,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [5,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [6,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [7,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [8,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [9,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [10,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [11,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [12,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [13,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [14,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [15,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [16,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [17,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [18,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [19,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [20,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [21,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [22,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [23,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [24,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [25,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [26,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [27,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [28,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [29,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [30,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [31,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [32,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [33,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [34,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [35,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [36,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [37,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [38,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [39,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [40,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [41,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [42,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [43,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [44,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [45,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [46,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [47,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [48,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [49,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [50,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [51,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [52,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [53,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [54,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [55,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [56,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [57,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [58,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [59,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [60,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [61,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [62,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [63,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [64,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [65,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [66,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [67,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [68,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##    [69,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [70,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [71,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [72,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [73,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [74,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [75,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [76,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [77,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##    [78,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [79,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [80,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [81,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [82,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [83,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [84,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [85,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [86,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [87,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [88,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [89,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##    [90,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [91,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [92,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [93,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [94,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [95,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [96,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [97,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [98,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##    [99,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [102,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [103,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [106,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [107,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [109,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [112,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [114,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [119,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [121,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [124,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [135,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [137,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [139,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [140,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [144,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [147,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [148,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [149,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [151,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [152,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [153,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [154,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [155,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [158,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [161,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [162,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [163,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [164,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [169,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [171,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [172,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [174,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [175,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [181,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [183,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [185,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [186,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [194,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [196,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [197,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [201,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [202,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [203,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [205,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [207,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [208,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [211,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [213,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [214,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [221,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [222,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [224,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [225,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [230,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [231,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [232,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [233,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [235,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [236,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [240,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [242,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [245,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [246,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [247,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [252,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [253,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [255,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [262,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [263,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [264,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [266,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [274,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [276,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [277,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [281,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [284,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [289,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [290,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [292,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [294,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [295,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [299,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [302,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [303,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [307,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [309,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [310,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [311,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [316,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [318,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [338,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [341,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [348,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [350,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [353,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [355,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [356,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [360,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [362,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [364,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [365,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [367,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [368,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [374,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [381,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [383,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [393,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [399,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [402,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [403,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [405,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [409,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [410,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [411,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [412,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [413,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [414,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [415,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [416,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [417,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [418,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [419,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [420,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [421,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [422,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [423,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [424,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [425,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [426,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [427,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [428,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [429,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [430,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [431,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [432,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [433,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [434,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [435,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [436,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [437,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [438,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [439,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [440,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [441,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [442,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [443,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [444,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [445,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [446,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [447,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [448,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [449,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [450,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [451,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [452,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [453,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [454,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [455,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [456,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [457,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [458,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [459,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [460,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [461,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [462,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [463,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [464,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [465,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [466,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [467,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [468,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [469,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [470,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [471,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [472,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [473,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [474,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [475,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [476,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [477,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [478,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [479,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [480,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [481,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [482,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [483,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [484,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [485,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [486,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [487,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [488,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [489,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [490,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [491,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [492,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [493,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [494,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [495,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [496,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [497,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [498,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [499,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [500,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [501,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [502,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [503,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [504,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [505,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [506,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [507,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [508,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [509,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [510,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [511,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [512,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [513,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [514,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [515,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [516,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [517,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [518,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [519,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [520,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [521,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [522,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [523,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [524,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [525,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [526,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [527,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [528,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [529,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [530,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [531,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [532,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [533,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [534,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [535,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [536,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [537,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [538,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [539,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [540,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [541,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [542,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [543,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [544,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [545,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [546,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [547,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [548,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [549,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [550,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [551,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [552,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [553,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [554,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [555,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [556,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [557,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [558,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [559,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [560,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [561,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [562,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [563,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [564,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [565,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [566,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [567,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [568,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [569,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [570,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [571,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [572,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [573,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [574,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [575,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [576,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [577,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [578,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [579,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [580,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [581,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [582,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [583,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [584,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [585,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [586,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [587,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [588,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [589,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [590,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [591,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [592,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [593,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [594,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [595,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [596,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [597,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [598,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [599,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [600,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [601,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [602,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [603,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [604,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [605,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [606,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [607,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [608,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [609,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [610,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [611,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [612,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [613,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [614,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [615,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [616,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [617,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [618,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [619,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [620,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [621,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [622,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [623,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [624,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [625,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [626,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [627,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [628,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [629,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [630,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [631,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [632,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [633,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [634,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [635,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [636,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [637,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [638,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [639,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [640,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [641,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [642,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [643,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [644,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [645,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [646,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [647,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [648,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [649,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [650,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [651,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [652,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [653,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [654,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [655,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [656,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [657,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [658,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [659,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [660,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [661,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [662,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [663,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [664,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [665,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [666,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [667,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [668,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [669,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [670,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [671,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [672,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [673,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [674,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [675,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [676,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [677,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [678,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [679,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [680,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [681,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [682,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [683,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [684,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [685,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [686,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [687,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [688,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [689,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [690,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [691,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [692,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [693,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [694,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [695,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [696,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [697,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [698,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [699,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [700,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [701,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [702,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [703,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [704,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [705,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [706,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [707,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [708,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [709,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [710,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [711,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [712,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [713,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [714,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [715,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [716,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [717,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [718,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [719,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [720,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [721,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [722,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [723,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [724,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [725,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [726,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [727,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [728,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [729,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [730,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [731,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [732,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [733,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [734,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [735,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [736,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [737,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [738,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [739,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [740,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [741,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [742,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [743,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [744,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [745,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [746,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [747,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [748,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [749,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [750,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [751,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [752,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [753,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [754,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [755,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [756,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [757,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [758,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [759,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [760,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [761,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [762,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [763,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [764,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [765,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [766,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [767,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [768,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [769,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [770,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [771,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [772,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [773,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [774,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [775,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [776,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [777,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [778,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [779,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [780,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [781,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [782,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [783,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [784,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [785,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [786,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [787,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [788,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [789,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [790,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [791,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [792,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [793,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [794,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [795,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [796,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [797,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [798,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [799,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [800,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [801,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [802,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [803,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [804,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [805,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [806,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [807,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [808,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [809,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [810,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [811,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [812,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [813,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [814,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [815,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [816,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [817,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [818,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [819,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [820,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [821,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [822,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [823,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [824,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [825,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [826,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [827,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [828,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [829,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [830,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [831,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [832,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [833,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [834,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [835,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [836,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [837,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [838,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [839,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [840,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [841,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [842,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [843,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [844,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [845,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [846,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [847,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [848,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [849,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [850,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [851,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [852,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [853,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [854,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [855,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [856,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [857,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [858,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [859,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [860,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [861,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [862,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [863,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [864,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [865,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [866,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [867,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [868,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [869,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [870,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [871,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [872,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [873,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [874,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [875,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [876,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [877,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [878,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [879,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [880,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [881,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [882,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [883,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [884,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [885,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [886,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [887,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [888,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [889,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [890,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [891,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [892,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [893,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [894,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [895,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [896,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [897,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [898,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [899,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [900,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [901,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [902,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [903,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [904,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [905,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [906,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [907,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [908,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [909,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [910,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [911,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [912,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [913,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [914,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [915,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [916,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [917,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [918,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [919,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [920,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [921,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [922,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [923,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [924,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [925,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [926,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [927,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [928,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [929,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [930,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [931,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [932,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [933,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [934,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [935,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [936,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [937,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [938,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [939,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [940,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [941,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [942,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [943,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [944,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [945,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [946,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [947,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [948,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [949,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [950,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [951,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [952,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [953,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [954,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [955,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [956,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [957,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [958,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [959,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [960,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [961,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [962,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [963,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [964,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [965,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [966,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [967,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [968,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [969,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [970,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [971,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [972,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [973,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [974,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [975,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [976,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [977,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [978,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [979,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [980,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [981,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [982,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [983,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [984,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [985,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [986,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [987,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [988,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [989,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [990,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [991,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [992,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [993,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [994,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [995,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [996,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [997,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [998,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [999,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1000,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1001,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1002,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1003,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1004,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1005,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1006,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1007,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1008,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1009,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1010,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1011,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1012,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1013,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1014,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1015,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1016,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1017,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1018,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1019,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1020,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1021,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1022,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1023,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1024,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1025,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1026,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1027,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1028,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1029,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1030,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1031,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1032,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1033,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1034,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1035,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1036,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1037,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1038,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1039,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1040,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1041,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1042,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1043,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1044,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1045,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1046,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1047,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1048,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1049,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1050,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1051,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1052,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1053,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1054,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1055,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1056,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1057,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1058,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1059,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1060,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1061,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1062,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1063,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1064,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1065,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1066,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1067,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1068,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1069,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1070,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1071,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1072,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1073,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1074,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1075,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1076,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1077,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1078,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1079,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1080,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1081,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1082,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1083,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1084,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1085,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1086,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1087,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1088,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1089,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1090,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1091,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1092,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1093,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1094,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1095,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1096,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1097,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1098,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1099,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1102,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1103,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1106,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1107,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1109,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1112,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1114,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1119,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1121,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1123,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1124,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1134,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1137,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1139,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1140,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1144,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1147,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1148,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1149,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1151,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1152,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1154,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1158,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1161,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1162,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1163,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1164,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1169,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1171,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1174,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1175,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1176,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1179,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1181,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1183,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1184,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1185,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1194,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1196,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1197,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1199,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1202,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1203,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1205,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1207,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
##  [1208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1213,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1214,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1217,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1221,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1222,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1224,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1225,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1227,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1229,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1230,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1231,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1233,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1235,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1236,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1246,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1252,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1253,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1260,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1266,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1274,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1276,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1277,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1281,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1284,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1286,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1287,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1289,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1290,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1291,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1292,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1293,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1295,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1299,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1302,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1303,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1307,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1309,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1310,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1311,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1316,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1318,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1319,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1338,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1341,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1348,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1350,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1353,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1355,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1356,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1360,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1362,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1364,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1365,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1367,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1368,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1372,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1374,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1377,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1381,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1383,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1393,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1398,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1399,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1401,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1402,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1403,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1405,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##           1962  1963  1964  1965  1966  1967  1968  1969  1970  1971  1972
##     [1,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [2,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [3,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [4,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [5,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [6,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [7,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [8,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [9,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [10,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [11,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [12,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [13,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [14,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [15,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [16,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [17,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [18,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [19,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [20,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [21,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [22,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [23,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [24,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [25,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [26,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [27,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [28,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [29,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [30,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [31,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [32,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [33,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [34,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [35,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [36,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [37,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [38,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [39,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [40,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [41,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [42,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [43,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [44,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [45,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [46,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [47,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [48,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [49,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [50,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [51,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [52,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [53,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [54,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [55,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [56,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [57,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [58,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [59,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [60,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [61,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [62,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [63,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [64,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [65,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [66,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [67,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [68,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [69,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [70,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [71,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [72,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [73,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [74,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [75,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [76,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [77,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [78,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [79,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##    [80,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [81,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [82,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [83,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [84,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [85,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [86,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [87,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [88,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [89,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [90,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [91,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [92,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [93,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [94,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [95,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [96,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [97,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [98,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [99,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [102,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [103,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE
##   [104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [106,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [107,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##   [108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [109,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [112,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [114,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [119,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [121,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [124,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [135,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [137,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [139,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [140,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [144,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [147,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [148,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [149,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [151,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [152,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [153,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [154,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [155,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [158,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [161,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [162,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [163,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [164,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [169,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [170,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [171,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [172,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [174,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [175,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [180,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [181,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [183,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [185,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [196,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [197,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [201,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [202,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [203,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [205,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [207,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [213,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [214,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [218,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [221,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [222,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [224,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [225,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [230,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [231,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [232,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [233,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [235,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [236,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [240,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [242,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [245,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [246,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [247,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [252,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [253,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [262,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [263,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [264,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [266,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [274,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [276,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [277,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [281,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [284,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [289,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [290,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [292,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [295,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE
##   [296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [299,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [300,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [302,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [303,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [307,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [309,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [310,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [311,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [316,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [318,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [320,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [321,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [326,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [338,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [341,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [348,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [350,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [352,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [353,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [355,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [356,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [360,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [362,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [364,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [365,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [367,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [368,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [374,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [378,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [381,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [383,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [393,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [399,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [402,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [403,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE
##   [405,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [409,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [410,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [411,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [412,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [413,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [414,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [415,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [416,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [417,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [418,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [419,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [420,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [421,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [422,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [423,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [424,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [425,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [426,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [427,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [428,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [429,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [430,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [431,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [432,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [433,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [434,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [435,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [436,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [437,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [438,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [439,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [440,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [441,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [442,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [443,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [444,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [445,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [446,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [447,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [448,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [449,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [450,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [451,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [452,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [453,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [454,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [455,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [456,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [457,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [458,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [459,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [460,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [461,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [462,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [463,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [464,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [465,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [466,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [467,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [468,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [469,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [470,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [471,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [472,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [473,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [474,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [475,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [476,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [477,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [478,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [479,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [480,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [481,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [482,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [483,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [484,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [485,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [486,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [487,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [488,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [489,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [490,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [491,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [492,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [493,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [494,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [495,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [496,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [497,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [498,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [499,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [500,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [501,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [502,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [503,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [504,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [505,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [506,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [507,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [508,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [509,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [510,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [511,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [512,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [513,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [514,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [515,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [516,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [517,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [518,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [519,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [520,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [521,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [522,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [523,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [524,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [525,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [526,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [527,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [528,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [529,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [530,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [531,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [532,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [533,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [534,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [535,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [536,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [537,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [538,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [539,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [540,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [541,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [542,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [543,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [544,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [545,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [546,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [547,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [548,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [549,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [550,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [551,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [552,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [553,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [554,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [555,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [556,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [557,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [558,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [559,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [560,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [561,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [562,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [563,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [564,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [565,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [566,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [567,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [568,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [569,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [570,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [571,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [572,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [573,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [574,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [575,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [576,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [577,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [578,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [579,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [580,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [581,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [582,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [583,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [584,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [585,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [586,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [587,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [588,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [589,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [590,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [591,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [592,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [593,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [594,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [595,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [596,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [597,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [598,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [599,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [600,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [601,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [602,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [603,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [604,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [605,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [606,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [607,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [608,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [609,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [610,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [611,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [612,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [613,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [614,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [615,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [616,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [617,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [618,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [619,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [620,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [621,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [622,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [623,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [624,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [625,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [626,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [627,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [628,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [629,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [630,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [631,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [632,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [633,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [634,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [635,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [636,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [637,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [638,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [639,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [640,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [641,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [642,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [643,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [644,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [645,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [646,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [647,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [648,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [649,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [650,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [651,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [652,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [653,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [654,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [655,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [656,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [657,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [658,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [659,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [660,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [661,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [662,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [663,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [664,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [665,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [666,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [667,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [668,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [669,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [670,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [671,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [672,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [673,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [674,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [675,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [676,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [677,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [678,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [679,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [680,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [681,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [682,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [683,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [684,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [685,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [686,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [687,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [688,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [689,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [690,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [691,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [692,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [693,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [694,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [695,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [696,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [697,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [698,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [699,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [700,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [701,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [702,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [703,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [704,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [705,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [706,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [707,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [708,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [709,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [710,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [711,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [712,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [713,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [714,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [715,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [716,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [717,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [718,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [719,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [720,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [721,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [722,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [723,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [724,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [725,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [726,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [727,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [728,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [729,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [730,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [731,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [732,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [733,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [734,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [735,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [736,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [737,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [738,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [739,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [740,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [741,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [742,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [743,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [744,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [745,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [746,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [747,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [748,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [749,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [750,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [751,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [752,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [753,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [754,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [755,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [756,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [757,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [758,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [759,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [760,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [761,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [762,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [763,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [764,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [765,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [766,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [767,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [768,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [769,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [770,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [771,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [772,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [773,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [774,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [775,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [776,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [777,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [778,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [779,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [780,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [781,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [782,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [783,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [784,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [785,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [786,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [787,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [788,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [789,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [790,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [791,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [792,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [793,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [794,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [795,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [796,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [797,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [798,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [799,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [800,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [801,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [802,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [803,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [804,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [805,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [806,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [807,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [808,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [809,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [810,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [811,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [812,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [813,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [814,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [815,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [816,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [817,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [818,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [819,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [820,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [821,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [822,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [823,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [824,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [825,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [826,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [827,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [828,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [829,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [830,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [831,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [832,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [833,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [834,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [835,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [836,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [837,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [838,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [839,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [840,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [841,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [842,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [843,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [844,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [845,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [846,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [847,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [848,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [849,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [850,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [851,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [852,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [853,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [854,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [855,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [856,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [857,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [858,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [859,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [860,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [861,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [862,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [863,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [864,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [865,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [866,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [867,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [868,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [869,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [870,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [871,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [872,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [873,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [874,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [875,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [876,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [877,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [878,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [879,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [880,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [881,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [882,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [883,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [884,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [885,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [886,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [887,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [888,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [889,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [890,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [891,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [892,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [893,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [894,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [895,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [896,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [897,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [898,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [899,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [900,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [901,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [902,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [903,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [904,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [905,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [906,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [907,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [908,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [909,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [910,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [911,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [912,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [913,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [914,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [915,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [916,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [917,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [918,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [919,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [920,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [921,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [922,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [923,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [924,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [925,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [926,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [927,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [928,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [929,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [930,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [931,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [932,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [933,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [934,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [935,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [936,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [937,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [938,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [939,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [940,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [941,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [942,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [943,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [944,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [945,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [946,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [947,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [948,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [949,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [950,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [951,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [952,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [953,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [954,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [955,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [956,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [957,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [958,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [959,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [960,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [961,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [962,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [963,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [964,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [965,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [966,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [967,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [968,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [969,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [970,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [971,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [972,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [973,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [974,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [975,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [976,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [977,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [978,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [979,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [980,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [981,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [982,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [983,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [984,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [985,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [986,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [987,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [988,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [989,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [990,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [991,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [992,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [993,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [994,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [995,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [996,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [997,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [998,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [999,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1000,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1001,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1002,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1003,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1004,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1005,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1006,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1007,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1008,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1009,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1010,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1011,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1012,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1013,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1014,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1015,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1016,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1017,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1018,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1019,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1020,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1021,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1022,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1023,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1024,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1025,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1026,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1027,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1028,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1029,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1030,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1031,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1032,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1033,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1034,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1035,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1036,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1037,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1038,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1039,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1040,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1041,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1042,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1043,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1044,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1045,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1046,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1047,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1048,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1049,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1050,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1051,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1052,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1053,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1054,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1055,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1056,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1057,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1058,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1059,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1060,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1061,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1062,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1063,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1064,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1065,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1066,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1067,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1068,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1069,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1070,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1071,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1072,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1073,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1074,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1075,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1076,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1077,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1078,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1079,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1080,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1081,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1082,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1083,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1084,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1085,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1086,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1087,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1088,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1089,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1090,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1091,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1092,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1093,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1094,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1095,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1096,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1097,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1098,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1099,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1102,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1103,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1106,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1107,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1109,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1112,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1114,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1119,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1121,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1123,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1124,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1134,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1139,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1140,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1144,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE
##  [1145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1147,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1151,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1152,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1154,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1158,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1161,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1162,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1163,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1164,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1169,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1171,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1174,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1175,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1179,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1181,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1183,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1184,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1185,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1196,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1197,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1198,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1202,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1203,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1205,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1207,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1213,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1214,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1217,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1221,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1222,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1224,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1225,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1227,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1228,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1230,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1231,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1233,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1235,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1236,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1246,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1252,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1253,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1260,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1266,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1274,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1276,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1277,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1281,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1284,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1286,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1287,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1289,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1290,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1291,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1292,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1293,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1295,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1299,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1302,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1303,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1307,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1309,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1310,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##  [1311,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##  [1313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1316,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1318,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1319,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1320,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1334,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1338,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1341,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE
##  [1344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1348,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1350,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1353,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1355,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1356,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1360,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1362,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1364,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1365,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1367,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1368,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1372,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1374,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1377,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1381,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1383,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1393,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1398,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1399,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1401,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1402,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1403,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1405,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##           1973  1974  1975  1976  1977  1978  1979  1980  1981  1982  1983
##     [1,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [2,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [3,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [4,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [5,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [6,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [7,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##     [8,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [9,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [10,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [11,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [12,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [13,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [14,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [15,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [16,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [17,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [18,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [19,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [20,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [21,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [22,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##    [23,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [24,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##    [25,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [26,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [27,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [28,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [29,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [30,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [31,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [32,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [33,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [34,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [35,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [36,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [37,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [38,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [39,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [40,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [41,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [42,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [43,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [44,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [45,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [46,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [47,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [48,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##    [49,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [50,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [51,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##    [52,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##    [53,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [54,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [55,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [56,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [57,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [58,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [59,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [60,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [61,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [62,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [63,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [64,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##    [65,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [66,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [67,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [68,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [69,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [70,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [71,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [72,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [73,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [74,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [75,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [76,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [77,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [78,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [79,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [80,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [81,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [82,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [83,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [84,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [85,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [86,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [87,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [88,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [89,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [90,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [91,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [92,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [93,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [94,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [95,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [96,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [97,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [98,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [99,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [101,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [102,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [103,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [106,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [107,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [109,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [112,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [114,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [119,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [121,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [135,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [137,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [139,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [140,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [144,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [147,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [148,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [149,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [151,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [152,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [153,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [154,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [156,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [158,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [161,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [162,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [163,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [164,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [167,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [169,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [170,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [171,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [173,] FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [174,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [175,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [176,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [178,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [180,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [181,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [183,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [185,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [188,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [190,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [193,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [194,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [195,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [196,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [197,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [201,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [202,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [203,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [204,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [205,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [207,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [211,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [212,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [213,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [214,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [217,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [218,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [220,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [221,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [222,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [224,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [225,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [226,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [227,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [228,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [230,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [231,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [232,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [233,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [235,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [236,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [238,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [241,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [242,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [245,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [246,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [248,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [249,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [252,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [253,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [262,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [263,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [264,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [266,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [274,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [276,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [277,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [281,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [284,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [289,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [290,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [292,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [295,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [298,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [299,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [300,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [302,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [303,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [307,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [309,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [310,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [311,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [316,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [318,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##   [319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [320,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE
##   [321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [326,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [331,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [336,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [338,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [341,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [348,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [350,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [352,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [353,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [355,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [356,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [357,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [360,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [362,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [364,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [365,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [367,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [368,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [374,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [378,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [381,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [383,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [384,] FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [391,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [393,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [399,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE  TRUE
##   [400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [402,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [403,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [405,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [409,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE
##   [410,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [411,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [412,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [413,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [414,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [415,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [416,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [417,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [418,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [419,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [420,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [421,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [422,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [423,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [424,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [425,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [426,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [427,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [428,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [429,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [430,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [431,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [432,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [433,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [434,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [435,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [436,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [437,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [438,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [439,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [440,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [441,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [442,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [443,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [444,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [445,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [446,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [447,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [448,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [449,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [450,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [451,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [452,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [453,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [454,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [455,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [456,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [457,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [458,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [459,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [460,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [461,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [462,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [463,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [464,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [465,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [466,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [467,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [468,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [469,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [470,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [471,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [472,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [473,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [474,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [475,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [476,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [477,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [478,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [479,] FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [480,] FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [481,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [482,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [483,] FALSE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [484,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [485,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [486,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [487,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [488,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [489,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [490,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [491,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [492,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [493,] FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [494,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [495,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [496,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [497,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [498,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [499,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [500,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [501,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [502,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [503,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [504,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [505,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [506,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [507,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [508,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [509,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [510,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [511,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [512,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [513,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [514,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [515,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [516,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [517,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [518,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [519,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [520,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [521,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [522,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [523,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [524,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [525,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [526,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [527,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [528,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [529,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [530,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [531,] FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [532,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [533,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [534,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [535,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [536,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [537,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [538,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [539,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [540,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [541,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [542,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [543,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [544,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [545,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [546,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [547,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [548,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [549,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [550,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [551,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [552,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [553,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [554,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [555,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [556,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [557,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [558,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [559,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [560,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [561,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [562,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [563,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [564,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [565,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [566,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [567,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [568,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [569,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [570,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [571,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [572,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [573,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [574,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [575,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [576,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [577,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [578,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [579,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [580,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [581,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [582,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [583,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [584,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [585,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [586,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [587,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [588,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [589,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [590,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [591,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [592,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [593,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [594,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [595,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [596,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [597,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [598,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [599,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [600,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [601,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [602,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [603,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [604,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [605,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [606,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [607,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [608,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [609,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [610,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [611,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [612,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [613,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [614,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [615,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [616,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [617,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [618,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [619,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [620,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [621,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [622,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [623,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [624,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [625,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [626,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [627,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [628,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [629,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [630,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [631,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [632,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [633,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [634,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [635,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [636,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [637,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [638,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [639,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [640,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [641,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [642,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [643,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [644,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [645,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [646,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [647,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [648,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [649,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [650,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [651,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [652,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [653,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [654,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [655,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [656,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [657,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [658,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [659,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [660,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [661,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [662,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [663,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [664,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [665,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [666,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [667,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [668,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [669,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [670,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [671,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [672,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [673,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [674,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [675,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [676,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [677,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [678,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [679,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [680,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [681,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [682,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [683,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [684,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [685,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [686,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [687,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [688,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [689,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [690,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [691,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [692,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [693,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [694,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [695,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [696,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [697,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [698,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [699,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [700,] FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [701,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [702,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [703,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [704,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [705,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [706,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [707,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [708,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [709,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [710,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [711,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [712,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [713,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [714,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [715,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [716,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [717,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [718,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [719,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [720,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [721,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [722,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [723,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [724,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [725,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [726,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [727,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [728,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [729,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [730,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [731,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [732,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [733,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [734,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [735,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [736,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [737,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [738,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [739,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [740,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [741,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [742,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [743,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [744,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [745,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [746,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [747,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [748,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [749,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [750,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [751,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [752,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [753,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [754,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [755,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [756,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [757,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [758,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [759,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [760,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [761,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [762,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [763,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE
##   [764,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [765,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [766,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [767,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [768,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [769,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [770,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [771,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [772,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [773,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [774,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [775,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [776,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [777,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [778,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [779,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [780,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [781,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [782,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [783,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [784,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [785,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [786,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [787,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [788,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [789,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [790,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [791,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [792,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [793,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [794,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [795,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [796,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [797,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [798,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [799,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [800,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [801,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [802,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [803,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [804,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [805,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [806,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [807,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [808,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [809,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [810,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [811,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [812,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [813,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [814,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [815,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [816,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [817,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [818,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [819,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [820,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [821,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [822,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [823,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [824,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [825,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [826,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [827,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [828,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [829,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [830,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [831,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [832,] FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [833,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [834,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [835,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [836,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [837,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [838,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [839,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [840,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [841,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [842,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [843,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [844,] FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE
##   [845,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [846,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [847,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [848,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [849,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [850,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [851,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [852,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [853,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [854,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [855,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [856,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [857,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [858,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [859,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [860,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [861,]  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [862,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [863,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [864,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [865,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [866,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [867,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [868,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [869,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [870,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [871,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [872,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [873,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [874,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [875,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [876,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [877,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [878,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [879,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [880,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [881,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [882,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [883,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [884,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [885,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [886,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [887,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [888,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [889,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [890,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [891,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [892,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [893,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [894,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [895,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [896,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [897,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [898,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [899,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [900,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [901,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [902,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [903,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [904,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [905,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [906,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [907,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [908,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [909,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [910,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [911,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [912,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [913,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [914,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [915,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [916,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [917,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [918,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [919,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [920,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [921,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [922,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [923,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [924,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [925,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [926,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [927,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [928,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [929,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [930,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [931,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [932,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [933,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [934,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [935,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [936,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [937,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [938,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [939,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [940,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [941,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [942,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [943,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [944,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [945,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [946,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [947,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [948,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [949,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [950,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [951,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [952,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [953,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [954,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [955,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [956,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [957,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [958,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [959,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [960,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [961,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [962,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [963,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [964,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [965,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [966,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [967,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [968,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [969,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [970,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [971,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [972,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [973,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [974,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [975,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [976,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [977,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [978,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [979,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [980,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [981,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [982,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [983,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [984,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [985,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [986,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [987,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [988,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [989,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [990,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [991,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [992,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [993,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [994,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [995,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [996,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [997,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [998,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [999,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1000,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1001,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1002,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1003,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1004,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1005,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1006,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1007,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1008,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1009,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1010,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1011,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1012,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1013,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1014,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1015,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1016,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1017,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1018,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1019,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1020,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1021,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1022,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1023,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1024,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1025,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1026,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1027,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1028,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1029,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1030,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1031,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1032,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1033,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1034,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1035,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1036,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1037,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1038,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1039,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1040,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1041,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1042,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1043,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1044,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1045,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1046,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1047,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1048,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1049,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1050,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1051,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1052,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1053,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE
##  [1054,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1055,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1056,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1057,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1058,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1059,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1060,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1061,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1062,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1063,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1064,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1065,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1066,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1067,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1068,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1069,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1070,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1071,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1072,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1073,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1074,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1075,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1076,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1077,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1078,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1079,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1080,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1081,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1082,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1083,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1084,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1085,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1086,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1087,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1088,]  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1089,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1090,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1091,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1092,]  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE
##  [1093,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1094,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1095,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1096,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1097,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1098,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1099,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1102,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1103,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1104,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1106,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1107,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1109,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1112,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1113,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1114,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE
##  [1115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1119,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1120,]  TRUE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE
##  [1121,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1123,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1124,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1125,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1126,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE
##  [1127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1132,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1134,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1139,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1140,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1143,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1144,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1147,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1151,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1152,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1154,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1161,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1162,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1163,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1164,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1169,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1171,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1174,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1175,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1179,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1181,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1183,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1184,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1185,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1196,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1197,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1198,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1202,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1203,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1205,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1206,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1207,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1213,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1214,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1217,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1221,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1222,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1224,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1225,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1227,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1228,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1230,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1231,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1233,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1235,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1236,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1246,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1252,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1253,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1259,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1260,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1261,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1266,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1269,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1274,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1276,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1277,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1281,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1284,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1286,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1287,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1289,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1290,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1291,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1292,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1293,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1295,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1299,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1301,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1302,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1303,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1305,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1307,]  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1309,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1310,] FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1311,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##  [1312,] FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1313,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##  [1314,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1315,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1316,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1317,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1318,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##  [1319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1321,]  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1322,] FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1323,]  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##  [1324,] FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1325,]  TRUE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE
##  [1326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1329,]  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##  [1330,]  TRUE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1331,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1332,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1333,]  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1334,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1338,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##  [1339,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1340,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1341,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1343,]  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1345,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1346,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1348,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1350,]  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##  [1351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1353,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1354,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1355,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1356,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1357,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##  [1358,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1360,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1361,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE
##  [1362,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1364,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1365,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1367,]  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1368,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE
##  [1369,]  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1374,]  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##  [1375,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1376,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1377,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE
##  [1379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1381,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1383,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1388,]  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1389,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##  [1392,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1393,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1394,] FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1396,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1397,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE
##  [1399,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1400,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1402,] FALSE FALSE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1403,] FALSE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1404,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1405,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##  [1408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##           1984  1985  1986  1987  1988  1989  1990  1991  1992  1993  1994
##     [1,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [2,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [3,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [4,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [5,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [6,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [7,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [8,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [9,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [10,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [11,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [12,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [13,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [14,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [15,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [16,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [17,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [18,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [19,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [20,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [21,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [22,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [23,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [24,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [25,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [26,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [27,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [28,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [29,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [30,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [31,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [32,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [33,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [34,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [35,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [36,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [37,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [38,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [39,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [40,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [41,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [42,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [43,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [44,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [45,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [46,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [47,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [48,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [49,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [50,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [51,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [52,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [53,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [54,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [55,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [56,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [57,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [58,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [59,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [60,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [61,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [62,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [63,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [64,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [65,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [66,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [67,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [68,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [69,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [70,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [71,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [72,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [73,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [74,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [75,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [76,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [77,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [78,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [79,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [80,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [81,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [82,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [83,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [84,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [85,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [86,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [87,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [88,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [89,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [90,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [91,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [92,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [93,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [94,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [95,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [96,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [97,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [98,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [99,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [101,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [102,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [103,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [106,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [107,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [109,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [112,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [113,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [114,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [119,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [121,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [127,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [129,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [131,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [135,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [137,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [139,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [140,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [144,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [147,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [149,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [151,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [152,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [153,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [154,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [156,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [161,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [162,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [163,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [164,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [167,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [168,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [169,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [171,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [172,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [173,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [174,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [175,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [177,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [180,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [181,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [183,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [185,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [191,] FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE
##   [192,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [194,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [196,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [197,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [198,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [201,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [202,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [203,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [205,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [206,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [207,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [213,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [214,]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [219,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [221,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [222,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [224,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [225,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [226,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [230,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [231,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [233,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [235,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [236,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [237,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [240,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [242,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [245,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [246,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [248,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [249,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [252,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [253,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [262,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [263,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [264,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [266,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [268,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [274,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [276,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [277,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [281,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [284,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [289,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [290,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [292,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [295,]  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [298,]  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [299,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [300,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [302,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [303,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [307,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [309,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [310,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [311,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [316,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [318,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [320,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [326,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [331,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [336,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##   [337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [338,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [341,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [348,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [350,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [353,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [355,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [356,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [357,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [360,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [362,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [364,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [365,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [367,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [368,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [374,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [375,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [378,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [381,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [383,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [384,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [391,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [392,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [393,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [399,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [402,] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [403,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [405,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [409,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [410,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [411,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [412,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [413,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [414,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [415,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [416,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [417,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [418,] FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [419,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [420,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [421,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [422,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [423,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [424,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [425,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [426,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [427,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [428,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [429,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [430,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [431,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [432,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [433,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [434,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [435,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [436,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [437,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [438,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [439,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [440,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [441,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [442,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [443,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [444,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [445,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [446,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [447,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [448,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [449,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [450,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [451,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [452,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [453,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [454,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [455,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [456,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [457,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [458,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [459,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [460,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [461,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [462,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [463,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [464,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [465,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [466,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [467,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [468,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [469,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [470,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [471,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [472,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [473,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [474,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [475,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [476,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [477,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [478,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [479,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [480,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [481,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [482,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [483,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [484,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [485,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [486,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [487,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [488,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [489,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [490,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [491,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [492,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [493,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [494,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [495,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [496,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [497,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [498,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [499,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [500,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [501,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [502,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [503,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [504,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [505,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [506,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [507,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [508,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [509,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [510,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [511,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [512,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [513,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [514,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [515,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [516,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [517,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [518,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [519,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [520,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [521,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [522,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [523,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [524,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [525,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [526,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [527,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [528,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [529,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [530,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [531,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [532,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [533,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [534,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [535,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [536,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [537,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [538,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [539,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [540,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE
##   [541,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [542,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [543,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [544,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [545,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [546,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [547,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [548,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [549,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [550,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [551,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [552,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [553,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [554,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [555,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [556,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [557,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [558,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [559,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [560,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [561,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [562,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [563,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [564,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [565,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [566,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [567,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [568,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [569,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [570,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [571,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [572,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [573,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [574,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [575,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [576,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [577,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [578,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [579,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [580,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [581,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [582,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [583,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [584,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [585,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [586,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [587,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [588,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [589,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [590,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [591,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [592,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [593,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [594,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [595,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [596,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [597,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [598,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [599,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [600,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [601,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [602,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [603,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [604,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [605,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [606,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [607,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [608,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [609,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [610,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [611,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [612,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [613,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [614,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [615,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [616,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [617,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [618,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [619,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [620,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [621,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [622,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [623,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [624,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [625,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [626,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [627,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [628,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [629,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [630,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [631,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [632,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [633,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [634,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [635,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [636,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [637,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [638,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [639,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [640,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [641,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [642,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [643,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [644,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [645,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [646,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [647,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [648,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [649,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [650,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [651,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [652,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [653,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [654,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [655,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [656,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [657,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [658,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [659,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [660,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [661,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [662,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [663,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [664,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [665,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [666,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [667,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [668,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [669,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [670,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [671,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [672,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [673,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [674,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [675,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [676,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [677,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [678,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [679,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [680,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [681,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [682,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [683,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [684,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [685,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##   [686,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [687,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [688,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [689,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##   [690,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [691,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [692,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [693,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [694,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [695,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [696,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [697,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [698,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [699,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [700,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [701,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [702,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [703,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [704,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [705,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [706,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [707,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [708,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [709,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [710,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [711,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [712,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [713,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [714,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [715,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [716,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [717,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [718,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [719,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [720,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [721,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [722,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [723,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [724,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [725,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [726,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [727,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [728,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [729,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [730,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [731,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [732,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [733,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [734,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [735,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [736,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [737,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [738,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [739,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [740,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [741,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [742,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [743,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [744,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [745,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [746,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [747,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [748,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [749,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [750,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [751,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [752,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [753,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [754,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [755,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [756,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [757,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [758,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [759,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [760,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [761,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [762,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [763,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [764,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [765,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [766,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [767,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [768,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [769,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [770,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [771,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [772,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [773,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [774,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [775,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [776,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [777,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [778,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [779,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [780,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [781,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [782,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [783,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [784,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [785,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [786,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [787,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [788,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [789,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [790,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [791,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [792,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [793,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [794,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [795,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [796,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [797,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [798,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [799,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [800,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [801,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [802,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [803,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [804,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [805,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [806,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [807,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [808,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [809,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [810,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [811,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [812,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [813,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [814,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [815,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [816,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [817,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [818,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [819,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [820,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [821,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [822,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [823,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [824,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [825,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [826,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [827,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [828,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [829,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [830,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [831,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [832,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [833,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [834,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [835,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [836,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [837,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [838,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [839,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [840,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [841,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [842,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [843,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [844,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [845,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [846,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [847,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [848,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [849,]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [850,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [851,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [852,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [853,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [854,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [855,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [856,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [857,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [858,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [859,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [860,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [861,]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [862,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [863,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [864,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [865,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [866,]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [867,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [868,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [869,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [870,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [871,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [872,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [873,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [874,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [875,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [876,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [877,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [878,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [879,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [880,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [881,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [882,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [883,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [884,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [885,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [886,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [887,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [888,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [889,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [890,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [891,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [892,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [893,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [894,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [895,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [896,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [897,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [898,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [899,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [900,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [901,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [902,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [903,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [904,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [905,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [906,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [907,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [908,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [909,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [910,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [911,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [912,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [913,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [914,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [915,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [916,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [917,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [918,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [919,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [920,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [921,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [922,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [923,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [924,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [925,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [926,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [927,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [928,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [929,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [930,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [931,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [932,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [933,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [934,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [935,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [936,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [937,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [938,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [939,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [940,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [941,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [942,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [943,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [944,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [945,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [946,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [947,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [948,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [949,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [950,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [951,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [952,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [953,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [954,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [955,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [956,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [957,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [958,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [959,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [960,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [961,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [962,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [963,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [964,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [965,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [966,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [967,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [968,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [969,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [970,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [971,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [972,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [973,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [974,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [975,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [976,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [977,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [978,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [979,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [980,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [981,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [982,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [983,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [984,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [985,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [986,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [987,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [988,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [989,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [990,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [991,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [992,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [993,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [994,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [995,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [996,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [997,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [998,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [999,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1000,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1001,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1002,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1003,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1004,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1005,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1006,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1007,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1008,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1009,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1010,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1011,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1012,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1013,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1014,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1015,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1016,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1017,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1018,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1019,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1020,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1021,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1022,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1023,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1024,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1025,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1026,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1027,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1028,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1029,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1030,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1031,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1032,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1033,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1034,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1035,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1036,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1037,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1038,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1039,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1040,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1041,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1042,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1043,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1044,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1045,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1046,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1047,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1048,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1049,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1050,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1051,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1052,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1053,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1054,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1055,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1056,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1057,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1058,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1059,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1060,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1061,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1062,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1063,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1064,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1065,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1066,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1067,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1068,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1069,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1070,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1071,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1072,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1073,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1074,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1075,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1076,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1077,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1078,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1079,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1080,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1081,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1082,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1083,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1084,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1085,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1086,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1087,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1088,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1089,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1090,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1091,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1092,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1093,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1094,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1095,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1096,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1097,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1098,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1099,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1102,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1103,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1104,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1106,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1107,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1109,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1111,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1112,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1114,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1115,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1119,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1121,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1132,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1133,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1138,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1139,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1140,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1143,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1144,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1147,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1150,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1151,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1152,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1154,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1157,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1161,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1162,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1163,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1164,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1165,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1169,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1171,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1174,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1175,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1179,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1181,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1182,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1183,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1184,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1185,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1188,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1196,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1197,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1202,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1203,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1205,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1207,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1209,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1213,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1214,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1217,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1221,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1222,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1224,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1225,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1227,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1228,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1229,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1230,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1231,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1233,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1235,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1236,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1237,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##  [1238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1244,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1246,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1252,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1253,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1259,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1261,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1266,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1269,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1274,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1276,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1277,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1281,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1284,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1285,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1286,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1287,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1288,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1289,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1290,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1291,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1292,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1295,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1299,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1302,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1303,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1304,] FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1305,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE
##  [1306,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1307,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1308,]  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1309,] FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##  [1310,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1311,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1316,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1317,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##  [1318,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1319,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1323,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1326,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1330,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1334,] FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1336,] FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1337,] FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1338,] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1339,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1341,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1344,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##  [1346,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1347,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1348,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1349,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1350,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1353,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1355,] FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1356,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1360,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##  [1362,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1364,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1365,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1367,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1368,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##  [1369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1373,]  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1374,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1377,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1381,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1383,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1384,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1386,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##  [1387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##  [1393,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1398,] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1399,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1402,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1403,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1405,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1406,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##           1995  1996  1997  1998  1999  2000  2001  2002  2003  2004  2005
##     [1,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [2,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [3,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##     [4,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##     [5,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##     [6,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##     [7,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [8,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [9,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [10,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [11,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [12,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [13,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [14,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [15,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [16,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [17,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [18,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [19,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [20,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [21,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [22,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [23,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [24,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [25,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [26,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [27,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##    [28,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##    [29,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [30,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [31,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [32,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [33,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [34,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [35,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE
##    [36,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [37,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [38,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [39,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [40,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [41,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##    [42,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [43,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [44,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##    [45,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [46,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [47,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [48,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [49,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
##    [50,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##    [51,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [52,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [53,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [54,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##    [55,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##    [56,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [57,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##    [58,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [59,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [60,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [61,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [62,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##    [63,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [64,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [65,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE
##    [66,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
##    [67,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##    [68,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [69,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [70,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [71,] FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [72,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [73,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [74,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [75,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [76,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##    [77,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##    [78,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [79,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [80,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [81,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [82,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [83,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [84,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [85,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [86,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [87,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [88,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [89,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [90,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [91,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [92,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [93,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [94,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [95,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [96,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [97,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##    [98,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [99,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [100,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [102,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [103,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [104,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [106,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [107,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [108,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [109,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [110,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [111,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [112,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [113,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [114,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [115,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [116,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [119,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [121,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [122,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [127,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [128,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [129,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [130,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [131,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [132,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [133,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [134,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [136,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [138,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [139,]  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE
##   [140,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [142,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [143,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [144,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE
##   [146,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [147,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [150,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [151,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [152,]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [153,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [154,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [155,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [156,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [157,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [161,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [162,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [163,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [164,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [165,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [166,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [167,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [168,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [169,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [171,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE
##   [172,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [173,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [174,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [175,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE
##   [176,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [177,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [180,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [181,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [182,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [183,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [185,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [192,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [196,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [197,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE
##   [198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [200,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [201,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [202,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [203,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [205,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [206,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [207,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [208,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [209,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [210,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [213,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [214,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [219,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [221,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [222,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [224,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [225,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [226,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [229,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [230,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [231,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [233,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE
##   [234,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [235,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
##   [236,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [237,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [239,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [240,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [243,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [244,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [245,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [246,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [248,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [249,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [250,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [252,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [253,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [256,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [257,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [261,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [262,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [263,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [264,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [265,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [266,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [268,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [269,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [274,] FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [275,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [276,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [277,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [279,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [280,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [281,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [283,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [284,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [285,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [288,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [289,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [290,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [292,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [295,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [299,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [302,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [303,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [304,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [305,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [307,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [309,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [310,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [311,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [316,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [317,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [318,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [328,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [332,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [335,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [336,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [338,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [339,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [340,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [341,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [342,] FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [343,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [344,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [345,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##   [346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [348,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [350,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [353,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [355,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [356,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [357,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [359,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [360,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [362,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [363,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [364,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [365,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [367,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [368,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [371,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [374,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [375,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##   [378,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [379,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [381,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [382,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [383,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [384,] FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE
##   [385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [388,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [389,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [391,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [392,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [393,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [399,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [400,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [402,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [403,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [405,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [407,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [409,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [410,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [411,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [412,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [413,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [414,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [415,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [416,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [417,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [418,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [419,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [420,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [421,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [422,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [423,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [424,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [425,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [426,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [427,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [428,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE
##   [429,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [430,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [431,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [432,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [433,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [434,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [435,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [436,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [437,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [438,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [439,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [440,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [441,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [442,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [443,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [444,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [445,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [446,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [447,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [448,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [449,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [450,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [451,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [452,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [453,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [454,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [455,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [456,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [457,]  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [458,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [459,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [460,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [461,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [462,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [463,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [464,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [465,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [466,]  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [467,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [468,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [469,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [470,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [471,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [472,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [473,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [474,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [475,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [476,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [477,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [478,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [479,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [480,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [481,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [482,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [483,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [484,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [485,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [486,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [487,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [488,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [489,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [490,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [491,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [492,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [493,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [494,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [495,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [496,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [497,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [498,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [499,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [500,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [501,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [502,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [503,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [504,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [505,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [506,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [507,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [508,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [509,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
##   [510,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [511,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [512,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [513,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [514,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [515,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [516,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [517,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [518,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [519,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [520,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [521,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [522,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [523,]  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [524,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [525,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [526,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [527,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [528,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [529,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [530,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [531,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [532,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [533,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [534,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [535,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [536,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [537,] FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [538,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [539,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [540,]  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [541,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [542,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [543,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [544,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [545,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##   [546,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [547,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [548,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [549,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [550,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [551,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [552,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [553,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [554,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [555,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE
##   [556,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [557,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [558,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [559,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [560,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [561,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [562,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [563,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [564,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [565,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [566,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [567,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [568,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##   [569,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [570,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [571,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [572,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [573,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [574,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [575,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [576,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [577,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [578,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [579,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [580,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [581,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [582,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [583,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [584,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [585,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [586,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [587,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [588,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [589,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [590,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [591,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [592,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [593,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [594,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [595,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [596,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [597,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [598,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [599,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [600,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [601,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [602,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [603,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [604,]  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [605,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [606,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [607,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [608,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [609,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [610,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [611,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [612,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [613,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [614,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [615,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [616,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [617,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [618,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE
##   [619,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [620,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [621,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [622,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [623,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [624,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [625,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [626,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [627,] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [628,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [629,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [630,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [631,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [632,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [633,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [634,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE
##   [635,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [636,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [637,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [638,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [639,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [640,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [641,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [642,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [643,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [644,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [645,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [646,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [647,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [648,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [649,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [650,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [651,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [652,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [653,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
##   [654,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [655,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [656,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [657,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [658,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [659,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [660,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [661,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [662,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [663,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [664,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [665,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [666,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [667,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE
##   [668,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [669,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [670,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [671,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [672,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [673,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [674,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [675,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [676,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [677,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [678,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [679,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [680,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [681,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [682,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [683,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [684,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [685,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [686,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [687,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [688,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [689,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [690,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [691,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [692,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [693,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [694,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [695,]  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [696,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [697,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [698,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [699,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [700,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [701,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [702,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [703,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [704,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [705,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [706,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [707,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [708,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [709,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [710,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##   [711,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [712,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [713,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [714,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [715,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [716,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [717,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [718,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [719,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [720,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [721,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [722,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [723,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [724,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [725,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [726,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [727,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [728,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [729,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [730,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [731,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [732,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [733,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [734,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [735,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [736,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [737,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [738,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [739,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [740,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [741,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [742,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [743,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [744,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [745,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [746,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [747,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [748,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [749,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [750,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [751,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [752,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [753,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [754,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [755,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [756,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [757,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [758,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [759,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [760,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [761,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [762,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [763,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [764,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [765,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [766,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [767,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [768,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [769,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [770,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [771,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [772,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [773,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [774,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [775,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [776,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [777,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [778,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [779,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [780,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [781,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [782,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [783,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [784,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [785,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [786,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [787,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [788,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [789,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [790,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [791,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [792,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [793,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [794,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [795,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [796,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [797,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [798,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [799,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [800,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [801,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [802,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [803,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [804,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [805,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [806,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [807,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [808,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [809,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [810,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [811,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [812,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [813,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [814,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [815,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [816,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [817,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [818,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [819,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [820,] FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [821,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [822,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [823,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [824,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [825,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [826,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [827,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [828,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [829,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [830,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [831,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [832,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [833,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [834,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [835,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [836,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [837,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [838,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [839,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [840,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [841,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [842,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [843,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [844,] FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [845,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [846,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [847,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [848,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [849,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [850,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [851,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [852,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [853,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [854,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [855,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [856,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [857,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [858,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [859,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [860,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [861,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [862,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [863,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [864,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [865,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [866,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [867,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [868,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [869,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [870,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [871,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [872,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [873,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [874,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [875,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [876,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [877,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [878,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [879,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [880,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [881,] FALSE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [882,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [883,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [884,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [885,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [886,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [887,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [888,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [889,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [890,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [891,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [892,]  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [893,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [894,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [895,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [896,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [897,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [898,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [899,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [900,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [901,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [902,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [903,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [904,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [905,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE
##   [906,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [907,] FALSE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [908,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [909,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [910,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [911,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [912,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [913,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [914,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [915,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [916,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [917,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [918,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [919,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [920,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [921,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [922,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [923,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [924,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [925,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [926,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [927,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [928,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [929,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE
##   [930,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [931,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE
##   [932,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [933,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [934,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [935,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [936,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [937,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [938,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [939,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [940,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [941,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [942,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [943,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [944,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [945,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [946,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [947,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [948,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [949,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [950,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [951,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [952,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE
##   [953,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE
##   [954,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [955,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [956,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [957,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [958,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [959,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [960,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE
##   [961,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [962,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [963,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [964,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [965,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [966,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [967,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE
##   [968,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [969,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [970,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [971,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [972,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [973,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [974,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [975,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [976,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [977,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE
##   [978,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE
##   [979,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [980,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [981,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [982,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [983,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##   [984,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##   [985,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [986,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [987,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [988,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [989,] FALSE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [990,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [991,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [992,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [993,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [994,] FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [995,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [996,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [997,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##   [998,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE
##   [999,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1000,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1001,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1002,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1003,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1004,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1005,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1006,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1007,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1008,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1009,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1010,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1011,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1012,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1013,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1014,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1015,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1016,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1017,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1018,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1019,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1020,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1021,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE
##  [1022,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1023,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1024,]  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1025,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1026,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1027,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1028,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1029,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##  [1030,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1031,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1032,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1033,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1034,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1035,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1036,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1037,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1038,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1039,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1040,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1041,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1042,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1043,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE FALSE FALSE  TRUE
##  [1044,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1045,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1046,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1047,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1048,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1049,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1050,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1051,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##  [1052,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1053,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1054,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1055,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1056,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1057,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1058,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##  [1059,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1060,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1061,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1062,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1063,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1064,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1065,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1066,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##  [1067,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1068,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1069,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1070,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1071,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1072,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1073,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1074,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1075,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1076,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1077,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##  [1078,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1079,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##  [1080,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##  [1081,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1082,]  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1083,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1084,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1085,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1086,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1087,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1088,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1089,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1090,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1091,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1092,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1093,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1094,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1095,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1096,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1097,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1098,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1099,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1100,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1102,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1103,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1104,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1105,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1106,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1107,]  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1108,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1109,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1110,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1111,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1112,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1114,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1115,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1116,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1117,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1118,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1119,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1121,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1127,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1128,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1129,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1130,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1131,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1132,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1133,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1136,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1138,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1139,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1140,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1141,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1142,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1143,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1144,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1145,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1146,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1147,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1150,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1151,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1152,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1154,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1156,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1157,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1159,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1161,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1162,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1163,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1164,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1165,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1166,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1169,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1170,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1171,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1174,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1175,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1176,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1178,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1181,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1182,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1183,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1185,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1188,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1192,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1196,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1197,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1198,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1199,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1200,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1202,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##  [1203,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE
##  [1204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1205,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1207,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1209,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1210,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1212,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1213,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1214,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1215,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1216,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1219,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1220,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1221,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1222,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1224,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1225,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1226,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE
##  [1227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1229,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1230,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1231,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1232,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1233,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1234,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1235,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1236,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1237,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1239,]  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1241,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1244,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1246,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1248,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1249,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1250,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1251,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1252,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1253,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1254,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1256,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1257,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1258,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1260,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1261,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1265,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1266,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1267,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1268,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1269,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1270,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1271,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1273,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1274,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1275,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1276,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1277,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1278,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1279,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1280,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1281,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1283,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1284,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1285,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1288,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1289,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1290,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1291,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1292,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1295,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##  [1297,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1299,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1300,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1302,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1303,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1307,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1309,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE
##  [1310,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1311,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1316,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1318,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1319,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##  [1321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1327,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1328,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1334,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1338,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1341,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1342,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1345,]  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1348,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1350,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1351,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1353,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1355,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1356,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1360,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE  TRUE
##  [1361,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1362,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1364,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1365,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1366,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##  [1367,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1368,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1370,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##  [1372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1374,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1379,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1381,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1382,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE
##  [1383,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1392,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1393,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1398,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1399,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1402,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1403,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1405,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##           2006  2007  2008  2009  2010  2011  2012
##     [1,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [2,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [3,] FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##     [4,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [5,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [6,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##     [7,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [8,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##     [9,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [10,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [11,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [12,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [13,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [14,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [15,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [16,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [17,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [18,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [19,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [20,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [21,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [22,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [23,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [24,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [25,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [26,] FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE
##    [27,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [28,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [29,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [30,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [31,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [32,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [33,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [34,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [35,] FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##    [36,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [37,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [38,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [39,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [40,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [41,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [42,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [43,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [44,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [45,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [46,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##    [47,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [48,] FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE
##    [49,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [50,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [51,] FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##    [52,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [53,]  TRUE FALSE FALSE FALSE  TRUE  TRUE FALSE
##    [54,] FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##    [55,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##    [56,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [57,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [58,] FALSE  TRUE FALSE  TRUE FALSE  TRUE  TRUE
##    [59,] FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##    [60,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [61,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [62,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [63,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [64,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [65,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [66,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##    [67,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [68,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [69,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [70,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [71,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [72,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [73,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [74,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [75,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [76,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [77,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [78,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [79,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [80,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [81,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [82,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [83,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [84,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [85,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [86,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [87,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [88,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [89,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [90,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [91,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [92,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [93,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##    [94,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [95,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [96,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##    [97,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##    [98,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##    [99,]  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [100,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [101,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [102,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [103,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [104,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [105,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [106,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [107,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [108,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [109,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [110,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [111,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [112,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [114,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [115,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [116,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [117,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [118,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [119,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [120,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [121,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [122,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [125,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [126,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [127,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [128,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [129,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [130,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [131,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [132,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [133,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [134,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [136,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [138,] FALSE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [139,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [140,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [141,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [142,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [144,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [145,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [146,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [147,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [150,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [151,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [152,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [154,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [156,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [157,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [159,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [160,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [161,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [162,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [163,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [164,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [165,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [166,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [167,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [168,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [169,] FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [170,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [171,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [172,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [174,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [175,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [176,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [178,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [180,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [181,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [182,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [183,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [185,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [186,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [187,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [188,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [190,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [192,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [193,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [195,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [196,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [197,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [198,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [199,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [200,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [202,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [203,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [204,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [205,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [206,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [207,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [208,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [209,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [210,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [212,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [213,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [214,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [215,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [219,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [220,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [221,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [222,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [224,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [225,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [226,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [230,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [231,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [232,]  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [233,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [234,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [235,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [236,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [237,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [238,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [239,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [241,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [243,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [244,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [246,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [248,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [249,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [250,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [251,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [252,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [253,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [254,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [256,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [257,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [258,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [259,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [260,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [261,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [265,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [266,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [267,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [268,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [269,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [270,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [271,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [272,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [273,]  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##   [274,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [275,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [276,] FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE
##   [277,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [278,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [279,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [280,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [281,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [282,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [283,] FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE
##   [284,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [285,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [288,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [289,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [290,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [292,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [295,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [296,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [297,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [298,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [299,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [301,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [302,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [303,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [306,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [307,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [308,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [309,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [310,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [311,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [312,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [313,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [314,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [315,]  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [316,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [317,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [318,]  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [319,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [320,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [322,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [323,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [324,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [327,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [328,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [329,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [330,] FALSE FALSE  TRUE FALSE FALSE  TRUE  TRUE
##   [331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [333,] FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE
##   [334,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [336,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [338,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [341,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [342,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [344,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [345,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [347,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [348,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [350,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [351,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [352,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [353,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [355,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [356,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [357,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [358,]  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE
##   [359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [360,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [361,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE
##   [362,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [364,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [365,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [366,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [367,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [368,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [369,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [370,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [371,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [374,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [375,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [376,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [377,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [378,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [379,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [380,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [381,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [382,]  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [383,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [384,] FALSE FALSE  TRUE FALSE FALSE FALSE  TRUE
##   [385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [386,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [387,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [388,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##   [389,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [391,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [392,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [393,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [394,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [395,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [396,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [398,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [399,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [400,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [402,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [403,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [405,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [407,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [409,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [410,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [411,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [412,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [413,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [414,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [415,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [416,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [417,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [418,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [419,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [420,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [421,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##   [422,]  TRUE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [423,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [424,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [425,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [426,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [427,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [428,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##   [429,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [430,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [431,] FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##   [432,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [433,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [434,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [435,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [436,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [437,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [438,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [439,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [440,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [441,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [442,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [443,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [444,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [445,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [446,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [447,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [448,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [449,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [450,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [451,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [452,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [453,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [454,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [455,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [456,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [457,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [458,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [459,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [460,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [461,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [462,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [463,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [464,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [465,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [466,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [467,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [468,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [469,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [470,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [471,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [472,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [473,] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [474,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [475,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [476,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [477,] FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE
##   [478,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [479,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [480,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [481,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [482,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [483,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [484,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [485,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [486,] FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE
##   [487,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [488,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [489,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [490,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [491,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [492,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [493,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [494,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [495,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [496,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [497,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [498,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [499,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [500,] FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE
##   [501,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [502,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [503,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [504,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [505,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [506,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [507,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [508,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [509,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [510,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [511,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [512,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [513,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [514,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [515,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [516,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [517,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [518,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [519,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [520,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [521,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##   [522,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [523,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [524,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [525,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [526,] FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE
##   [527,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [528,]  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE
##   [529,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [530,]  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE
##   [531,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [532,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [533,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##   [534,] FALSE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [535,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [536,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [537,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [538,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [539,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [540,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [541,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [542,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [543,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [544,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [545,]  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [546,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [547,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [548,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [549,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [550,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [551,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [552,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [553,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [554,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [555,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [556,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [557,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [558,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [559,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [560,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [561,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [562,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [563,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [564,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [565,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [566,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [567,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [568,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [569,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [570,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [571,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [572,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [573,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [574,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [575,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [576,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [577,] FALSE FALSE  TRUE FALSE FALSE FALSE  TRUE
##   [578,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [579,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [580,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [581,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [582,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [583,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [584,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [585,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [586,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [587,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [588,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [589,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [590,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [591,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [592,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [593,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [594,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [595,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [596,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [597,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [598,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [599,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE
##   [600,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [601,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [602,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [603,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [604,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [605,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [606,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [607,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [608,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [609,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [610,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [611,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##   [612,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [613,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [614,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [615,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [616,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [617,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [618,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [619,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [620,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [621,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [622,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [623,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [624,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [625,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE
##   [626,]  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE
##   [627,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [628,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [629,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [630,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [631,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [632,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [633,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [634,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [635,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [636,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [637,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [638,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [639,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [640,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [641,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [642,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [643,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [644,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [645,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [646,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [647,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [648,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [649,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [650,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [651,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [652,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE
##   [653,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [654,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [655,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [656,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [657,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [658,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [659,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [660,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [661,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [662,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [663,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [664,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [665,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [666,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [667,]  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##   [668,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [669,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [670,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [671,]  TRUE  TRUE  TRUE FALSE  TRUE FALSE  TRUE
##   [672,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [673,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
##   [674,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [675,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [676,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [677,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [678,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [679,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [680,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [681,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [682,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [683,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [684,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [685,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [686,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [687,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [688,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [689,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [690,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [691,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [692,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [693,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [694,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [695,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [696,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [697,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [698,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [699,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [700,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [701,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [702,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [703,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [704,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [705,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [706,] FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [707,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [708,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [709,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [710,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [711,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [712,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [713,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [714,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [715,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [716,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [717,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [718,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [719,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [720,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [721,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [722,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [723,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [724,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [725,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [726,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [727,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [728,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [729,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [730,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [731,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [732,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [733,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [734,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [735,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [736,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [737,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [738,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [739,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [740,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [741,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [742,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [743,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [744,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [745,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [746,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [747,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [748,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [749,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [750,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [751,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [752,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [753,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [754,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [755,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE
##   [756,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE
##   [757,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [758,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [759,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [760,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [761,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [762,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [763,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [764,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [765,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [766,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [767,] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE
##   [768,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [769,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [770,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [771,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [772,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [773,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [774,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [775,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [776,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [777,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [778,]  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE
##   [779,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [780,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [781,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [782,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [783,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [784,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [785,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [786,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [787,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [788,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [789,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [790,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [791,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##   [792,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [793,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [794,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [795,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [796,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [797,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [798,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [799,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [800,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [801,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [802,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [803,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
##   [804,] FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [805,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [806,] FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [807,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [808,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [809,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [810,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [811,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [812,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [813,]  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [814,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [815,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [816,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [817,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [818,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [819,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [820,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [821,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [822,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [823,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [824,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [825,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [826,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [827,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [828,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [829,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [830,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [831,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [832,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [833,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [834,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [835,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [836,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [837,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [838,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [839,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [840,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [841,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [842,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [843,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [844,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [845,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [846,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [847,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [848,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [849,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [850,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [851,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [852,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [853,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [854,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [855,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [856,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [857,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [858,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [859,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [860,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [861,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [862,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [863,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [864,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [865,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [866,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [867,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [868,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
##   [869,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [870,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [871,]  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE
##   [872,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [873,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [874,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [875,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [876,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [877,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [878,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [879,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [880,] FALSE  TRUE FALSE FALSE FALSE  TRUE  TRUE
##   [881,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [882,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [883,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [884,]  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##   [885,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [886,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [887,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [888,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [889,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [890,]  TRUE FALSE  TRUE  TRUE FALSE FALSE  TRUE
##   [891,]  TRUE FALSE  TRUE  TRUE FALSE FALSE  TRUE
##   [892,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [893,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [894,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [895,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [896,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [897,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [898,]  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##   [899,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [900,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [901,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [902,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [903,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [904,]  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE
##   [905,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [906,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [907,]  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
##   [908,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [909,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [910,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [911,]  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE
##   [912,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [913,]  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE
##   [914,]  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE
##   [915,]  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##   [916,]  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE
##   [917,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [918,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [919,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [920,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [921,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [922,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [923,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [924,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [925,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [926,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [927,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [928,]  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE
##   [929,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [930,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [931,] FALSE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##   [932,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [933,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [934,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [935,] FALSE  TRUE FALSE  TRUE FALSE FALSE  TRUE
##   [936,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [937,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [938,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [939,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [940,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [941,]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
##   [942,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [943,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [944,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [945,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [946,]  TRUE FALSE  TRUE FALSE  TRUE FALSE  TRUE
##   [947,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [948,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##   [949,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [950,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [951,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [952,] FALSE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##   [953,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [954,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##   [955,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [956,]  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE
##   [957,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [958,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [959,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [960,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [961,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [962,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [963,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [964,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [965,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [966,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE
##   [967,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##   [968,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [969,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [970,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [971,]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
##   [972,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##   [973,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [974,]  TRUE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##   [975,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##   [976,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [977,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [978,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [979,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [980,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [981,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [982,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [983,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [984,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [985,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##   [986,]  TRUE FALSE FALSE FALSE  TRUE FALSE FALSE
##   [987,]  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE
##   [988,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [989,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [990,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [991,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##   [992,]  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##   [993,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [994,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##   [995,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [996,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##   [997,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [998,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##   [999,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1000,]  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE
##  [1001,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1002,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1003,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1004,]  TRUE  TRUE  TRUE FALSE FALSE FALSE  TRUE
##  [1005,]  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
##  [1006,] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
##  [1007,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1008,]  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE
##  [1009,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1010,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1011,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1012,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1013,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1014,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1015,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1016,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1017,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1018,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1019,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1020,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1021,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1022,]  TRUE  TRUE FALSE FALSE FALSE  TRUE FALSE
##  [1023,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1024,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1025,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1026,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1027,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1028,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1029,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1030,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1031,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE
##  [1032,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1033,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1034,] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE
##  [1035,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1036,] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE
##  [1037,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1038,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1039,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1040,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1041,] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE
##  [1042,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1043,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1044,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1045,] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
##  [1046,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1047,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1048,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1049,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##  [1050,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1051,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1052,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1053,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1054,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1055,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1056,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1057,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1058,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1059,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1060,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1061,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1062,] FALSE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1063,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1064,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##  [1065,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1066,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1067,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1068,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1069,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1070,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1071,]  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1072,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1073,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1074,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1075,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1076,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1077,] FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
##  [1078,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1079,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1080,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1081,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1082,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1083,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1084,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1085,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1086,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1087,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1088,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1089,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1090,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1091,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1092,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1093,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1094,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1095,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1096,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1097,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1098,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1099,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1100,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1101,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1102,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1103,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1104,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1105,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1106,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1107,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1108,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1109,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1110,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1111,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1112,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1113,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1114,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1115,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1116,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1117,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1118,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1119,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1120,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1121,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1122,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1123,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1124,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1125,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1126,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1127,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1128,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1129,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1130,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1131,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1132,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1133,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1134,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1135,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1136,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1137,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1138,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1139,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1140,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1141,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1142,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1143,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1144,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1145,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1146,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1147,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1148,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1149,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1150,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1151,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1152,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1153,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1154,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1155,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1156,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1157,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1158,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1159,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1160,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1161,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1162,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1163,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1164,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1165,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1166,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1167,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1168,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1169,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1170,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1171,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1172,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1173,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1174,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1175,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1176,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1177,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1178,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1179,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1180,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1181,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1182,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1183,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1184,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1185,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1186,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1187,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1188,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1189,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1190,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1191,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1192,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1193,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1194,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1195,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1196,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1197,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1198,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1199,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1200,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1201,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1202,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1203,] FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE
##  [1204,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1205,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1206,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1207,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1208,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1209,] FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##  [1210,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1211,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1212,] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE
##  [1213,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1214,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1215,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1216,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1217,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1218,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1219,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1220,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1221,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1222,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1223,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1224,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1225,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1226,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1227,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1228,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1229,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1230,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1231,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1232,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1233,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1234,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1235,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1236,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1237,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1238,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1239,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1240,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1241,]  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE
##  [1242,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1243,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1244,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1245,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1246,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1247,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1248,]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1249,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE
##  [1250,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1251,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1252,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1253,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1254,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1255,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1256,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1257,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1258,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1259,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1260,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1261,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1262,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1263,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1264,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1265,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1266,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1267,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1268,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1269,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1270,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1271,] FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE
##  [1272,]  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE
##  [1273,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1274,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1275,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1276,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1277,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1278,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1279,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1280,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1281,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1282,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1283,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE
##  [1284,] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1285,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1286,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1287,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1288,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1289,] FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE
##  [1290,] FALSE  TRUE FALSE  TRUE  TRUE FALSE FALSE
##  [1291,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1292,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1293,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1294,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1295,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1296,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1297,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1298,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1299,] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1300,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1301,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1302,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1303,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1304,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1305,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1306,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1307,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1308,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1309,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1310,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1311,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1312,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1313,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1314,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1315,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1316,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1317,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1318,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1319,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1320,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1321,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1322,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1323,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1324,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1325,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1326,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1327,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1328,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1329,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1330,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1331,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1332,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1333,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1334,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1335,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1336,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1337,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1338,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1339,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1340,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1341,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1342,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1343,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1344,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1345,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1346,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1347,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1348,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1349,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1350,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1351,] FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1352,]  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1353,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1354,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1355,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1356,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1357,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1358,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1359,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1360,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1361,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1362,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1363,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1364,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1365,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1366,] FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE
##  [1367,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1368,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1369,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1370,]  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE
##  [1371,] FALSE FALSE  TRUE FALSE  TRUE FALSE  TRUE
##  [1372,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1373,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1374,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1375,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1376,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1377,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1378,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1379,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1380,]  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1381,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1382,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1383,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1384,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1385,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1386,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1387,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1388,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1389,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1390,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1391,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1392,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1393,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1394,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1395,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1396,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1397,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1398,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1399,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1400,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1401,] FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [1402,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1403,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1404,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1405,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1406,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1407,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [1408,]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
##  [ reached getOption("max.print") -- omitted 16284 rows ]
```

```r
sapply(fisheries, class)
```

```
##                 Country             Common name          ISSCAAP group# 
##             "character"             "character"               "numeric" 
## ISSCAAP taxonomic group          ASFIS species#      ASFIS species name 
##             "character"             "character"             "character" 
##  FAO major fishing area                 Measure                    1950 
##               "numeric"             "character"             "character" 
##                    1951                    1952                    1953 
##             "character"             "character"             "character" 
##                    1954                    1955                    1956 
##             "character"             "character"             "character" 
##                    1957                    1958                    1959 
##             "character"             "character"             "character" 
##                    1960                    1961                    1962 
##             "character"             "character"             "character" 
##                    1963                    1964                    1965 
##             "character"             "character"             "character" 
##                    1966                    1967                    1968 
##             "character"             "character"             "character" 
##                    1969                    1970                    1971 
##             "character"             "character"             "character" 
##                    1972                    1973                    1974 
##             "character"             "character"             "character" 
##                    1975                    1976                    1977 
##             "character"             "character"             "character" 
##                    1978                    1979                    1980 
##             "character"             "character"             "character" 
##                    1981                    1982                    1983 
##             "character"             "character"             "character" 
##                    1984                    1985                    1986 
##             "character"             "character"             "character" 
##                    1987                    1988                    1989 
##             "character"             "character"             "character" 
##                    1990                    1991                    1992 
##             "character"             "character"             "character" 
##                    1993                    1994                    1995 
##             "character"             "character"             "character" 
##                    1996                    1997                    1998 
##             "character"             "character"             "character" 
##                    1999                    2000                    2001 
##             "character"             "character"             "character" 
##                    2002                    2003                    2004 
##             "character"             "character"             "character" 
##                    2005                    2006                    2007 
##             "character"             "character"             "character" 
##                    2008                    2009                    2010 
##             "character"             "character"             "character" 
##                    2011                    2012 
##             "character"             "character"
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <-janitor::clean_names(fisheries)
```


```r
names(fisheries)
```

```
##  [1] "country"                 "common_name"            
##  [3] "isscaap_group_number"    "isscaap_taxonomic_group"
##  [5] "asfis_species_number"    "asfis_species_name"     
##  [7] "fao_major_fishing_area"  "measure"                
##  [9] "x1950"                   "x1951"                  
## [11] "x1952"                   "x1953"                  
## [13] "x1954"                   "x1955"                  
## [15] "x1956"                   "x1957"                  
## [17] "x1958"                   "x1959"                  
## [19] "x1960"                   "x1961"                  
## [21] "x1962"                   "x1963"                  
## [23] "x1964"                   "x1965"                  
## [25] "x1966"                   "x1967"                  
## [27] "x1968"                   "x1969"                  
## [29] "x1970"                   "x1971"                  
## [31] "x1972"                   "x1973"                  
## [33] "x1974"                   "x1975"                  
## [35] "x1976"                   "x1977"                  
## [37] "x1978"                   "x1979"                  
## [39] "x1980"                   "x1981"                  
## [41] "x1982"                   "x1983"                  
## [43] "x1984"                   "x1985"                  
## [45] "x1986"                   "x1987"                  
## [47] "x1988"                   "x1989"                  
## [49] "x1990"                   "x1991"                  
## [51] "x1992"                   "x1993"                  
## [53] "x1994"                   "x1995"                  
## [55] "x1996"                   "x1997"                  
## [57] "x1998"                   "x1999"                  
## [59] "x2000"                   "x2001"                  
## [61] "x2002"                   "x2003"                  
## [63] "x2004"                   "x2005"                  
## [65] "x2006"                   "x2007"                  
## [67] "x2008"                   "x2009"                  
## [69] "x2010"                   "x2011"                  
## [71] "x2012"
```


```r
fisheries$country <- as.factor(fisheries$country)
```


```r
  fisheries$isscaap_group_number <-as.factor(fisheries$isscaap_group_number) 
  fisheries$asfis_species_number <-as.factor(fisheries$asfis_species_number) 
  fisheries$fao_major_fishing_area <-as.factor(fisheries$fao_major_fishing_area)
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  count(country)
```

```
## # A tibble: 203 × 2
## # Groups:   country [203]
##    country                 n
##    <fct>               <int>
##  1 Albania               934
##  2 Algeria              1561
##  3 American Samoa        556
##  4 Angola               2119
##  5 Anguilla              129
##  6 Antigua and Barbuda   356
##  7 Argentina            3403
##  8 Aruba                 172
##  9 Australia            8183
## 10 Bahamas               423
## # … with 193 more rows
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_new <-fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
fisheries_new
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_specie…¹  year catch
##    <fct>   <chr>                   <chr>              <fct>          <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1995    NA
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1996    53
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1997    20
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1998    31
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1999    30
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2000    30
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2001    16
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2002    79
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2003     1
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2004     4
## # … with 376,761 more rows, and abbreviated variable name ¹​asfis_species_number
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_new %>% 
  summarize(distinct_species = n_distinct(asfis_species_number))
```

```
## # A tibble: 1 × 1
##   distinct_species
##              <int>
## 1             1551
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_new %>% 
  filter(year == 2000) %>% 
  select(country, year, catch) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 8,793 × 3
##    country                   year catch
##    <fct>                    <dbl> <dbl>
##  1 China                     2000  9068
##  2 Peru                      2000  5717
##  3 Russian Federation        2000  5065
##  4 Viet Nam                  2000  4945
##  5 Chile                     2000  4299
##  6 China                     2000  3288
##  7 China                     2000  2782
##  8 United States of America  2000  2438
##  9 China                     2000  1234
## 10 Philippines               2000   999
## # … with 8,783 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_new %>%
  group_by(country) %>% 
  filter(asfis_species_name == "Sardina pilchardus") %>% 
  filter(between(year, 1990,2000)) %>% 
  summarize(sardine_catch = sum(catch)) %>% 
  arrange(desc(sardine_catch))
```

```
## # A tibble: 37 × 2
##    country               sardine_catch
##    <fct>                         <dbl>
##  1 Morocco                        7470
##  2 Spain                          3507
##  3 Russian Federation             1639
##  4 Ukraine                        1030
##  5 Portugal                        818
##  6 Greece                          528
##  7 Italy                           507
##  8 Serbia and Montenegro           478
##  9 Denmark                         477
## 10 Tunisia                         427
## # … with 27 more rows
```


8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_new %>% 
  group_by(country) %>% 
  filter(between(year, 2008,2012)) %>% 
  filter(isscaap_taxonomic_group == "Squids, cuttlefishes, octopuses") %>%
  summarize(cephalopod_catch = sum(catch, na.rm = T)) %>% 
  arrange(desc(cephalopod_catch)) %>% 
  head(n=5)
```

```
## # A tibble: 5 × 2
##   country            cephalopod_catch
##   <fct>                         <dbl>
## 1 China                          8349
## 2 Korea, Republic of             3480
## 3 Peru                           3422
## 4 Japan                          3248
## 5 Chile                          2775
```


9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fisheries_new %>% 
  group_by(asfis_species_name) %>% 
  filter(between(year, 2008,2012)) %>% 
  filter(asfis_species_name != "Osteichthyes") %>%
  tabyl(asfis_species_name, na.rm=T) %>% 
  arrange(desc(total=(n)))
```

```
##                asfis_species_name    n      percent
##                 Thunnus albacares 1006 2.030109e-02
##                    Thunnus obesus  923 1.862615e-02
##                   Xiphias gladius  837 1.689066e-02
##                    Elasmobranchii  761 1.535698e-02
##                Katsuwonus pelamis  761 1.535698e-02
##                  Thunnus alalunga  755 1.523590e-02
##                 Makaira nigricans  584 1.178512e-02
##                         Mugilidae  482 9.726763e-03
##                        Rajiformes  427 8.616862e-03
##                       Scombroidei  417 8.415062e-03
##                         Brachyura  410 8.273802e-03
##                     Sphyraena spp  381 7.688582e-03
##                       Octopodidae  377 7.607862e-03
##                    Makaira indica  362 7.305162e-03
##                   Prionace glauca  361 7.284982e-03
##                          Mollusca  358 7.224442e-03
##                 Scomber japonicus  351 7.083182e-03
##                 Isurus oxyrinchus  335 6.760302e-03
##                 Tetrapturus audax  333 6.719942e-03
##                          Sparidae  323 6.518142e-03
##                        Carangidae  321 6.477782e-03
##       Loliginidae, Ommastrephidae  319 6.437422e-03
##                          Natantia  314 6.336522e-03
##               Coryphaena hippurus  302 6.094362e-03
##                   Epinephelus spp  296 5.973282e-03
##              Sepiidae, Sepiolidae  287 5.791662e-03
##          Auxis thazard, A. rochei  278 5.610042e-03
##                     Istiophoridae  277 5.589862e-03
##                 Pleuronectiformes  277 5.589862e-03
##                           Ariidae  264 5.327521e-03
##                         Crustacea  263 5.307341e-03
##        Haemulidae (=Pomadasyidae)  261 5.266981e-03
##            Acanthocybium solandri  256 5.166081e-03
##                        Serranidae  255 5.145901e-03
##                        Lutjanidae  246 4.964281e-03
##                        Sciaenidae  246 4.964281e-03
##           Istiophorus platypterus  237 4.782661e-03
##                     Panulirus spp  230 4.641401e-03
##                     Trachurus spp  225 4.540501e-03
##               Trichiurus lepturus  225 4.540501e-03
##            Engraulis encrasicolus  214 4.318521e-03
##            Euthynnus alletteratus  213 4.298341e-03
##                       Penaeus spp  212 4.278161e-03
##                    Sardinella spp  211 4.257981e-03
##                       Sarda sarda  207 4.177261e-03
##                Sardina pilchardus  200 4.036001e-03
##                        Clupeoidei  199 4.015821e-03
##              Istiophorus albicans  194 3.914921e-03
##                        Caranx spp  188 3.793841e-03
##                      Scorpaenidae  177 3.571861e-03
##                      Gadus morhua  176 3.551681e-03
##               Tetrapturus albidus  173 3.491141e-03
##                   Thunnus thynnus  164 3.309521e-03
##                      Lutjanus spp  163 3.289341e-03
##                        Loligo spp  162 3.269161e-03
##                        Zeus faber  162 3.269161e-03
##                  Scomber scombrus  158 3.188441e-03
##             Merluccius merluccius  156 3.148081e-03
##                          Bivalvia  153 3.087541e-03
##                     Holothuroidea  152 3.067361e-03
##                       Lethrinidae  151 3.047181e-03
##          Dissostichus eleginoides  149 3.006821e-03
##                     Psetta maxima  149 3.006821e-03
##                       Solea solea  146 2.946281e-03
##                 Euthynnus affinis  140 2.825201e-03
##                       Siganus spp  140 2.825201e-03
##                 Sprattus sprattus  140 2.825201e-03
##              Merlangius merlangus  139 2.805021e-03
##                       Boops boops  137 2.764661e-03
##                          Raja spp  136 2.744481e-03
##                         Triglidae  136 2.744481e-03
##                 Squalus acanthias  135 2.724301e-03
##      Reinhardtius hippoglossoides  133 2.683941e-03
##                      Sebastes spp  133 2.683941e-03
##           Scomberomorus commerson  132 2.663761e-03
##                        Balistidae  131 2.643581e-03
##               Nephrops norvegicus  131 2.643581e-03
##               Pomatomus saltatrix  131 2.643581e-03
##                   Panulirus argus  128 2.583041e-03
##         Hippoglossus hippoglossus  126 2.542681e-03
##                Platichthys flesus  125 2.522501e-03
##          Melanogrammus aeglefinus  121 2.441781e-03
##                         Squalidae  121 2.441781e-03
##                     Conger conger  120 2.421601e-03
##                       Exocoetidae  120 2.421601e-03
##                 Scomberomorus spp  119 2.401421e-03
##                     Belone belone  118 2.381241e-03
##                 Pandalus borealis  118 2.381241e-03
##                      Strombus spp  118 2.381241e-03
##                      Mustelus spp  116 2.340881e-03
##                          Scaridae  116 2.340881e-03
##                   Clupea harengus  115 2.320701e-03
##                       Seriola spp  112 2.260161e-03
##                     Macrourus spp  111 2.239981e-03
##                     Sparus aurata  111 2.239981e-03
##                    Decapterus spp  108 2.179441e-03
##                        Gadiformes  108 2.179441e-03
##                        Mullus spp  108 2.179441e-03
##          Micromesistius poutassou  107 2.159261e-03
##              Rachycentron canadum  107 2.159261e-03
##        Glyptocephalus cynoglossus  106 2.139081e-03
##                  Homarus gammarus  106 2.139081e-03
##                          Labridae  105 2.118901e-03
##                  Thunnus maccoyii  105 2.118901e-03
##              Dicentrarchus labrax  104 2.098721e-03
##                     Cynoglossidae  103 2.078541e-03
##           Spondyliosoma cantharus  103 2.078541e-03
##                     Pagrus pagrus  102 2.058361e-03
##          Parapenaeus longirostris  102 2.058361e-03
##                        Gastropoda   99 1.997821e-03
##                       Lamna nasus   99 1.997821e-03
##                 Pollachius virens   99 1.997821e-03
##                 Sepia officinalis   99 1.997821e-03
##               Trachurus trachurus   99 1.997821e-03
##                       Perciformes   98 1.977641e-03
##                       Sarpa salpa   98 1.977641e-03
##                 Antimora rostrata   97 1.957461e-03
##                   Hemiramphus spp   97 1.957461e-03
##                       Lophius spp   97 1.957461e-03
##                 Sardinella aurita   97 1.957461e-03
##                      Stromateidae   97 1.957461e-03
##                   Thunnus tonggol   96 1.937281e-03
##                    Carcharhinidae   94 1.896921e-03
##                Galeorhinus galeus   94 1.896921e-03
##                    Anarhichas spp   93 1.876741e-03
##                         Beryx spp   92 1.856561e-03
##                  Octopus vulgaris   90 1.816201e-03
##                       Polynemidae   90 1.816201e-03
##             Pleuronectes platessa   89 1.796021e-03
##                      Trichiuridae   89 1.796021e-03
##                       Brama brama   88 1.775840e-03
##                       Lichia amia   88 1.775840e-03
##            Rastrelliger kanagurta   88 1.775840e-03
##                       Atherinidae   87 1.755660e-03
##             Lithognathus mormyrus   87 1.755660e-03
##          Coryphaenoides rupestris   86 1.735480e-03
##                 Mullus surmuletus   86 1.735480e-03
##                  Seriola dumerili   86 1.735480e-03
##                        Sphyrnidae   86 1.735480e-03
##                      Synodontidae   86 1.735480e-03
##                      Invertebrata   85 1.715300e-03
##                       Spicara spp   85 1.715300e-03
##            Strongylocentrotus spp   85 1.715300e-03
##                          Mullidae   83 1.674940e-03
##                          Gobiidae   82 1.654760e-03
##      Hippoglossoides platessoides   82 1.654760e-03
##                Ruvettus pretiosus   82 1.654760e-03
##                     Ammodytes spp   81 1.634580e-03
##                       Cephalopoda   80 1.614400e-03
##                  Drepane africana   79 1.594220e-03
##                 Phycis blennoides   79 1.594220e-03
##                     Brosme brosme   78 1.574040e-03
##                Portunus pelagicus   78 1.574040e-03
##                        Dentex spp   76 1.533680e-03
##                      Diplodus spp   76 1.533680e-03
##                     Argentina spp   75 1.513500e-03
##                    Nemipterus spp   75 1.513500e-03
##            Galeoides decadactylus   74 1.493320e-03
##         Helicolenus dactylopterus   74 1.493320e-03
##                Lepidopus caudatus   74 1.493320e-03
##                Thunnus atlanticus   74 1.493320e-03
##                       Molva molva   73 1.473140e-03
##                    Mugil cephalus   73 1.473140e-03
##                      Acanthuridae   72 1.452960e-03
##                     Dentex dentex   72 1.452960e-03
##             Pollachius pollachius   72 1.452960e-03
##            Selar crumenophthalmus   72 1.452960e-03
##                     Rhopilema spp   71 1.432780e-03
##              Dissostichus mawsoni   70 1.412600e-03
##        Lepidocybium flavobrunneum   70 1.412600e-03
##        Lepidorhombus whiffiagonis   70 1.412600e-03
##              Scophthalmus rhombus   70 1.412600e-03
##               Pagellus erythrinus   69 1.392420e-03
##                     Palinurus spp   69 1.392420e-03
##                        Pectinidae   69 1.392420e-03
##                      Raja clavata   69 1.392420e-03
##                       Upeneus spp   69 1.392420e-03
##                      Pagellus spp   68 1.372240e-03
##                  Microstomus kitt   67 1.352060e-03
##                   Oblada melanura   67 1.352060e-03
##                   Trachinus draco   67 1.352060e-03
##            Epinephelus marginatus   66 1.331880e-03
##                        Scombridae   66 1.331880e-03
##                Trisopterus luscus   66 1.331880e-03
##                         Alosa spp   65 1.311700e-03
##                    Cancer pagurus   65 1.311700e-03
##                   Crangon crangon   65 1.311700e-03
##               Ethmalosa fimbriata   65 1.311700e-03
##                    Scylla serrata   65 1.311700e-03
##                         Belonidae   64 1.291520e-03
##          Carcharhinus falciformis   64 1.291520e-03
##               Genypterus blacodes   63 1.271340e-03
##                   Limanda limanda   63 1.271340e-03
##                 Macrourus berglax   63 1.271340e-03
##                       Salmo salar   63 1.271340e-03
##                      Sillaginidae   63 1.271340e-03
##                  Alopias vulpinus   62 1.251160e-03
##                         Congridae   62 1.251160e-03
##                        Pagrus spp   61 1.230980e-03
##              Polyprion americanus   61 1.230980e-03
##                   Trachinotus spp   61 1.230980e-03
##            Brachydeuterus auritus   60 1.210800e-03
##                   Crassostrea spp   60 1.210800e-03
##                   Diplodus sargus   60 1.210800e-03
##                   Penaeus monodon   60 1.210800e-03
##          Chloroscombrus chrysurus   59 1.190620e-03
##                Argyrosomus regius   58 1.170440e-03
##                Pseudotolithus spp   58 1.170440e-03
##                   Centropomus spp   57 1.150260e-03
##               Lophius piscatorius   57 1.150260e-03
##                     Maja squinado   57 1.150260e-03
##                      Salmo trutta   57 1.150260e-03
##             Sardinella maderensis   57 1.150260e-03
##             Scomberomorus cavalla   57 1.150260e-03
##            Scomberomorus guttatus   57 1.150260e-03
##                  Lates calcarifer   56 1.130080e-03
##                   Priacanthus spp   56 1.130080e-03
##              Elagatis bipinnulata   55 1.109900e-03
##                       Engraulidae   55 1.109900e-03
##                 Ocyurus chrysurus   55 1.109900e-03
##                  Pampus argenteus   55 1.109900e-03
##                 Trachurus murphyi   55 1.109900e-03
##                  Anarhichas lupus   54 1.089720e-03
##                Eutrigla gurnardus   54 1.089720e-03
##                        Gerres spp   53 1.069540e-03
##                Megalaspis cordyla   53 1.069540e-03
##                  Molva dypterygia   53 1.069540e-03
##        Tetrapturus angustirostris   52 1.049360e-03
##                     Nototheniidae   51 1.029180e-03
##                 Osmerus eperlanus   51 1.029180e-03
##                  Buccinum undatum   50 1.009000e-03
##                    Merluccius spp   50 1.009000e-03
##              Parastromateus niger   50 1.009000e-03
##            Pseudupeneus prayensis   50 1.009000e-03
##              Scomberomorus tritor   50 1.009000e-03
##                          Soleidae   50 1.009000e-03
##                  Urophycis tenuis   50 1.009000e-03
##                  Branchiostegidae   49 9.888203e-04
##           Hoplostethus atlanticus   49 9.888203e-04
##          Polydactylus quadrifilis   49 9.888203e-04
##           Trachurus mediterraneus   49 9.888203e-04
##                       Alopias spp   48 9.686403e-04
##                       Caesionidae   48 9.686403e-04
##                  Illex argentinus   48 9.686403e-04
##                   Mullus barbatus   48 9.686403e-04
##                Penaeus kerathurus   48 9.686403e-04
##                    Mytilus edulis   47 9.484603e-04
##                     Ostrea edulis   47 9.484603e-04
##                 Sebastes mentella   47 9.484603e-04
##                     Chanos chanos   46 9.282803e-04
##          Micromesistius australis   46 9.282803e-04
##                    Pecten maximus   46 9.282803e-04
##             Tetrapturus pfluegeri   46 9.282803e-04
##                Cerastoderma edule   45 9.081003e-04
##                  Chirocentrus spp   45 9.081003e-04
##                 Mallotus villosus   45 9.081003e-04
##                  Scomberoides spp   45 9.081003e-04
##                Thunnus orientalis   45 9.081003e-04
##           Macruronus magellanicus   44 8.879202e-04
##                Pagellus bogaraveo   44 8.879202e-04
##                      Rhinobatidae   44 8.879202e-04
##                   Rutilus rutilus   44 8.879202e-04
##                     Echinodermata   43 8.677402e-04
##                     Holocentridae   43 8.677402e-04
##      Plectorhinchus mediterraneus   43 8.677402e-04
##                Pomadasys jubelini   43 8.677402e-04
##                   Dosidicus gigas   42 8.475602e-04
##                Illex illecebrosus   42 8.475602e-04
##                 Palinurus elephas   42 8.475602e-04
##                Euthynnus lineatus   41 8.273802e-04
##                  Scyliorhinus spp   41 8.273802e-04
##                    Tetraodontidae   41 8.273802e-04
##                Cyclopterus lumpus   40 8.072002e-04
##                     Cynoscion spp   40 8.072002e-04
##                        Gempylidae   40 8.072002e-04
##                 Harpadon nehereus   40 8.072002e-04
##                   Ilisha africana   40 8.072002e-04
##                   Metapenaeus spp   40 8.072002e-04
##         Mytilus galloprovincialis   40 8.072002e-04
##               Penaeus merguiensis   40 8.072002e-04
##          Pseudotolithus elongatus   40 8.072002e-04
##                     Abramis brama   39 7.870202e-04
##                   Clupea pallasii   39 7.870202e-04
##                Epinephelus aeneus   39 7.870202e-04
##                        Muraenidae   39 7.870202e-04
##                  Sebastes marinus   39 7.870202e-04
##                   Seriola lalandi   39 7.870202e-04
##                       Raja naevus   38 7.668402e-04
##                       Scyllaridae   38 7.668402e-04
##             Balistes carolinensis   37 7.466602e-04
##           Carcharhinus longimanus   37 7.466602e-04
##             Dentex macrophthalmus   37 7.466602e-04
##                Limanda ferruginea   37 7.466602e-04
##                         Mytilidae   37 7.466602e-04
##                Stromateus fiatola   37 7.466602e-04
##         Argyrosomus hololepidotus   36 7.264802e-04
##                 Galeocerdo cuvier   36 7.264802e-04
##                 Merluccius hubbsi   36 7.264802e-04
##                    Raja brachyura   36 7.264802e-04
##                     Raja montagui   36 7.264802e-04
##                   Sphyrna zygaena   36 7.264802e-04
##                   Aphanopus carbo   35 7.063002e-04
##                Aspitrigla cuculus   35 7.063002e-04
##                  Chamelea gallina   35 7.063002e-04
##                 Crassostrea gigas   35 7.063002e-04
##               Muraenesox cinereus   35 7.063002e-04
##                   Pagellus acarne   35 7.063002e-04
##            Pentanemus quinquarius   35 7.063002e-04
##                  Psettodes erumei   35 7.063002e-04
##                  Rastrelliger spp   35 7.063002e-04
##                  Tenualosa ilisha   35 7.063002e-04
##             Theragra chalcogramma   35 7.063002e-04
##                    Thyrsites atun   35 7.063002e-04
##                         Gerreidae   34 6.861202e-04
##                        Phycis spp   34 6.861202e-04
##             Scyliorhinus canicula   34 6.861202e-04
##     Selachimorpha (Pleurotremata)   34 6.861202e-04
##                   Selene dorsalis   34 6.861202e-04
##                   Stolephorus spp   34 6.861202e-04
##                     Auxis thazard   33 6.659402e-04
##                Salilota australis   33 6.659402e-04
##                       Salmonoidei   33 6.659402e-04
##                 Dicentrarchus spp   32 6.457602e-04
##               Orcynopsis unicolor   32 6.457602e-04
##              Ruditapes decussatus   32 6.457602e-04
##                         Veneridae   32 6.457602e-04
##                   Carcinus maenas   31 6.255802e-04
##                Chimaera monstrosa   31 6.255802e-04
##               Lactarius lactarius   31 6.255802e-04
##                 Lutjanus synagris   31 6.255802e-04
##                      Myliobatidae   31 6.255802e-04
##                 Palaemon serratus   31 6.255802e-04
##               Trisopterus minutus   31 6.255802e-04
##              Xiphopenaeus kroyeri   31 6.255802e-04
##               Callinectes sapidus   30 6.054002e-04
##           Centrophorus granulosus   30 6.054002e-04
##           Chelidonichthys lucerna   30 6.054002e-04
##               Coregonus lavaretus   30 6.054002e-04
##                        Dasyatidae   30 6.054002e-04
##               Decapterus russelli   30 6.054002e-04
##           Dicentrarchus punctatus   30 6.054002e-04
##                         Donax spp   30 6.054002e-04
##       Eleutheronema tetradactylum   30 6.054002e-04
##                        Ephippidae   30 6.054002e-04
##               Gadus macrocephalus   30 6.054002e-04
##                 Galeus melastomus   30 6.054002e-04
##                     Leiognathidae   30 6.054002e-04
##                       Loligo gahi   30 6.054002e-04
##                Lutjanus purpureus   30 6.054002e-04
##                    Pagrus auratus   30 6.054002e-04
##       Pseudotolithus senegalensis   30 6.054002e-04
##              Sardinella longiceps   30 6.054002e-04
##              Scomberomorus sierra   30 6.054002e-04
##                   Sepia pharaonis   30 6.054002e-04
##              Trisopterus esmarkii   30 6.054002e-04
##              Dicologlossa cuneata   29 5.852202e-04
##              Merluccius australis   29 5.852202e-04
##                    Squilla mantis   29 5.852202e-04
##              Todarodes sagittatus   29 5.852202e-04
##                   Urophycis chuss   29 5.852202e-04
##                     Littorina spp   28 5.650402e-04
##               Umbrina canariensis   28 5.650402e-04
##               Aristeus antennatus   27 5.448602e-04
##                     Caranx crysos   27 5.448602e-04
##                      Haliotis spp   27 5.448602e-04
##           Merluccius senegalensis   27 5.448602e-04
##          Oncorhynchus tshawytscha   27 5.448602e-04
##               Opisthonema oglinum   27 5.448602e-04
##             Alopias superciliosus   26 5.246801e-04
##                    Centrolophidae   26 5.246801e-04
##                 Mustelus mustelus   26 5.246801e-04
##                         Percoidei   26 5.246801e-04
##           Aequipecten opercularis   25 5.045001e-04
##                     Albula vulpes   25 5.045001e-04
##                   Anadara granosa   25 5.045001e-04
##                  Anarhichas minor   25 5.045001e-04
##            Anodontostoma chacunda   25 5.045001e-04
##                 Argyrops spinifer   25 5.045001e-04
##            Ginglymostoma cirratum   25 5.045001e-04
##                Lophius americanus   25 5.045001e-04
##         Macruronus novaezelandiae   25 5.045001e-04
##  Merluccius capensis, M.paradoxus   25 5.045001e-04
##                      Nemipteridae   25 5.045001e-04
##            Oncorhynchus gorbuscha   25 5.045001e-04
##                  Penaeus notialis   25 5.045001e-04
##              Penaeus semisulcatus   25 5.045001e-04
##                   Pogonias cromis   25 5.045001e-04
##                        Raja batis   25 5.045001e-04
##        Scomberomorus brasiliensis   25 5.045001e-04
##                       Sergestidae   25 5.045001e-04
##                         Solen spp   25 5.045001e-04
##                     Tylosurus spp   25 5.045001e-04
##                   Umbrina cirrosa   25 5.045001e-04
##                 Zoarces viviparus   25 5.045001e-04
##                        Asteroidea   24 4.843201e-04
##                     Caranx hippos   24 4.843201e-04
##              Cepola macrophthalma   24 4.843201e-04
##                     Elops lacerta   24 4.843201e-04
##               Epigonus telescopus   24 4.843201e-04
##                  Lampris guttatus   24 4.843201e-04
##               Macrourus carinatus   24 4.843201e-04
##               Megalops atlanticus   24 4.843201e-04
##                  Muraenolepis spp   24 4.843201e-04
##                Pagellus bellottii   24 4.843201e-04
##                 Penaeus japonicus   24 4.843201e-04
##                        Rapana spp   24 4.843201e-04
##                    Sphyrna lewini   24 4.843201e-04
##                 Thenus orientalis   24 4.843201e-04
##                          Bothidae   23 4.641401e-04
##                   Brotula barbata   23 4.641401e-04
##               Carassius carassius   23 4.641401e-04
##           Champsocephalus gunnari   23 4.641401e-04
##                   Channichthyidae   23 4.641401e-04
##                       Eledone spp   23 4.641401e-04
##                        Kyphosidae   23 4.641401e-04
##                   Raja circularis   23 4.641401e-04
##           Ruditapes philippinarum   23 4.641401e-04
##                  Sarda chiliensis   23 4.641401e-04
##         Squalidae, Scyliorhinidae   23 4.641401e-04
##                  Trachurus trecae   23 4.641401e-04
##            Centrophorus squamosus   22 4.439601e-04
##                    Etrumeus teres   22 4.439601e-04
##                 Hexanchus griseus   22 4.439601e-04
##                Littorina littorea   22 4.439601e-04
##                       Macrouridae   22 4.439601e-04
##                 Oncorhynchus keta   22 4.439601e-04
##                    Raja fullonica   22 4.439601e-04
##                  Sarda orientalis   22 4.439601e-04
##                   Sebastes alutus   22 4.439601e-04
##                    Solea lascaris   22 4.439601e-04
##               Sphyraena sphyraena   22 4.439601e-04
##                     Spicara maena   22 4.439601e-04
##                Anoplopoma fimbria   21 4.237801e-04
##          Centroscymnus coelolepis   21 4.237801e-04
##                        Cyprinidae   21 4.237801e-04
##              Epinephelus guttatus   21 4.237801e-04
##             Mercenaria mercenaria   21 4.237801e-04
##                      Raja radiata   21 4.237801e-04
##                         Reptantia   21 4.237801e-04
##                Sparisoma cretense   21 4.237801e-04
##                       Squatinidae   21 4.237801e-04
##         Acanthopagrus bifasciatus   20 4.036001e-04
##                     Alosa pontica   20 4.036001e-04
##           Cetengraulis mysticetus   20 4.036001e-04
##              Chelidonichthys kumu   20 4.036001e-04
##                  Chionoecetes spp   20 4.036001e-04
##                   Cololabis saira   20 4.036001e-04
##             Crassostrea virginica   20 4.036001e-04
##                Diplodus annularis   20 4.036001e-04
##                  Drepane punctata   20 4.036001e-04
##               Engraulis japonicus   20 4.036001e-04
##               Epinephelus tauvina   20 4.036001e-04
##                  Gaidropsarus spp   20 4.036001e-04
##                       Galatheidae   20 4.036001e-04
##             Gnathanodon speciosus   20 4.036001e-04
##                   Leiognathus spp   20 4.036001e-04
##               Lethrinus nebulosus   20 4.036001e-04
##                Menippe mercenaria   20 4.036001e-04
##              Merluccius productus   20 4.036001e-04
##            Micropogonias furnieri   20 4.036001e-04
##                    Muraenesox spp   20 4.036001e-04
##                         Murex spp   20 4.036001e-04
##                Oncorhynchus nerka   20 4.036001e-04
##        Paralithodes camtschaticus   20 4.036001e-04
##            Patagonotothen ramsayi   20 4.036001e-04
##                     Phycis phycis   20 4.036001e-04
##                   Platycephalidae   20 4.036001e-04
##              Pleurogrammus azonus   20 4.036001e-04
##                      Plotosus spp   20 4.036001e-04
##                   Raja oxyrinchus   20 4.036001e-04
##                    Saurida tumbil   20 4.036001e-04
##             Selaroides leptolepis   20 4.036001e-04
##               Trachurus japonicus   20 4.036001e-04
##   Xiphopenaeus, Trachypenaeus spp   20 4.036001e-04
##                Zenopsis nebulosus   20 4.036001e-04
##                 Alosa sapidissima   19 3.834201e-04
##              Ammodytes personatus   19 3.834201e-04
##                          Arca spp   19 3.834201e-04
##                Beryx decadactylus   19 3.834201e-04
##                     Harengula spp   19 3.834201e-04
##                        Isurus spp   19 3.834201e-04
##                Macrourus whitsoni   19 3.834201e-04
##                     Monacanthidae   19 3.834201e-04
##                      Mya arenaria   19 3.834201e-04
##                         Myxinidae   19 3.834201e-04
##              Oncorhynchus kisutch   19 3.834201e-04
##                       Ostraciidae   19 3.834201e-04
##                        Paphia spp   19 3.834201e-04
##                  Paralichthys spp   19 3.834201e-04
##                  Penaeus duorarum   19 3.834201e-04
##               Pomadasys argenteus   19 3.834201e-04
##                Raja microocellata   19 3.834201e-04
##                Uranoscopus scaber   19 3.834201e-04
##            Urophycis brasiliensis   19 3.834201e-04
##                       Vimba vimba   19 3.834201e-04
##                      Alosa fallax   18 3.632401e-04
##                   Caranx rhonchus   18 3.632401e-04
##             Carcharhinus limbatus   18 3.632401e-04
##               Centroberyx affinis   18 3.632401e-04
##                   Cyprinus carpio   18 3.632401e-04
##                    Dalatias licha   18 3.632401e-04
##                     Deania calcea   18 3.632401e-04
##                   Illex coindetii   18 3.632401e-04
##                           Moridae   18 3.632401e-04
##              Penaeus brevirostris   18 3.632401e-04
##                      Portunus spp   18 3.632401e-04
##               Pseudocaranx dentex   18 3.632401e-04
##                         Raja alba   18 3.632401e-04
##                    Raja georgiana   18 3.632401e-04
##               Venerupis pullastra   18 3.632401e-04
##                Zenopsis conchifer   18 3.632401e-04
##                   Callista chione   17 3.430601e-04
##              Eleginops maclovinus   17 3.430601e-04
##                      Elops saurus   17 3.430601e-04
##          Hemiramphus brasiliensis   17 3.430601e-04
##                        Lithodidae   17 3.430601e-04
##                 Micropogonias spp   17 3.430601e-04
##                    Muraena helena   17 3.430601e-04
##                 Myliobatis aquila   17 3.430601e-04
##           Patinopecten yessoensis   17 3.430601e-04
##                        Polychaeta   17 3.430601e-04
##                     Scolopsis spp   17 3.430601e-04
##                Scomberesox saurus   17 3.430601e-04
##                   Atherina boyeri   16 3.228801e-04
##                       Calamus spp   16 3.228801e-04
##               Campogramma glaycos   16 3.228801e-04
##                       Capros aper   16 3.228801e-04
##         Lutjanus argentimaculatus   16 3.228801e-04
##                         Mora moro   16 3.228801e-04
##              Muraenolepis microps   16 3.228801e-04
##                       Myctophidae   16 3.228801e-04
##                      Necora puber   16 3.228801e-04
##             Opisthonema libertate   16 3.228801e-04
##                    Osmerus mordax   16 3.228801e-04
##                         Pristidae   16 3.228801e-04
##                   Pteroscion peli   16 3.228801e-04
##           Sardinops melanostictus   16 3.228801e-04
##             Scomber australasicus   16 3.228801e-04
##            Scyliorhinus stellaris   16 3.228801e-04
##                 Scyllarides latus   16 3.228801e-04
##                Trachurus capensis   16 3.228801e-04
##               Acanthopagrus latus   15 3.027001e-04
##              Alectis alexandrinus   15 3.027001e-04
##                    Arripis trutta   15 3.027001e-04
##               Atheresthes stomias   15 3.027001e-04
##           Bregmaceros mcclellandi   15 3.027001e-04
##                   Cancer magister   15 3.027001e-04
##                  Caranx ignobilis   15 3.027001e-04
##                      Caranx ruber   15 3.027001e-04
##           Carcharhinus brachyurus   15 3.027001e-04
##                Carcinus aestuarii   15 3.027001e-04
##               Cephalopholis fulva   15 3.027001e-04
##                  Cheimerius nufar   15 3.027001e-04
##               Chionoecetes opilio   15 3.027001e-04
##                Chirocentrus dorab   15 3.027001e-04
##                          Cottidae   15 3.027001e-04
##               Cynoscion nebulosus   15 3.027001e-04
##                 Dussumieria acuta   15 3.027001e-04
##                  Engraulis mordax   15 3.027001e-04
##              Epinephelus coioides   15 3.027001e-04
##           Hippoglossus stenolepis   15 3.027001e-04
##            Larimichthys polyactis   15 3.027001e-04
##                          Latridae   15 3.027001e-04
##                 Lethrinus lentjan   15 3.027001e-04
##                  Lutjanus griseus   15 3.027001e-04
##                Macrodon ancylodon   15 3.027001e-04
##              Megalops cyprinoides   15 3.027001e-04
##                     Mene maculata   15 3.027001e-04
##            Metapenaeus endeavouri   15 3.027001e-04
##                  Nemadactylus spp   15 3.027001e-04
##            Notorynchus cepedianus   15 3.027001e-04
##            Notothenia squamifrons   15 3.027001e-04
##                Ophiodon elongatus   15 3.027001e-04
##        Osmerus spp, Hypomesus spp   15 3.027001e-04
##                   Otolithes ruber   15 3.027001e-04
##                       Palinuridae   15 3.027001e-04
##                Panulirus longipes   15 3.027001e-04
##                  Pellona ditchela   15 3.027001e-04
##                   Penaeus aztecus   15 3.027001e-04
##                 Penaeus setiferus   15 3.027001e-04
##                     Perna viridis   15 3.027001e-04
##          Portunus trituberculatus   15 3.027001e-04
##          Priacanthus macracanthus   15 3.027001e-04
##                     Prionotus spp   15 3.027001e-04
##           Rastrelliger brachysoma   15 3.027001e-04
##                    Rexea solandri   15 3.027001e-04
##               Sardinops caeruleus   15 3.027001e-04
##      Scomberoides commersonnianus   15 3.027001e-04
##          Scomberomorus lineolatus   15 3.027001e-04
##           Scomberomorus maculatus   15 3.027001e-04
##           Scomberomorus niphonius   15 3.027001e-04
##                    Scyliorhinidae   15 3.027001e-04
##                    Sillago sihama   15 3.027001e-04
##               Sphyraena barracuda   15 3.027001e-04
##                   Sphyraena jello   15 3.027001e-04
##                       Stomatopoda   15 3.027001e-04
##                       Terapon spp   15 3.027001e-04
##                       Tinca tinca   15 3.027001e-04
##               Todarodes pacificus   15 3.027001e-04
##                       Torpedo spp   15 3.027001e-04
##             Trachurus symmetricus   15 3.027001e-04
##        Trachypenaeus curvirostris   15 3.027001e-04
##                   Umbrina canosai   15 3.027001e-04
##                       Anadara spp   14 2.825201e-04
##                         Cardiidae   14 2.825201e-04
##                   Chaceon maritae   14 2.825201e-04
##                 Engraulis ringens   14 2.825201e-04
##               Gymnosarda unicolor   14 2.825201e-04
##                  Merluccius polli   14 2.825201e-04
##                         Mola mola   14 2.825201e-04
##                  Morone saxatilis   14 2.825201e-04
##                      Pandalus spp   14 2.825201e-04
##                  Pecten jacobaeus   14 2.825201e-04
##            Penaeus californiensis   14 2.825201e-04
##           Rhomboplites aurorubens   14 2.825201e-04
##               Sardinops ocellatus   14 2.825201e-04
##                 Scymnodon ringens   14 2.825201e-04
##                 Squatina squatina   14 2.825201e-04
##                 Arctica islandica   13 2.623401e-04
##               Argentina sphyraena   13 2.623401e-04
##                    Aulacomya ater   13 2.623401e-04
##                 Bathyraja eatonii   13 2.623401e-04
##                   Brama australis   13 2.623401e-04
##        Callorhinchus callorynchus   13 2.623401e-04
##           Chionobathyscus dewitti   13 2.623401e-04
##                Chirocentrus nudus   13 2.623401e-04
##                Conger orbignyanus   13 2.623401e-04
##                Dasyatis pastinaca   13 2.623401e-04
##              Epinephelus striatus   13 2.623401e-04
##              Girella tricuspidata   13 2.623401e-04
##                   Labrus bergylta   13 2.623401e-04
##              Lachnolaimus maximus   13 2.623401e-04
##                 Lophius vomerinus   13 2.623401e-04
##             Merluccius bilinearis   13 2.623401e-04
##                Moroteuthis ingens   13 2.623401e-04
##                Panulirus gracilis   13 2.623401e-04
##                  Penaeus vannamei   13 2.623401e-04
##        Plesiopenaeus edwardsianus   13 2.623401e-04
##                     Sciaena umbra   13 2.623401e-04
##                 Selene setapinnis   13 2.623401e-04
##                  Seriolella brama   13 2.623401e-04
##               Seriolella punctata   13 2.623401e-04
##                 Serranus cabrilla   13 2.623401e-04
##                         Solenidae   13 2.623401e-04
##                Tetrapturus belone   13 2.623401e-04
##          Centroscymnus crepidater   12 2.421601e-04
##                   Chaceon affinis   12 2.421601e-04
##                 Chlamys islandica   12 2.421601e-04
##                  Cottoperca gobio   12 2.421601e-04
##                  Cynoscion analis   12 2.421601e-04
##                 Diplodus vulgaris   12 2.421601e-04
##                 Lithodes santolla   12 2.421601e-04
##              Lobotes surinamensis   12 2.421601e-04
##                   Loligo vulgaris   12 2.421601e-04
##                   Merluccius gayi   12 2.421601e-04
##                      Mugil curema   12 2.421601e-04
##             Paracentrotus lividus   12 2.421601e-04
##              Penaeus latisulcatus   12 2.421601e-04
##                Petromyzon marinus   12 2.421601e-04
##             Pomacanthus maculosus   12 2.421601e-04
##         Pseudopercis semifasciata   12 2.421601e-04
##              Rhabdosargus haffara   12 2.421601e-04
##               Saurida undosquamis   12 2.421601e-04
##                       Scomber spp   12 2.421601e-04
##                 Sparidentex hasta   12 2.421601e-04
##            Zygochlamys patagonica   12 2.421601e-04
##             Alepocephalus bairdii   11 2.219801e-04
##                   Argentina silus   11 2.219801e-04
##                 Aristeus varidens   11 2.219801e-04
##                   Beryx splendens   11 2.219801e-04
##                Cetorhinus maximus   11 2.219801e-04
##                  Coregonus albula   11 2.219801e-04
##           Crassostrea rhizophorae   11 2.219801e-04
##                 Epinephelus morio   11 2.219801e-04
##                 Etmopterus spinax   11 2.219801e-04
##                    Etmopterus spp   11 2.219801e-04
##            Gasterosteus aculeatus   11 2.219801e-04
##                    Hydrolagus spp   11 2.219801e-04
##           Hyperoglyphe antarctica   11 2.219801e-04
##                     Isurus paucus   11 2.219801e-04
##              Lethrinus atlanticus   11 2.219801e-04
##                    Leuciscus idus   11 2.219801e-04
##                 Loligo opalescens   11 2.219801e-04
##               Oncorhynchus mykiss   11 2.219801e-04
##        Oreochromis (=Tilapia) spp   11 2.219801e-04
##               Paralomis granulosa   11 2.219801e-04
##                     Peprilus paru   11 2.219801e-04
##            Plectorhinchus schotaf   11 2.219801e-04
##         Pseudotolithus senegallus   11 2.219801e-04
##                    Spisula solida   11 2.219801e-04
##              Squatina californica   11 2.219801e-04
##             Trachipterus arcticus   11 2.219801e-04
##                 Trachurus lathami   11 2.219801e-04
##                       Abramis spp   10 2.018001e-04
##               Acanthopagrus berda   10 2.018001e-04
##                  Acetes japonicus   10 2.018001e-04
##                    Alepes djedaba   10 2.018001e-04
##                       Alosa alosa   10 2.018001e-04
##              Alosa pseudoharengus   10 2.018001e-04
##                  Amblygaster sirm   10 2.018001e-04
##                      Anchoa nasus   10 2.018001e-04
##       Archosargus probatocephalus   10 2.018001e-04
##             Arctoscopus japonicus   10 2.018001e-04
##                    Ariomma indica   10 2.018001e-04
##           Aristaeomorpha foliacea   10 2.018001e-04
##                 Arius thalassinus   10 2.018001e-04
##                     Aspius aspius   10 2.018001e-04
##            Atractoscion aequidens   10 2.018001e-04
##          Austroglossus microlepis   10 2.018001e-04
##                    Batrachoididae   10 2.018001e-04
##                   Blicca bjoerkna   10 2.018001e-04
##                  Boreogadus saida   10 2.018001e-04
##                  Brevoortia aurea   10 2.018001e-04
##               Brevoortia tyrannus   10 2.018001e-04
##                       Busycon spp   10 2.018001e-04
##               Callorhinchus milii   10 2.018001e-04
##                  Cancer irroratus   10 2.018001e-04
##                  Cancer productus   10 2.018001e-04
##       Cantherhines (=Navodon) spp   10 2.018001e-04
##                 Carangoides bajad   10 2.018001e-04
##           Carangoides malabaricus   10 2.018001e-04
##             Caulolatilus princeps   10 2.018001e-04
##           Centropomus undecimalis   10 2.018001e-04
##             Centropristis striata   10 2.018001e-04
##              Cephalopholis boenak   10 2.018001e-04
##           Chaenocephalus aceratus   10 2.018001e-04
##               Cheilinus undulatus   10 2.018001e-04
##              Cheilodactylus bergi   10 2.018001e-04
##         Cheilodactylus variegatus   10 2.018001e-04
##                 Chrysoblephus spp   10 2.018001e-04
##                    Cilus gilberti   10 2.018001e-04
##                        Citharidae   10 2.018001e-04
##                Clupanodon thrissa   10 2.018001e-04
##         Clupeonella cultriventris   10 2.018001e-04
##           Concholepas concholepas   10 2.018001e-04
##                   Conodon nobilis   10 2.018001e-04
##                     Coregonus spp   10 2.018001e-04
##             Cromileptes altivelis   10 2.018001e-04
##                Cymatoceps nasutus   10 2.018001e-04
##                 Cynoscion regalis   10 2.018001e-04
##                Cynoscion striatus   10 2.018001e-04
##               Decapterus maruadsi   10 2.018001e-04
##                  Eledone cirrhosa   10 2.018001e-04
##              Emmelichthys nitidus   10 2.018001e-04
##                Engraulis capensis   10 2.018001e-04
##                  Eopsetta jordani   10 2.018001e-04
##                 Epinephelus merra   10 2.018001e-04
##               Ethmidium maculatum   10 2.018001e-04
##               Genypterus capensis   10 2.018001e-04
##                      Gerres oyena   10 2.018001e-04
##             Glycymeris glycymeris   10 2.018001e-04
##           Glyptocephalus zachirus   10 2.018001e-04
##                  Gymnocranius spp   10 2.018001e-04
##                    Haliotis rubra   10 2.018001e-04
##           Haliporoides triarthrus   10 2.018001e-04
##                Homarus americanus   10 2.018001e-04
##               Isacia conceptionis   10 2.018001e-04
##                    Jasus lalandii   10 2.018001e-04
##                   Jasus verreauxi   10 2.018001e-04
##                          Lamnidae   10 2.018001e-04
##              Larimichthys croceus   10 2.018001e-04
##             Lateolabrax japonicus   10 2.018001e-04
##              Leiostomus xanthurus   10 2.018001e-04
##            Lepidopsetta bilineata   10 2.018001e-04
##                 Lepidorhombus spp   10 2.018001e-04
##              Lethrinus borbonicus   10 2.018001e-04
##                 Lethrinus mahsena   10 2.018001e-04
##                Lethrinus microdon   10 2.018001e-04
##                Limulus polyphemus   10 2.018001e-04
##                  Liza klunzingeri   10 2.018001e-04
##     Lopholatilus chamaeleonticeps   10 2.018001e-04
##           Lutjanus argentiventris   10 2.018001e-04
##              Lutjanus campechanus   10 2.018001e-04
##                 Lutjanus guttatus   10 2.018001e-04
##              Lutjanus malabaricus   10 2.018001e-04
##              Malacanthus plumieri   10 2.018001e-04
##                   Menidia menidia   10 2.018001e-04
##           Menticirrhus littoralis   10 2.018001e-04
##                      Meretrix spp   10 2.018001e-04
##                   Microchirus spp   10 2.018001e-04
##           Micropogonias undulatus   10 2.018001e-04
##             Microstomus pacificus   10 2.018001e-04
##                         Mobulidae   10 2.018001e-04
##                       Mugil soiuy   10 2.018001e-04
##              Mustelus antarcticus   10 2.018001e-04
##                 Mustelus schmitti   10 2.018001e-04
##                  Mycteroperca spp   10 2.018001e-04
##               Nototodarus sloanii   10 2.018001e-04
##                Oncorhynchus masou   10 2.018001e-04
##                   Panopea abrupta   10 2.018001e-04
##                 Paphies australis   10 2.018001e-04
##            Paralichthys olivaceus   10 2.018001e-04
##                 Penaeus chinensis   10 2.018001e-04
##                Pennahia argentata   10 2.018001e-04
##            Percophis brasiliensis   10 2.018001e-04
##          Placopecten magellanicus   10 2.018001e-04
##                        Platax spp   10 2.018001e-04
##             Platycephalus indicus   10 2.018001e-04
##                Plectorhinchus spp   10 2.018001e-04
##            Plectropomus leopardus   10 2.018001e-04
##                Pleoticus robustus   10 2.018001e-04
##              Pleuronectes vetulus   10 2.018001e-04
##                Pomadasys stridens   10 2.018001e-04
##                Pristipomoides spp   10 2.018001e-04
##                 Psenopsis anomala   10 2.018001e-04
##        Psettichthys melanostictus   10 2.018001e-04
##     Pseudopleuronectes americanus   10 2.018001e-04
##          Pterygotrigla polyommata   10 2.018001e-04
##           Rhynchobatus australiae   10 2.018001e-04
##                Sardinella gibbosa   10 2.018001e-04
##                 Sardinella lemuru   10 2.018001e-04
##                   Sardinops sagax   10 2.018001e-04
##               Saxidomus giganteus   10 2.018001e-04
##             Scomberomorus regalis   10 2.018001e-04
##        Scorpaenichthys marmoratus   10 2.018001e-04
##                Sebastes entomelas   10 2.018001e-04
##                 Sebastes flavidus   10 2.018001e-04
##                   Sebastes goodei   10 2.018001e-04
##              Sebastes paucispinis   10 2.018001e-04
##                 Sebastes pinniger   10 2.018001e-04
##            Sebastolobus alascanus   10 2.018001e-04
##           Sepioteuthis lessoniana   10 2.018001e-04
##                 Seriola rivoliana   10 2.018001e-04
##                    Seriolella spp   10 2.018001e-04
##           Seriolina nigrofasciata   10 2.018001e-04
##               Spisula solidissima   10 2.018001e-04
##                Squatina argentina   10 2.018001e-04
##                        Squillidae   10 2.018001e-04
##               Stichopus japonicus   10 2.018001e-04
##                    Tenualosa toli   10 2.018001e-04
##                   Trachichthyidae   10 2.018001e-04
##             Trachinotus carolinus   10 2.018001e-04
##                     Trachinus spp   10 2.018001e-04
##                Trachurus declivis   10 2.018001e-04
##                 Trochus niloticus   10 2.018001e-04
##                    Turbo cornutus   10 2.018001e-04
##                  Valamugil seheli   10 2.018001e-04
##                     Variola louti   10 2.018001e-04
##          Acanthistius brasilianus    9 1.816201e-04
##                     Acipenseridae    9 1.816201e-04
##           Anarhichas denticulatus    9 1.816201e-04
##            Carcharodon carcharias    9 1.816201e-04
##          Centrophorus lusitanicus    9 1.816201e-04
##           Centroscyllium fabricii    9 1.816201e-04
##             Chelon haematocheilus    9 1.816201e-04
##                    Chimaeriformes    9 1.816201e-04
##                Diplodus argenteus    9 1.816201e-04
##                      Epigonus spp    9 1.816201e-04
##                   Ilisha elongata    9 1.816201e-04
##                       Liza aurata    9 1.816201e-04
##                   Lutjanus analis    9 1.816201e-04
##                 Martialia hyadesi    9 1.816201e-04
##                  Menticirrhus spp    9 1.816201e-04
##             Metapenaeus monoceros    9 1.816201e-04
##                  Naucrates ductor    9 1.816201e-04
##                     Oreosomatidae    9 1.816201e-04
##                      Palaemonidae    9 1.816201e-04
##             Paralichthys dentatus    9 1.816201e-04
##                  Paralithodes spp    9 1.816201e-04
##                    Parona signata    9 1.816201e-04
##                 Pelecus cultratus    9 1.816201e-04
##              Penaeus occidentalis    9 1.816201e-04
##             Plectorhinchus pictus    9 1.816201e-04
##         Promethichthys prometheus    9 1.816201e-04
##     Pseudochaenichthys georgianus    9 1.816201e-04
##             Pterogymnus laniarius    9 1.816201e-04
##        Rhizoprionodon terraenovae    9 1.816201e-04
##                     Ruditapes spp    9 1.816201e-04
##           Somniosus microcephalus    9 1.816201e-04
##                Sprattus fuegensis    9 1.816201e-04
##                      Aphia minuta    8 1.614400e-04
##                Bothus pantherinus    8 1.614400e-04
##                          Bramidae    8 1.614400e-04
##             Centrolabrus exoletus    8 1.614400e-04
##          Chelidonichthys capensis    8 1.614400e-04
##                   Chelon labrosus    8 1.614400e-04
##            Dactylopterus volitans    8 1.614400e-04
##                  Diagramma pictum    8 1.614400e-04
##                   Gerres oblongus    8 1.614400e-04
##                  Gymnura altavela    8 1.614400e-04
##                Hydrolagus colliei    8 1.614400e-04
##                   Miichthys miiuy    8 1.614400e-04
##                        Mugil liza    8 1.614400e-04
##                 Mustelus asterias    8 1.614400e-04
##                   Mustelus henlei    8 1.614400e-04
##                 Mytilus platensis    8 1.614400e-04
##          Orthopristis chrysoptera    8 1.614400e-04
##                Pleoticus muelleri    8 1.614400e-04
##              Polyprion oxygeneios    8 1.614400e-04
##            Pseudocardium sybillae    8 1.614400e-04
##      Pseudopentaceros richardsoni    8 1.614400e-04
##                     Raja undulata    8 1.614400e-04
##              Schedophilus pemarco    8 1.614400e-04
##              Schedophilus velaini    8 1.614400e-04
##                  Scorpaena scrofa    8 1.614400e-04
##                  Zidona dufresnei    8 1.614400e-04
##                    Ablennes hians    7 1.412600e-04
##                 Alepocephalus spp    7 1.412600e-04
##              Argopecten irradians    7 1.412600e-04
##              Artemesia longinaris    7 1.412600e-04
##                    Artemia salina    7 1.412600e-04
##                 Carcharias taurus    7 1.412600e-04
##              Champsocephalus esox    7 1.412600e-04
##                 Dentex angolensis    7 1.412600e-04
##                 Dentex congoensis    7 1.412600e-04
##              Haliotis tuberculata    7 1.412600e-04
##                  Joturus pichardi    7 1.412600e-04
##              Lepidorhombus boscii    7 1.412600e-04
##                    Lutjanus bohar    7 1.412600e-04
##           Macroramphosus scolopax    7 1.412600e-04
##                  Metanephrops spp    7 1.412600e-04
##                  Nematalosa nasus    7 1.412600e-04
##                  Pandalus jordani    7 1.412600e-04
##         Paralichthys californicus    7 1.412600e-04
##              Penaeus stylirostris    7 1.412600e-04
##            Pogonophryne permitini    7 1.412600e-04
##                     Raja asterias    7 1.412600e-04
##                         Raja taaf    7 1.412600e-04
##                Allothunnus fallai    6 1.210800e-04
##                    Anadara ovalis    6 1.210800e-04
##             Argopecten purpuratus    6 1.210800e-04
##                        Aristeidae    6 1.210800e-04
##          Austroglossus pectoralis    6 1.210800e-04
##               Carcharhinus leucas    6 1.210800e-04
##             Carcharhinus plumbeus    6 1.210800e-04
##              Caulolatilus microps    6 1.210800e-04
##                  Chaceon notialis    6 1.210800e-04
##                       Chaceon spp    6 1.210800e-04
##                Echinus esculentus    6 1.210800e-04
##                Engraulis anchoita    6 1.210800e-04
##             Epinephelus goreensis    6 1.210800e-04
##             Epinephelus polylepis    6 1.210800e-04
##               Etrumeus whiteheadi    6 1.210800e-04
##         Eucinostomus melanopterus    6 1.210800e-04
##                        Gadus ogac    6 1.210800e-04
##        Hoplostethus mediterraneus    6 1.210800e-04
##                         Lophiidae    6 1.210800e-04
##                 Lophius budegassa    6 1.210800e-04
##                  Lutjanus vivanus    6 1.210800e-04
##               Maurolicus muelleri    6 1.210800e-04
##                Mesodesma donacium    6 1.210800e-04
##                    Mustelus canis    6 1.210800e-04
##               Mycteroperca bonaci    6 1.210800e-04
##                 Mytilus chilensis    6 1.210800e-04
##            Neocyttus rhomboidalis    6 1.210800e-04
##           Notothenia gibberifrons    6 1.210800e-04
##                 Notothenia rossii    6 1.210800e-04
##            Nototheniops nudifrons    6 1.210800e-04
##             Ommastrephes bartrami    6 1.210800e-04
##                        Ophidiidae    6 1.210800e-04
##            Palinurus mauritanicus    6 1.210800e-04
##            Paralomis spinosissima    6 1.210800e-04
##              Penaeus brasiliensis    6 1.210800e-04
##                  Petrus rupestris    6 1.210800e-04
##                 Pomadasys incisus    6 1.210800e-04
##            Pseudocyttus maculatus    6 1.210800e-04
##                   Raja hyperborea    6 1.210800e-04
##                           Rajidae    6 1.210800e-04
##                    Salvelinus spp    6 1.210800e-04
##           Sardinella brasiliensis    6 1.210800e-04
##               Schedophilus ovalis    6 1.210800e-04
##               Sciaenops ocellatus    6 1.210800e-04
##                Scomberoides lysan    6 1.210800e-04
##                Sphyraena obtusata    6 1.210800e-04
##           Acanthopagrus schlegeli    5 1.009000e-04
##                  Acanthurus sohal    5 1.009000e-04
##                 Acetes erythraeus    5 1.009000e-04
##             Acipenser medirostris    5 1.009000e-04
##           Acipenser transmontanus    5 1.009000e-04
##                Aethaloperca rogaa    5 1.009000e-04
##                  Allocyttus niger    5 1.009000e-04
##             Allocyttus verrucosus    5 1.009000e-04
##                        Ambassidae    5 1.009000e-04
##         Amphichthys cryptocentrus    5 1.009000e-04
##                 Aphareus rutilans    5 1.009000e-04
##            Aplodactylus punctatus    5 1.009000e-04
##                        Apogonidae    5 1.009000e-04
##                  Aprion virescens    5 1.009000e-04
##                    Apsilus fuscus    5 1.009000e-04
##                        Arca zebra    5 1.009000e-04
##          Archosargus rhomboidalis    5 1.009000e-04
##            Argopecten ventricosus    5 1.009000e-04
##             Argyrozona argyrozona    5 1.009000e-04
##                Arripis georgianus    5 1.009000e-04
##             Atheresthes evermanni    5 1.009000e-04
##              Atractoscion nobilis    5 1.009000e-04
##                    Atrobucca nibe    5 1.009000e-04
##                        Atule mate    5 1.009000e-04
##                 Austroglossus spp    5 1.009000e-04
##       Austromegabalanus psittacus    5 1.009000e-04
##                      Auxis rochei    5 1.009000e-04
##                 Babylonia spirata    5 1.009000e-04
##                  Bathyraja irrasa    5 1.009000e-04
##                 Bathyraja murrayi    5 1.009000e-04
##                  Benthodesmus spp    5 1.009000e-04
##               Benthosema pterotum    5 1.009000e-04
##             Berryteuthis magister    5 1.009000e-04
##            Bolbometopon muricatum    5 1.009000e-04
##               Brevoortia patronus    5 1.009000e-04
##                   Callianassa spp    5 1.009000e-04
##                 Callinectes danae    5 1.009000e-04
##            Callorhinchus capensis    5 1.009000e-04
##                   Cancer borealis    5 1.009000e-04
##                  Cancer edwardsii    5 1.009000e-04
##               Caprodon longimanus    5 1.009000e-04
##         Carangoides fulvoguttatus    5 1.009000e-04
##                 Caranx melampygus    5 1.009000e-04
##               Caranx sexfasciatus    5 1.009000e-04
##                 Carassius auratus    5 1.009000e-04
##               Carcharhinus sorrah    5 1.009000e-04
##             Centriscops humerosus    5 1.009000e-04
##               Cephalopholis argus    5 1.009000e-04
##         Cephalopholis hemistiktos    5 1.009000e-04
##             Cephalopholis miniata    5 1.009000e-04
##         Cephaloscyllium isabellum    5 1.009000e-04
##                 Cervimunida johni    5 1.009000e-04
##            Cetengraulis edentulus    5 1.009000e-04
##                   Chaceon fenneri    5 1.009000e-04
##               Chaceon quinquedens    5 1.009000e-04
##         Channichthys rhinoceratus    5 1.009000e-04
##                     Charybdis spp    5 1.009000e-04
##         Chelidonichthys lastoviza    5 1.009000e-04
##                Chione stutchburyi    5 1.009000e-04
##            Chionoecetes japonicus    5 1.009000e-04
##            Chloroscombrus orqueta    5 1.009000e-04
##               Choromytilus chorus    5 1.009000e-04
##            Citharichthys sordidus    5 1.009000e-04
##            Clinocardium nuttallii    5 1.009000e-04
##            Coelorinchus chilensis    5 1.009000e-04
##                  Conger myriaster    5 1.009000e-04
##                  Conger oceanicus    5 1.009000e-04
##                       Crangonidae    5 1.009000e-04
##              Crassostrea iredalei    5 1.009000e-04
##               Crenidens crenidens    5 1.009000e-04
##             Ctenolabrus rupestris    5 1.009000e-04
##                       Cymbium spp    5 1.009000e-04
##             Cynoponticus coniceps    5 1.009000e-04
##                  Cynoscion acoupa    5 1.009000e-04
##               Cynoscion arenarius    5 1.009000e-04
##               Cynoscion guatucupa    5 1.009000e-04
##             Cynoscion jamaicensis    5 1.009000e-04
##               Cynoscion leiarchus    5 1.009000e-04
##               Cynoscion virescens    5 1.009000e-04
##                   Cyttus traversi    5 1.009000e-04
##                Dasyatis americana    5 1.009000e-04
##                Deania profundorum    5 1.009000e-04
##              Decapterus macrosoma    5 1.009000e-04
##                 Diapterus auratus    5 1.009000e-04
##           Diastobranchus capensis    5 1.009000e-04
##                 Diplodus puntazzo    5 1.009000e-04
##              Dipturus innominatus    5 1.009000e-04
##            Dussumieria elopsoides    5 1.009000e-04
##                 Eleginus gracilis    5 1.009000e-04
##                   Eleginus navaga    5 1.009000e-04
##          Encrasicholina punctifer    5 1.009000e-04
##                    Ensis directus    5 1.009000e-04
##             Epinephelus areolatus    5 1.009000e-04
##               Epinephelus caninus    5 1.009000e-04
##          Epinephelus chlorostigma    5 1.009000e-04
##             Epinephelus fasciatus    5 1.009000e-04
##         Epinephelus flavolimbatus    5 1.009000e-04
##         Epinephelus fuscoguttatus    5 1.009000e-04
##               Epinephelus morrhua    5 1.009000e-04
##          Epinephelus multinotatus    5 1.009000e-04
##            Epinephelus mystacinus    5 1.009000e-04
##              Epinephelus nigritus    5 1.009000e-04
##              Epinephelus niveatus    5 1.009000e-04
##               Epinephelus summana    5 1.009000e-04
##              Eptatretus cirrhatus    5 1.009000e-04
##              Erimacrus isenbeckii    5 1.009000e-04
##                Fistularia corneta    5 1.009000e-04
##               Gadiculus argenteus    5 1.009000e-04
##            Gasterochisma melampus    5 1.009000e-04
##               Genyonemus lineatus    5 1.009000e-04
##              Genypterus chilensis    5 1.009000e-04
##              Genypterus maculatus    5 1.009000e-04
##                    Genypterus spp    5 1.009000e-04
##                      Gerres nigri    5 1.009000e-04
##                   Geryon longipes    5 1.009000e-04
##                 Girella nigricans    5 1.009000e-04
##         Glossanodon semifasciatus    5 1.009000e-04
##           Grammoplites suppositus    5 1.009000e-04
##            Gymnoscopelus nicholsi    5 1.009000e-04
##                Haemulon plumierii    5 1.009000e-04
##                      Haemulon spp    5 1.009000e-04
##                 Haliotis gigantea    5 1.009000e-04
##            Haliporoides diomedeae    5 1.009000e-04
##                 Hemiramphus balao    5 1.009000e-04
##    Herklotsichthys quadrimaculat.    5 1.009000e-04
##                Heterocarpus reedi    5 1.009000e-04
##           Hexagrammos decagrammus    5 1.009000e-04
##                Himantura gerrardi    5 1.009000e-04
##         Hippoglossoides elassodon    5 1.009000e-04
##             Holothuria fuscogilva    5 1.009000e-04
##                Holothuria nobilis    5 1.009000e-04
##                 Holothuria scabra    5 1.009000e-04
##                  Homalaspis plana    5 1.009000e-04
##            Hoplopagrus guentherii    5 1.009000e-04
##        Hydrolagus novaezealandiae    5 1.009000e-04
##             Hyperoglyphe bythites    5 1.009000e-04
##                   Ibacus ciliatus    5 1.009000e-04
##            Isopisthus parvipinnis    5 1.009000e-04
##                   Jasus edwardsii    5 1.009000e-04
##                   Jasus frontalis    5 1.009000e-04
##             Jasus novaehollandiae    5 1.009000e-04
##                   Jasus paulensis    5 1.009000e-04
##                    Jasus tristani    5 1.009000e-04
##            Kathetostoma giganteum    5 1.009000e-04
##               Konosirus punctatus    5 1.009000e-04
##                 Larimus breviceps    5 1.009000e-04
##             Lepidoperca pulchella    5 1.009000e-04
##       Lepidorhynchus denticulatus    5 1.009000e-04
##         Lepidotrigla brachyoptera    5 1.009000e-04
##           Leptomelanosoma indicum    5 1.009000e-04
##                   Lethrinus harak    5 1.009000e-04
##               Lethrinus obsoletus    5 1.009000e-04
##            Lethrinus xanthochilus    5 1.009000e-04
##                    Limanda aspera    5 1.009000e-04
##               Lithodes aequispina    5 1.009000e-04
##                      Liza saliens    5 1.009000e-04
##                    Loligo forbesi    5 1.009000e-04
##                    Loligo pealeii    5 1.009000e-04
##                  Loligo reynaudii    5 1.009000e-04
##              Lophius gastrophysus    5 1.009000e-04
##                  Loxechinus albus    5 1.009000e-04
##               Lutjanus buccanella    5 1.009000e-04
##              Lutjanus cyanopterus    5 1.009000e-04
##                   Lutjanus gibbus    5 1.009000e-04
##                   Lutjanus johnii    5 1.009000e-04
##                  Lutjanus kasmira    5 1.009000e-04
##                     Lutjanus peru    5 1.009000e-04
##          Lutjanus quinquelineatus    5 1.009000e-04
##                       Lycodes spp    5 1.009000e-04
##           Macrozoarces americanus    5 1.009000e-04
##              Mancopsetta maculata    5 1.009000e-04
##            Menticirrhus saxatilis    5 1.009000e-04
##                  Meretrix lusoria    5 1.009000e-04
##                Merluccius albidus    5 1.009000e-04
##               Merluccius capensis    5 1.009000e-04
##       Mesogobius batrachocephalus    5 1.009000e-04
##          Metanephrops challengeri    5 1.009000e-04
##           Metanephrops mozambicus    5 1.009000e-04
##               Metapenaeus joyneri    5 1.009000e-04
##                 Microgadus tomcod    5 1.009000e-04
##                   Mithrax armatus    5 1.009000e-04
##                    Mobula mobular    5 1.009000e-04
##             Monotaxis grandoculis    5 1.009000e-04
##                     Mugil incilis    5 1.009000e-04
##                       Mulinia spp    5 1.009000e-04
##      Mulloidichthys flavolineatus    5 1.009000e-04
##                 Mullus argentinae    5 1.009000e-04
##                   Munida gregaria    5 1.009000e-04
##             Mustelus lenticulatus    5 1.009000e-04
##           Mycteroperca microlepis    5 1.009000e-04
##               Mycteroperca phenax    5 1.009000e-04
##             Mycteroperca venenosa    5 1.009000e-04
##                  Mytilus coruscus    5 1.009000e-04
##                    Naso unicornis    5 1.009000e-04
##           Nematopalaemon hastatus    5 1.009000e-04
##           Nematopalaemon schmitti    5 1.009000e-04
##              Nemipterus japonicus    5 1.009000e-04
##               Nemipterus virgatus    5 1.009000e-04
##            Normanichthys crockeri    5 1.009000e-04
##                 Notopogon lilliei    5 1.009000e-04
##              Nototheniops larseni    5 1.009000e-04
##                      Octopus maya    5 1.009000e-04
##                 Odontesthes regia    5 1.009000e-04
##             Oligoplites refulgens    5 1.009000e-04
##                      Ophichthidae    5 1.009000e-04
##                  Ostrea chilensis    5 1.009000e-04
##                    Ostrea lutaria    5 1.009000e-04
##              Ostreola conchaphila    5 1.009000e-04
##                 Oxynotus centrina    5 1.009000e-04
##                Palinurus delagoae    5 1.009000e-04
##              Palinurus gilchristi    5 1.009000e-04
##                        Pampus spp    5 1.009000e-04
##               Pandalus hypsinotus    5 1.009000e-04
##                 Pandalus kessleri    5 1.009000e-04
##               Pandalus platyceros    5 1.009000e-04
##                  Panulirus cygnus    5 1.009000e-04
##                 Panulirus homarus    5 1.009000e-04
##       Parachaenichthys georgianus    5 1.009000e-04
##              Paralabrax humeralis    5 1.009000e-04
##                    Paralabrax spp    5 1.009000e-04
##             Paralichthys oblongus    5 1.009000e-04
##             Paralithodes brevipes    5 1.009000e-04
##             Paralithodes platypus    5 1.009000e-04
##            Paralonchurus peruanus    5 1.009000e-04
##          Parapenaeopsis atlantica    5 1.009000e-04
##                Parapenaeopsis spp    5 1.009000e-04
##                 Parapercis colias    5 1.009000e-04
##                     Parika scaber    5 1.009000e-04
##           Paristiopterus labiosus    5 1.009000e-04
##         Patagonotothen brevicauda    5 1.009000e-04
##             Patinopecten caurinus    5 1.009000e-04
##             Pecten novaezelandiae    5 1.009000e-04
##            Pelates quadrilineatus    5 1.009000e-04
##              Penaeus penicillatus    5 1.009000e-04
##                     Pennahia anea    5 1.009000e-04
##                       Perna perna    5 1.009000e-04
##                   Petromyzontidae    5 1.009000e-04
##                    Pharus legumen    5 1.009000e-04
##                   Phycis chesteri    5 1.009000e-04
##             Pinguipes brasilianus    5 1.009000e-04
##               Pinguipes chilensis    5 1.009000e-04
##         Plagiogeneion rubiginosum    5 1.009000e-04
##             Platichthys stellatus    5 1.009000e-04
##          Plectorhinchus gaterinus    5 1.009000e-04
##           Plectorhinchus sordidus    5 1.009000e-04
##            Plectropomus areolatus    5 1.009000e-04
##         Plectropomus pessuliferus    5 1.009000e-04
##       Pleurogrammus monopterygius    5 1.009000e-04
##              Pleuroncodes monodon    5 1.009000e-04
##                    Pleuronectidae    5 1.009000e-04
##          Pleuronichthys decurrens    5 1.009000e-04
##             Pollicipes pollicipes    5 1.009000e-04
##                     Pomacanthidae    5 1.009000e-04
##                  Pomadasys kaakan    5 1.009000e-04
##                   Pontinus kuhlii    5 1.009000e-04
##                 Pristiophorus spp    5 1.009000e-04
##              Prolatilus jugularis    5 1.009000e-04
##               Protothaca staminea    5 1.009000e-04
##                  Protothaca thaca    5 1.009000e-04
##            Protrachypene precipua    5 1.009000e-04
##               Pseudophycis bachus    5 1.009000e-04
##      Pseudopleuronectes herzenst.    5 1.009000e-04
##               Pterygotrigla picta    5 1.009000e-04
##                     Raja erinacea    5 1.009000e-04
##            Rhabdosargus globiceps    5 1.009000e-04
##              Rhinobatos planiceps    5 1.009000e-04
##                Rhinoptera bonasus    5 1.009000e-04
##                   Rhombosolea spp    5 1.009000e-04
##           Rhynchobatus djiddensis    5 1.009000e-04
##                       Rutilus spp    5 1.009000e-04
##                Salvelinus alpinus    5 1.009000e-04
##                 Sardinella zunasi    5 1.009000e-04
##           Sardinops neopilchardus    5 1.009000e-04
##           Sargocentron spiniferum    5 1.009000e-04
##                    Scarus ghobban    5 1.009000e-04
##                   Scarus persicus    5 1.009000e-04
##                   Scatophagus spp    5 1.009000e-04
##                Scolopsis taeniata    5 1.009000e-04
##                  Scomberoides tol    5 1.009000e-04
##                    Scophthalmidae    5 1.009000e-04
##              Scophthalmus aquosus    5 1.009000e-04
##                  Sebastes crameri    5 1.009000e-04
##                 Sebastes melanops    5 1.009000e-04
##                  Selene peruviana    5 1.009000e-04
##                     Semele solida    5 1.009000e-04
##             Semicossyphus pulcher    5 1.009000e-04
##               Seriolella caerulea    5 1.009000e-04
##                 Seriolella porosa    5 1.009000e-04
##                   Serranus scriba    5 1.009000e-04
##             Sicyonia brevirostris    5 1.009000e-04
##                 Sicyonia ingentis    5 1.009000e-04
##                    Siliqua patula    5 1.009000e-04
##                Solea senegalensis    5 1.009000e-04
##              Solenocera agassizii    5 1.009000e-04
##             Sphoeroides maculatus    5 1.009000e-04
##                  Spisula polynyma    5 1.009000e-04
##                       Spisula spp    5 1.009000e-04
##            Spratelloides gracilis    5 1.009000e-04
##               Stenotomus chrysops    5 1.009000e-04
##           Stephanolepis cirrhifer    5 1.009000e-04
##                 Stereolepis gigas    5 1.009000e-04
##             Strangomera bentincki    5 1.009000e-04
##           Stromateus brasiliensis    5 1.009000e-04
##                Strongylura marina    5 1.009000e-04
##                  Symphodus melops    5 1.009000e-04
##       Taractichthys steindachneri    5 1.009000e-04
##                    Tautoga onitis    5 1.009000e-04
##           Tautogolabrus adspersus    5 1.009000e-04
##                       Tawera gayi    5 1.009000e-04
##               Tetrapturus georgii    5 1.009000e-04
##            Thaleichthys pacificus    5 1.009000e-04
##                  Thelenota ananas    5 1.009000e-04
##                 Tivela mactroides    5 1.009000e-04
##                       Trachinidae    5 1.009000e-04
##               Trachinotus blochii    5 1.009000e-04
##              Trachinotus mookalee    5 1.009000e-04
##                  Trachipterus spp    5 1.009000e-04
##         Tragulichthys jaculiferus    5 1.009000e-04
##                        Tresus spp    5 1.009000e-04
##              Tylosurus crocodilus    5 1.009000e-04
##              Upogebia pugettensis    5 1.009000e-04
##              Venerupis rhomboides    5 1.009000e-04
##               Xiphopenaeus riveti    5 1.009000e-04
##                Xyrichtys novacula    5 1.009000e-04
##                    Zearaja nasuta    5 1.009000e-04
##                            Zeidae    5 1.009000e-04
##            Zygochlamys delicatula    5 1.009000e-04
##             Bathyraja brachyurops    4 8.072002e-05
##                Bathyraja maccaini    4 8.072002e-05
##              Brevoortia pectinata    4 8.072002e-05
##               Carcharhinus isodon    4 8.072002e-05
##              Carpilius corallinus    4 8.072002e-05
##                       Coris julis    4 8.072002e-05
##                Dipturus chilensis    4 8.072002e-05
##                Echeneis naucrates    4 8.072002e-05
##               Echinorhinus brucus    4 8.072002e-05
##                     Ensis siliqua    4 8.072002e-05
##          Erugosquilla massavensis    4 8.072002e-05
##                   Etelis oculatus    4 8.072002e-05
##                    Galeus murinus    4 8.072002e-05
##                    Haliotis midae    4 8.072002e-05
##                Heptranchias perlo    4 8.072002e-05
##               Hyporhamphus sajori    4 8.072002e-05
##                    Lile stolifera    4 8.072002e-05
##           Menticirrhus americanus    4 8.072002e-05
##               Nemipterus randalli    4 8.072002e-05
##                  Notothenia acuta    4 8.072002e-05
##                Pagothenia hansoni    4 8.072002e-05
##             Palaemon longirostris    4 8.072002e-05
##              Pandalopsis japonica    4 8.072002e-05
##                 Pandalus goniurus    4 8.072002e-05
##                 Pandalus montagui    4 8.072002e-05
##                 Paralomis formosa    4 8.072002e-05
##               Pellona flavipinnis    4 8.072002e-05
##             Pelotretis flavilatus    4 8.072002e-05
##            Pentaceros decacanthus    4 8.072002e-05
##                   Raja castelnaui    4 8.072002e-05
##                   Raja cyclophora    4 8.072002e-05
##                       Raja fyllae    4 8.072002e-05
##             Rhinobatos percellens    4 8.072002e-05
##             Rhinobatos rhinobatos    4 8.072002e-05
##                  Rioraja agassizi    4 8.072002e-05
##                 Sclerocrangon spp    4 8.072002e-05
##        Scyllarides aequinoctialis    4 8.072002e-05
##                 Sebastes oculatus    4 8.072002e-05
##                  Seriola fasciata    4 8.072002e-05
##               Somniosus rostratus    4 8.072002e-05
##                 Sympterygia acuta    4 8.072002e-05
##            Sympterygia bonapartii    4 8.072002e-05
##                    Synodus saurus    4 8.072002e-05
##                       Tellina spp    4 8.072002e-05
##              Trachurus picturatus    4 8.072002e-05
##         Tripterophycis gilchristi    4 8.072002e-05
##               Ucides occidentalis    4 8.072002e-05
##                   Anchoa hepsetus    3 6.054002e-05
##              Bathyraja macloviana    3 6.054002e-05
##              Calanus finmarchicus    3 6.054002e-05
##             Caulolatilus chrysops    3 6.054002e-05
##                 Cubiceps capensis    3 6.054002e-05
##                   Cymbium cymbium    3 6.054002e-05
##                       Ensis ensis    3 6.054002e-05
##              Epinephelus analogus    3 6.054002e-05
##     Epinephelus caeruleopunctatus    3 6.054002e-05
##              Fistularia tabacaria    3 6.054002e-05
##                Gaidropsarus ensis    3 6.054002e-05
##                    Haemulon album    3 6.054002e-05
##          Hyperoglyphe perciformis    3 6.054002e-05
##           Lagocephalus sceleratus    3 6.054002e-05
##                Lagodon rhomboides    3 6.054002e-05
##              Leptocharias smithii    3 6.054002e-05
##                Lethrinus miniatus    3 6.054002e-05
##                Libinia emarginata    3 6.054002e-05
##                  Lithodes murrayi    3 6.054002e-05
##                  Loligo duvauceli    3 6.054002e-05
##               Molva macrophthalma    3 6.054002e-05
##             Mycteroperca xenarcha    3 6.054002e-05
##          Nemadactylus macropterus    3 6.054002e-05
##                Odontesthes smitti    3 6.054002e-05
##                Palaemon adspersus    3 6.054002e-05
##                 Panulirus ornatus    3 6.054002e-05
##             Paragaleus pectoralis    3 6.054002e-05
##                 Penaeus paulensis    3 6.054002e-05
##                      Peprilus spp    3 6.054002e-05
##                 Plesionika martia    3 6.054002e-05
##          Pleuragramma antarcticum    3 6.054002e-05
##            Pomatoschistus microps    3 6.054002e-05
##                  Regalecus glesne    3 6.054002e-05
##              Rhinobatos cemiculus    3 6.054002e-05
##              Rhinoptera marginata    3 6.054002e-05
##             Rhizoprionodon acutus    3 6.054002e-05
##                Sebastes diploproa    3 6.054002e-05
##                Sebastes viviparus    3 6.054002e-05
##                      Selene vomer    3 6.054002e-05
##               Somniosus pacificus    3 6.054002e-05
##               Spisula subtruncata    3 6.054002e-05
##                       Squalus spp    3 6.054002e-05
##                Trachinotus ovatus    3 6.054002e-05
##         Trachipterus trachipterus    3 6.054002e-05
##            Trachyscorpia echinata    3 6.054002e-05
##         Acipenser gueldenstaedtii    2 4.036001e-05
##               Acipenser stellatus    2 4.036001e-05
##                 Alepisaurus ferox    2 4.036001e-05
##                   Alosa mediocris    2 4.036001e-05
##                         Arca noae    2 4.036001e-05
##                 Atherina hepsetus    2 4.036001e-05
##                         Caproidae    2 4.036001e-05
##           Carcharhinus brevipinna    2 4.036001e-05
##                  Clepticus parrae    2 4.036001e-05
##               Cynomacrurus piriei    2 4.036001e-05
##               Dorosoma cepedianum    2 4.036001e-05
##            Fistularia commersonii    2 4.036001e-05
##                 Gollum attenuatus    2 4.036001e-05
##              Hemitriakis japanica    2 4.036001e-05
##             Hypoptychus dybowskii    2 4.036001e-05
##                     Labrus merula    2 4.036001e-05
##              Lampetra fluviatilis    2 4.036001e-05
##               Lampris immaculatus    2 4.036001e-05
##                 Lophius vaillanti    2 4.036001e-05
##                    Lutjanus vitta    2 4.036001e-05
##             Macrourus holotrachys    2 4.036001e-05
##                      Modiolus spp    2 4.036001e-05
##                  Morone americana    2 4.036001e-05
##                  Oncorhynchus spp    2 4.036001e-05
##       Parapristipoma octolineatum    2 4.036001e-05
##                   Penaeus indicus    2 4.036001e-05
##                  Penaeus schmitti    2 4.036001e-05
##                   Pitar rostratus    2 4.036001e-05
##             Pleuroncodes planipes    2 4.036001e-05
##                 Polymixia nobilis    2 4.036001e-05
##                Psettodes belcheri    2 4.036001e-05
##                Raja nidarosiensis    2 4.036001e-05
##       Scardinius erythrophthalmus    2 4.036001e-05
##                  Scorpaena porcus    2 4.036001e-05
##                Serranus atricauda    2 4.036001e-05
##                   Sphyraena ensis    2 4.036001e-05
##                    Spicara smaris    2 4.036001e-05
##                Squalus blainville    2 4.036001e-05
##             Stomolophus meleagris    2 4.036001e-05
##                       Tonna galea    2 4.036001e-05
##           Trachycardium muricatum    2 4.036001e-05
##              Triakis megalopterus    2 4.036001e-05
##                   Venus verrucosa    2 4.036001e-05
##                 Alopias pelagicus    1 2.018001e-05
##                  Alosa aestivalis    1 2.018001e-05
##                    Anchoa marinii    1 2.018001e-05
##             Aphanopus intermedius    1 2.018001e-05
##                      Aristeus spp    1 2.018001e-05
##                  Barbourisia rufa    1 2.018001e-05
##           Borostomias antarcticus    1 2.018001e-05
##            Carcharhinus acronotus    1 2.018001e-05
##             Carcharhinus obscurus    1 2.018001e-05
##               Chaenodraco wilsoni    1 2.018001e-05
##            Chaetodipterus zonatus    1 2.018001e-05
##                Chimaera phantasma    1 2.018001e-05
##                    Dasyatis longa    1 2.018001e-05
##                 Dasyatis violacea    1 2.018001e-05
##                        Echinoidea    1 2.018001e-05
##          Epinephelus adscensionis    1 2.018001e-05
##          Epinephelus drummondhayi    1 2.018001e-05
##                  Erilepis zonifer    1 2.018001e-05
##               Etmopterus princeps    1 2.018001e-05
##                 Gymnura marmorata    1 2.018001e-05
##          Halobatrachus didactylus    1 2.018001e-05
##            Lampanyctodes hectoris    1 2.018001e-05
##                  Lithognathus spp    1 2.018001e-05
##                 Lobotes pacificus    1 2.018001e-05
##              Magnisudis atlantica    1 2.018001e-05
##                   Manta birostris    1 2.018001e-05
##           Merluccius angustimanus    1 2.018001e-05
##            Myoxocephalus scorpius    1 2.018001e-05
##            Negaprion brevirostris    1 2.018001e-05
##              Notothenia coriiceps    1 2.018001e-05
##               Nototheniops mizops    1 2.018001e-05
##                Oxynotus paradoxus    1 2.018001e-05
##                  Penaeus subtilis    1 2.018001e-05
##              Peprilus triacanthus    1 2.018001e-05
##           Protemblemaria bicirris    1 2.018001e-05
##                       Raja lintea    1 2.018001e-05
##                   Raja maderensis    1 2.018001e-05
##                    Seriola zonata    1 2.018001e-05
##                      Serranus spp    1 2.018001e-05
##                   Sphoeroides spp    1 2.018001e-05
##                    Sphyrna tiburo    1 2.018001e-05
##              Todarodes filippovae    1 2.018001e-05
##              Trachyrincus scabrus    1 2.018001e-05
##                   Uranoscopus spp    1 2.018001e-05
##           Zanclorhynchus spinifer    1 2.018001e-05
```

10. Use the data to do at least one analysis of your choice.

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  arrange(desc(isscaap_group_number))
```

```
## # A tibble: 376,771 × 10
## # Groups:   country [203]
##    country   commo…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##    <fct>     <chr>   <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
##  1 Australia Aquati… 77      Miscel… 699XXX… Invert… 58      Quanti…  1997     1
##  2 Australia Aquati… 77      Miscel… 699XXX… Invert… 58      Quanti…  2008    NA
##  3 Australia Aquati… 77      Miscel… 699XXX… Invert… 58      Quanti…  2009    NA
##  4 Australia Aquati… 77      Miscel… 699XXX… Invert… 58      Quanti…  2010    NA
##  5 Australia Aquati… 77      Miscel… 699XXX… Invert… 58      Quanti…  2011     4
##  6 Australia Aquati… 77      Miscel… 699XXX… Invert… 58      Quanti…  2012     1
##  7 Australia Aquati… 77      Miscel… 699XXX… Invert… 57      Quanti…  2000    63
##  8 Australia Aquati… 77      Miscel… 699XXX… Invert… 57      Quanti…  2001    96
##  9 Australia Aquati… 77      Miscel… 699XXX… Invert… 57      Quanti…  2002    72
## 10 Australia Aquati… 77      Miscel… 699XXX… Invert… 57      Quanti…  2003    NA
## # … with 376,761 more rows, and abbreviated variable names ¹​common_name,
## #   ²​isscaap_group_number, ³​isscaap_taxonomic_group, ⁴​asfis_species_number,
## #   ⁵​asfis_species_name, ⁶​fao_major_fishing_area
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
