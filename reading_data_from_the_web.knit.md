---
title: "reading_data_from_the_web"
author: "Emily Potts"
date: "2022-10-13"
output: github_document
---





```r
library(tidyverse)
library(rvest)
library(httr)
```


# Extracting data

```r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"
drug_use_html = read_html(url)

drug_use_html
```

```
## {html_document}
## <html lang="en">
## [1] <head>\n<link rel="P3Pv1" href="http://www.samhsa.gov/w3c/p3p.xml">\n<tit ...
## [2] <body>\r\n\r\n<noscript>\r\n<p>Your browser's Javascript is off. Hyperlin ...
```

all the tables

```r
drug_use_html %>% 
  html_table()
```

```
## [[1]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "12.90… "13.36" "0.002" "13.28… "12.86" "0.063" "31.78" "32.07" "0.369"
##  3 "Nor… "13.88… "14.66" "0.005" "13.98" "13.51" "0.266" "34.66… "36.45" "0.008"
##  4 "Mid… "12.40… "12.76" "0.082" "12.45" "12.33" "0.726" "32.13" "32.20" "0.900"
##  5 "Sou… "11.24… "11.64" "0.029" "12.02" "11.88" "0.666" "28.93" "29.20" "0.581"
##  6 "Wes… "15.27" "15.62" "0.262" "15.53… "14.43" "0.018" "33.72" "33.19" "0.460"
##  7 "Ala… "9.98"  "9.60"  "0.426" "9.90"  "9.71"  "0.829" "26.99" "26.13" "0.569"
##  8 "Ala… "19.60… "21.92" "0.010" "17.30" "18.44" "0.392" "36.47… "40.69" "0.015"
##  9 "Ari… "13.69" "13.12" "0.364" "15.12" "13.45" "0.131" "31.53" "31.15" "0.826"
## 10 "Ark… "11.37" "11.59" "0.678" "12.79" "12.14" "0.538" "26.53" "27.06" "0.730"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[2]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "7.96a" "8.34"  "0.001" "7.22"  "7.20"  "0.905" "19.32" "19.70" "0.178"
##  3 "Nor… "8.58a" "9.28"  "0.001" "7.68"  "7.73"  "0.883" "21.19… "22.64" "0.007"
##  4 "Mid… "7.50a" "7.92"  "0.009" "6.64"  "6.80"  "0.530" "19.23" "19.29" "0.873"
##  5 "Sou… "6.74a" "7.02"  "0.044" "6.31"  "6.49"  "0.441" "17.20… "17.79" "0.092"
##  6 "Wes… "9.84"  "10.08" "0.324" "8.85"  "8.31"  "0.144" "21.30" "20.85" "0.425"
##  7 "Ala… "5.57"  "5.35"  "0.510" "4.98"  "5.16"  "0.779" "15.04" "14.33" "0.503"
##  8 "Ala… "11.85… "14.38" "0.002" "9.19"  "10.64" "0.204" "21.30… "25.02" "0.020"
##  9 "Ari… "8.80"  "8.51"  "0.570" "8.30"  "7.71"  "0.491" "20.04" "18.92" "0.412"
## 10 "Ark… "6.70"  "7.17"  "0.240" "6.22"  "6.46"  "0.748" "16.21" "16.93" "0.556"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[3]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "1.91"  "1.95"  "0.276" "5.60"  "5.41"  "0.106" "7.68"  "7.88"  "0.294"
##  3 "Nor… "2.01"  "2.04"  "0.634" "5.85b" "5.55"  "0.095" "8.40"  "8.67"  "0.410"
##  4 "Mid… "1.95"  "1.96"  "0.854" "5.31"  "5.12"  "0.208" "8.17"  "8.14"  "0.924"
##  5 "Sou… "1.69"  "1.75"  "0.137" "5.18"  "5.13"  "0.674" "6.77"  "7.12"  "0.171"
##  6 "Wes… "2.20"  "2.21"  "0.868" "6.37b" "6.02"  "0.085" "8.27"  "8.32"  "0.877"
##  7 "Ala… "1.42"  "1.49"  "0.383" "4.46"  "4.36"  "0.791" "6.04"  "6.39"  "0.524"
##  8 "Ala… "3.01a" "3.54"  "0.012" "6.99"  "7.52"  "0.371" "9.04b" "10.69" "0.079"
##  9 "Ari… "2.16"  "2.15"  "0.934" "6.58"  "6.09"  "0.302" "8.00"  "8.36"  "0.620"
## 10 "Ark… "1.82"  "1.84"  "0.794" "5.78"  "5.37"  "0.331" "6.63"  "7.08"  "0.471"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[4]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "1.66a" "1.76"  "0.040" "0.60"  "0.64"  "0.393" "4.51a" "4.98"  "0.005"
##  3 "Nor… "1.94a" "2.18"  "0.012" "0.60"  "0.66"  "0.374" "5.19a" "6.06"  "0.001"
##  4 "Mid… "1.37"  "1.43"  "0.282" "0.48"  "0.54"  "0.288" "3.81a" "4.22"  "0.020"
##  5 "Sou… "1.45b" "1.56"  "0.067" "0.53"  "0.57"  "0.462" "3.77a" "4.32"  "0.000"
##  6 "Wes… "2.03"  "2.05"  "0.816" "0.82"  "0.85"  "0.806" "5.78"  "5.88"  "0.740"
##  7 "Ala… "1.23"  "1.22"  "0.995" "0.42"  "0.41"  "0.883" "3.09"  "3.20"  "0.707"
##  8 "Ala… "1.54a" "2.00"  "0.010" "0.51"  "0.65"  "0.200" "3.84a" "4.79"  "0.035"
##  9 "Ari… "2.25"  "2.29"  "0.861" "1.01"  "0.85"  "0.262" "6.23"  "6.92"  "0.272"
## 10 "Ark… "0.93"  "1.07"  "0.208" "0.41"  "0.48"  "0.380" "2.54"  "2.89"  "0.234"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[5]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "0.30"  "0.33"  "0.217" "0.12"  "0.10"  "0.313" "0.73"  "0.69"  "0.469"
##  3 "Nor… "0.43a" "0.54"  "0.007" "0.13"  "0.13"  "0.984" "1.08"  "0.98"  "0.295"
##  4 "Mid… "0.30"  "0.31"  "0.638" "0.11"  "0.10"  "0.818" "0.74"  "0.74"  "0.995"
##  5 "Sou… "0.27"  "0.26"  "0.444" "0.12"  "0.08"  "0.147" "0.63"  "0.56"  "0.133"
##  6 "Wes… "0.25"  "0.29"  "0.152" "0.13"  "0.11"  "0.586" "0.63"  "0.65"  "0.797"
##  7 "Ala… "0.22"  "0.27"  "0.171" "0.10"  "0.08"  "0.676" "0.45b" "0.64"  "0.054"
##  8 "Ala… "0.70a" "1.23"  "0.044" "0.11"  "0.08"  "0.297" "1.19b" "0.91"  "0.073"
##  9 "Ari… "0.32a" "0.55"  "0.001" "0.17"  "0.20"  "0.603" "0.79"  "0.90"  "0.480"
## 10 "Ark… "0.19"  "0.17"  "0.398" "0.10"  "0.07"  "0.312" "0.40"  "0.42"  "0.773"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[6]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "52.42" "52.18" "0.337" "11.55… "10.58" "0.000" "59.60… "58.96" "0.088"
##  3 "Nor… "57.80… "56.66" "0.009" "13.19" "12.57" "0.130" "63.79" "64.17" "0.554"
##  4 "Mid… "55.14… "54.36" "0.032" "11.31… "10.30" "0.001" "63.11… "61.88" "0.014"
##  5 "Sou… "48.74" "48.85" "0.759" "10.87… "9.74"  "0.000" "56.75" "56.16" "0.243"
##  6 "Wes… "51.67" "52.07" "0.383" "11.71… "10.76" "0.016" "57.82" "56.92" "0.182"
##  7 "Ala… "44.72" "43.94" "0.533" "10.53… "8.76"  "0.038" "51.36" "51.99" "0.716"
##  8 "Ala… "54.02" "54.98" "0.444" "9.22"  "11.04" "0.209" "59.65" "62.57" "0.107"
##  9 "Ari… "51.80" "51.19" "0.613" "11.90… "10.45" "0.099" "58.02" "56.38" "0.333"
## 10 "Ark… "42.45" "41.81" "0.588" "9.90"  "9.34"  "0.491" "55.03… "51.60" "0.043"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[7]]
## # A tibble: 57 × 4
##    State                                                 Alcoh…¹ Alcoh…² Alcoh…³
##    <chr>                                                 <chr>   <chr>   <chr>  
##  1 "NOTE: State and census region estimates are based o… "NOTE:… "NOTE:… "NOTE:…
##  2 "Total U.S."                                          "22.76… "21.57" "0.000"
##  3 "Northeast"                                           "26.11" "25.98" "0.792"
##  4 "Midwest"                                             "23.73… "22.00" "0.000"
##  5 "South"                                               "20.68… "19.66" "0.010"
##  6 "West"                                                "22.73… "21.01" "0.000"
##  7 "Alabama"                                             "19.25" "18.19" "0.305"
##  8 "Alaska"                                              "21.47… "23.91" "0.058"
##  9 "Arizona"                                             "22.01… "19.25" "0.009"
## 10 "Arkansas"                                            "18.07" "16.65" "0.106"
## # … with 47 more rows, and abbreviated variable names
## #   ¹​`Alcohol Use inPast Month(2013-2014)`,
## #   ²​`Alcohol Use inPast Month(2014-2015)`,
## #   ³​`Alcohol Use inPast Month(P Value)`
## 
## [[8]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "25.36… "24.56" "0.000" "7.42a" "6.50"  "0.000" "36.04… "34.02" "0.000"
##  3 "Nor… "23.76" "23.30" "0.216" "7.18a" "6.22"  "0.001" "34.61… "32.89" "0.004"
##  4 "Mid… "28.57… "27.39" "0.000" "8.58a" "7.68"  "0.001" "40.75… "38.61" "0.000"
##  5 "Sou… "26.91… "26.24" "0.034" "7.57a" "6.67"  "0.000" "37.26… "35.33" "0.000"
##  6 "Wes… "21.20… "20.29" "0.015" "6.31a" "5.35"  "0.000" "31.04… "28.78" "0.000"
##  7 "Ala… "31.62" "30.46" "0.295" "8.43"  "7.78"  "0.458" "43.37" "42.27" "0.494"
##  8 "Ala… "29.30… "31.51" "0.048" "10.73" "9.87"  "0.429" "41.11" "42.61" "0.388"
##  9 "Ari… "22.14" "22.51" "0.678" "6.81"  "6.18"  "0.354" "32.74" "31.23" "0.329"
## 10 "Ark… "35.57" "34.05" "0.188" "10.89" "9.67"  "0.185" "43.57" "41.50" "0.210"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[9]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "21.05… "20.12" "0.000" "5.24a" "4.53"  "0.000" "29.49… "27.54" "0.000"
##  3 "Nor… "19.69" "19.13" "0.101" "5.10a" "4.37"  "0.001" "28.36… "26.89" "0.016"
##  4 "Mid… "23.84… "22.50" "0.000" "6.16a" "5.55"  "0.007" "32.84… "30.61" "0.000"
##  5 "Sou… "22.37… "21.41" "0.001" "5.22a" "4.50"  "0.000" "30.24… "28.57" "0.000"
##  6 "Wes… "17.43… "16.66" "0.026" "4.56a" "3.75"  "0.000" "26.21… "23.72" "0.000"
##  7 "Ala… "25.90" "24.25" "0.106" "5.66"  "5.34"  "0.612" "34.32" "34.00" "0.836"
##  8 "Ala… "22.00… "24.64" "0.008" "6.15"  "6.02"  "0.860" "34.04" "35.38" "0.416"
##  9 "Ari… "18.73" "19.23" "0.576" "4.95"  "4.15"  "0.110" "27.64" "25.33" "0.137"
## 10 "Ark… "28.51" "27.81" "0.519" "7.13"  "6.35"  "0.273" "34.10" "32.28" "0.244"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[10]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "6.50a" "6.14"  "0.001" "2.76"  "2.62"  "0.160" "12.64… "11.61" "0.000"
##  3 "Nor… "6.64"  "6.39"  "0.193" "2.88"  "2.72"  "0.371" "13.12… "12.31" "0.056"
##  4 "Mid… "6.59a" "6.25"  "0.033" "2.70"  "2.52"  "0.233" "13.56… "12.45" "0.000"
##  5 "Sou… "6.20a" "5.76"  "0.003" "2.65"  "2.52"  "0.315" "11.63… "10.61" "0.000"
##  6 "Wes… "6.80"  "6.47"  "0.120" "2.91"  "2.78"  "0.494" "13.03… "11.88" "0.005"
##  7 "Ala… "5.76a" "4.64"  "0.007" "2.84b" "2.17"  "0.053" "10.73" "9.65"  "0.234"
##  8 "Ala… "6.72"  "7.43"  "0.153" "2.12"  "2.55"  "0.223" "12.66" "12.30" "0.703"
##  9 "Ari… "7.60b" "6.66"  "0.062" "3.37"  "2.90"  "0.252" "13.03" "12.36" "0.488"
## 10 "Ark… "5.23"  "4.88"  "0.347" "2.63"  "2.76"  "0.703" "10.23" "9.64"  "0.508"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[11]]
## # A tibble: 57 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "3.04"  "2.97"  "0.321" "1.01"  "0.95"  "0.409" "5.61a" "5.18"  "0.005"
##  3 "Nor… "3.01"  "3.09"  "0.500" "1.02"  "0.94"  "0.402" "5.43"  "5.25"  "0.519"
##  4 "Mid… "3.06b" "2.86"  "0.061" "1.03"  "0.93"  "0.209" "5.83a" "5.30"  "0.012"
##  5 "Sou… "2.92a" "2.73"  "0.047" "0.96"  "0.92"  "0.594" "5.16a" "4.66"  "0.008"
##  6 "Wes… "3.25"  "3.37"  "0.409" "1.05"  "1.05"  "0.945" "6.24"  "5.82"  "0.152"
##  7 "Ala… "2.99a" "2.34"  "0.026" "0.98"  "0.80"  "0.264" "4.74"  "3.86"  "0.120"
##  8 "Ala… "3.21"  "3.67"  "0.200" "0.77"  "0.87"  "0.560" "6.19"  "6.23"  "0.960"
##  9 "Ari… "3.44"  "3.62"  "0.591" "1.11"  "1.10"  "0.969" "5.68"  "5.92"  "0.735"
## 10 "Ark… "2.73"  "2.42"  "0.255" "0.96"  "0.96"  "0.986" "5.03"  "4.30"  "0.210"
## # … with 47 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
## 
## [[12]]
## # A tibble: 57 × 10
##    State 18+(2…¹ 18+(2…² 18+(P…³ 18-25…⁴ 18-25…⁵ 18-25…⁶ 26+(2…⁷ 26+(2…⁸ 26+(P…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "4.15"  "4.05"  "0.325" "4.52a" "4.92"  "0.004" "4.09"  "3.91"  "0.110"
##  3 "Nor… "3.93"  "3.94"  "0.953" "4.67a" "5.15"  "0.023" "3.80"  "3.74"  "0.712"
##  4 "Mid… "4.45"  "4.36"  "0.511" "4.93a" "5.33"  "0.036" "4.37"  "4.19"  "0.285"
##  5 "Sou… "4.17"  "4.00"  "0.206" "4.18a" "4.54"  "0.027" "4.17b" "3.91"  "0.091"
##  6 "Wes… "4.02"  "3.96"  "0.681" "4.56b" "4.98"  "0.065" "3.93"  "3.78"  "0.412"
##  7 "Ala… "4.53"  "4.64"  "0.749" "4.30"  "4.97"  "0.137" "4.57"  "4.59"  "0.971"
##  8 "Ala… "3.90"  "4.02"  "0.707" "4.60a" "5.75"  "0.044" "3.77"  "3.69"  "0.844"
##  9 "Ari… "4.09"  "4.33"  "0.491" "4.45"  "5.06"  "0.244" "4.03"  "4.21"  "0.651"
## 10 "Ark… "5.24"  "5.27"  "0.942" "4.49"  "5.16"  "0.213" "5.36"  "5.29"  "0.882"
## # … with 47 more rows, and abbreviated variable names ¹​`18+(2013-2014)`,
## #   ²​`18+(2014-2015)`, ³​`18+(P Value)`, ⁴​`18-25(2013-2014)`,
## #   ⁵​`18-25(2014-2015)`, ⁶​`18-25(P Value)`, ⁷​`26+(2013-2014)`,
## #   ⁸​`26+(2014-2015)`, ⁹​`26+(P Value)`
## 
## [[13]]
## # A tibble: 57 × 10
##    State 18+(2…¹ 18+(2…² 18+(P…³ 18-25…⁴ 18-25…⁵ 18-25…⁶ 26+(2…⁷ 26+(2…⁸ 26+(P…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "18.29" "18.01" "0.146" "19.75… "20.89" "0.000" "18.05… "17.52" "0.020"
##  3 "Nor… "17.87" "17.76" "0.735" "20.80… "22.00" "0.012" "17.39" "17.07" "0.400"
##  4 "Mid… "18.61" "18.34" "0.356" "20.45… "21.43" "0.013" "18.29" "17.81" "0.150"
##  5 "Sou… "18.01" "17.82" "0.519" "18.22… "19.31" "0.001" "17.97" "17.57" "0.227"
##  6 "Wes… "18.79… "18.18" "0.088" "20.70… "22.03" "0.012" "18.46… "17.51" "0.022"
##  7 "Ala… "19.51" "18.85" "0.469" "18.09" "18.78" "0.529" "19.75" "18.86" "0.399"
##  8 "Ala… "18.12" "18.11" "0.989" "20.33… "24.93" "0.001" "17.70" "16.80" "0.341"
##  9 "Ari… "18.59" "18.32" "0.756" "18.76" "19.58" "0.518" "18.56" "18.10" "0.648"
## 10 "Ark… "20.00" "19.77" "0.816" "19.99" "21.50" "0.225" "20.00" "19.48" "0.645"
## # … with 47 more rows, and abbreviated variable names ¹​`18+(2013-2014)`,
## #   ²​`18+(2014-2015)`, ³​`18+(P Value)`, ⁴​`18-25(2013-2014)`,
## #   ⁵​`18-25(2014-2015)`, ⁶​`18-25(P Value)`, ⁷​`26+(2013-2014)`,
## #   ⁸​`26+(2014-2015)`, ⁹​`26+(P Value)`
## 
## [[14]]
## # A tibble: 57 × 10
##    State 18+(2…¹ 18+(2…² 18+(P…³ 18-25…⁴ 18-25…⁵ 18-25…⁶ 26+(2…⁷ 26+(2…⁸ 26+(P…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "3.94"  "3.99"  "0.526" "7.44a" "7.88"  "0.014" "3.34"  "3.34"  "0.994"
##  3 "Nor… "3.81"  "3.93"  "0.407" "7.60b" "8.15"  "0.058" "3.19"  "3.24"  "0.746"
##  4 "Mid… "4.11"  "4.14"  "0.791" "7.83"  "8.08"  "0.333" "3.48"  "3.48"  "0.993"
##  5 "Sou… "3.84"  "3.86"  "0.896" "6.89a" "7.40"  "0.029" "3.33"  "3.27"  "0.680"
##  6 "Wes… "4.02"  "4.12"  "0.522" "7.84"  "8.25"  "0.223" "3.35"  "3.41"  "0.749"
##  7 "Ala… "3.98"  "4.02"  "0.885" "7.31"  "7.76"  "0.501" "3.41"  "3.40"  "0.973"
##  8 "Ala… "4.21"  "4.68"  "0.237" "8.30b" "9.97"  "0.064" "3.43"  "3.66"  "0.613"
##  9 "Ari… "4.23"  "4.34"  "0.775" "7.04"  "8.06"  "0.208" "3.75"  "3.70"  "0.907"
## 10 "Ark… "4.58"  "4.41"  "0.682" "6.67"  "7.43"  "0.287" "4.23"  "3.90"  "0.515"
## # … with 47 more rows, and abbreviated variable names ¹​`18+(2013-2014)`,
## #   ²​`18+(2014-2015)`, ³​`18+(P Value)`, ⁴​`18-25(2013-2014)`,
## #   ⁵​`18-25(2014-2015)`, ⁶​`18-25(P Value)`, ⁷​`26+(2013-2014)`,
## #   ⁸​`26+(2014-2015)`, ⁹​`26+(P Value)`
## 
## [[15]]
## # A tibble: 57 × 13
##    State 18+(2…¹ 18+(2…² 18+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 "NOT… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:… "NOTE:…
##  2 "Tot… "6.63"  "6.64"  "0.915" "11.01… "11.93" "0.000" "9.00a" "9.79"  "0.000"
##  3 "Nor… "6.66"  "6.82"  "0.458" "10.63… "11.68" "0.002" "9.61a" "10.56" "0.009"
##  4 "Mid… "6.81"  "6.87"  "0.736" "10.81… "12.12" "0.000" "9.39a" "10.23" "0.003"
##  5 "Sou… "6.47"  "6.52"  "0.750" "10.77… "11.51" "0.008" "8.31a" "9.09"  "0.003"
##  6 "Wes… "6.67"  "6.47"  "0.353" "11.82… "12.59" "0.046" "9.30b" "9.94"  "0.079"
##  7 "Ala… "6.85"  "6.81"  "0.948" "10.74" "10.97" "0.764" "8.24"  "8.61"  "0.648"
##  8 "Ala… "6.57"  "6.73"  "0.770" "9.92a" "12.40" "0.012" "9.19a" "11.68" "0.019"
##  9 "Ari… "7.32"  "6.77"  "0.362" "13.23" "13.20" "0.970" "8.86"  "8.46"  "0.644"
## 10 "Ark… "7.31"  "7.78"  "0.446" "11.95" "12.72" "0.411" "9.52"  "10.27" "0.415"
## # … with 47 more rows, 3 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`18+(2013-2014)`, ²​`18+(2014-2015)`, ³​`18+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
```

just the first table

```r
table_marj =
  drug_use_html %>% 
  html_table() %>% 
  first()
```


```r
table_marj =
  drug_use_html %>% 
  html_table() %>% 
  first() %>% 
  slice(-1)

table_marj
```

```
## # A tibble: 56 × 16
##    State 12+(2…¹ 12+(2…² 12+(P…³ 12-17…⁴ 12-17…⁵ 12-17…⁶ 18-25…⁷ 18-25…⁸ 18-25…⁹
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 Tota… 12.90a  13.36   0.002   13.28b  12.86   0.063   31.78   32.07   0.369  
##  2 Nort… 13.88a  14.66   0.005   13.98   13.51   0.266   34.66a  36.45   0.008  
##  3 Midw… 12.40b  12.76   0.082   12.45   12.33   0.726   32.13   32.20   0.900  
##  4 South 11.24a  11.64   0.029   12.02   11.88   0.666   28.93   29.20   0.581  
##  5 West  15.27   15.62   0.262   15.53a  14.43   0.018   33.72   33.19   0.460  
##  6 Alab… 9.98    9.60    0.426   9.90    9.71    0.829   26.99   26.13   0.569  
##  7 Alas… 19.60a  21.92   0.010   17.30   18.44   0.392   36.47a  40.69   0.015  
##  8 Ariz… 13.69   13.12   0.364   15.12   13.45   0.131   31.53   31.15   0.826  
##  9 Arka… 11.37   11.59   0.678   12.79   12.14   0.538   26.53   27.06   0.730  
## 10 Cali… 14.49   15.25   0.103   15.03   14.11   0.190   33.69   32.72   0.357  
## # … with 46 more rows, 6 more variables: `26+(2013-2014)` <chr>,
## #   `26+(2014-2015)` <chr>, `26+(P Value)` <chr>, `18+(2013-2014)` <chr>,
## #   `18+(2014-2015)` <chr>, `18+(P Value)` <chr>, and abbreviated variable
## #   names ¹​`12+(2013-2014)`, ²​`12+(2014-2015)`, ³​`12+(P Value)`,
## #   ⁴​`12-17(2013-2014)`, ⁵​`12-17(2014-2015)`, ⁶​`12-17(P Value)`,
## #   ⁷​`18-25(2013-2014)`, ⁸​`18-25(2014-2015)`, ⁹​`18-25(P Value)`
```


# CSS selectors


```r
swm_html = 
  read_html("https://www.imdb.com/list/ls070150896/")
```

how do i get the stuff i want?

```r
sw_titles =
  swm_html %>% 
  html_elements(".lister-item-header a") %>% 
  html_text()

sw_runtime =
  swm_html %>% 
  html_elements(".runtime") %>% 
  html_text()

sw_runtime
```

```
## [1] "136 min" "142 min" "140 min" "121 min" "124 min" "131 min" "138 min"
## [8] "152 min" "141 min"
```

```r
sw_money =
  swm_html %>% 
  html_elements(".text-small:nth-child(7) span:nth-child(5)") %>% 
  html_text()
sw_money
```

```
## [1] "$474.54M" "$310.68M" "$380.26M" "$322.74M" "$290.48M" "$309.13M" "$936.66M"
## [8] "$620.18M" "$515.20M"
```


```r
sw_df = 
  tibble(
    title = sw_titles,
    runtime = sw_runtime, 
    money = sw_money
  )
sw_df
```

```
## # A tibble: 9 × 3
##   title                                          runtime money   
##   <chr>                                          <chr>   <chr>   
## 1 Star Wars: Episode I - The Phantom Menace      136 min $474.54M
## 2 Star Wars: Episode II - Attack of the Clones   142 min $310.68M
## 3 Star Wars: Episode III - Revenge of the Sith   140 min $380.26M
## 4 Star Wars                                      121 min $322.74M
## 5 Star Wars: Episode V - The Empire Strikes Back 124 min $290.48M
## 6 Star Wars: Episode VI - Return of the Jedi     131 min $309.13M
## 7 Star Wars: Episode VII - The Force Awakens     138 min $936.66M
## 8 Star Wars: Episode VIII - The Last Jedi        152 min $620.18M
## 9 Star Wars: The Rise Of Skywalker               141 min $515.20M
```


example w napoleon dynamite

```r
url = "https://www.amazon.com/product-reviews/B00005JNBQ/ref=cm_cr_arp_d_viewopt_rvwer?ie=UTF8&reviewerType=avp_only_reviews&sortBy=recent&pageNumber=1"

dynamite_html = read_html(url)

review_titles = 
  dynamite_html %>%
  html_elements(".a-text-bold span") %>%
  html_text()

review_stars = 
  dynamite_html %>%
  html_elements("#cm_cr-review_list .review-rating") %>%
  html_text()

review_text = 
  dynamite_html %>%
  html_elements(".review-text-content span") %>%
  html_text()

reviews = tibble(
  title = review_titles,
  stars = review_stars,
  text = review_text
)

reviews
```

```
## # A tibble: 10 × 3
##    title                                         stars              text        
##    <chr>                                         <chr>              <chr>       
##  1 Quirky                                        5.0 out of 5 stars Good family…
##  2 Funny movie - can't play it !                 1.0 out of 5 stars Sony 4k pla…
##  3 A brilliant story about teenage life          5.0 out of 5 stars Napoleon Dy…
##  4 HUHYAH                                        5.0 out of 5 stars Spicy       
##  5 Cult Classic                                  4.0 out of 5 stars Takes a tim…
##  6 Sweet                                         5.0 out of 5 stars Timeless Mo…
##  7 Cute                                          4.0 out of 5 stars Fun         
##  8 great collectible                             5.0 out of 5 stars one of the …
##  9 Iconic, hilarious flick ! About friend ship . 5.0 out of 5 stars Who doesn’t…
## 10 Funny                                         5.0 out of 5 stars Me and my d…
```



# Using an API

nyc open data

as a csv file

```r
nyc_water = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.csv") %>% 
  content("parsed")
```

```
## Rows: 43 Columns: 4
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (4): year, new_york_city_population, nyc_consumption_million_gallons_per...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
nyc_water
```

```
## # A tibble: 43 × 4
##     year new_york_city_population nyc_consumption_million_gallons_per_…¹ per_c…²
##    <dbl>                    <dbl>                                  <dbl>   <dbl>
##  1  1979                  7102100                                   1512     213
##  2  1980                  7071639                                   1506     213
##  3  1981                  7089241                                   1309     185
##  4  1982                  7109105                                   1382     194
##  5  1983                  7181224                                   1424     198
##  6  1984                  7234514                                   1465     203
##  7  1985                  7274054                                   1326     182
##  8  1986                  7319246                                   1351     185
##  9  1987                  7342476                                   1447     197
## 10  1988                  7353719                                   1484     202
## # … with 33 more rows, and abbreviated variable names
## #   ¹​nyc_consumption_million_gallons_per_day,
## #   ²​per_capita_gallons_per_person_per_day
```

as a JSON file

```r
nyc_water = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.json") %>% 
  content("text") %>%
  jsonlite::fromJSON() %>%
  as_tibble()
nyc_water
```

```
## # A tibble: 43 × 4
##    year  new_york_city_population nyc_consumption_million_gallons_per_…¹ per_c…²
##    <chr> <chr>                    <chr>                                  <chr>  
##  1 1979  7102100                  1512                                   213    
##  2 1980  7071639                  1506                                   213    
##  3 1981  7089241                  1309                                   185    
##  4 1982  7109105                  1382                                   194    
##  5 1983  7181224                  1424                                   198    
##  6 1984  7234514                  1465                                   203    
##  7 1985  7274054                  1326                                   182    
##  8 1986  7319246                  1351                                   185    
##  9 1987  7342476                  1447                                   197    
## 10 1988  7353719                  1484                                   202    
## # … with 33 more rows, and abbreviated variable names
## #   ¹​nyc_consumption_million_gallons_per_day,
## #   ²​per_capita_gallons_per_person_per_day
```

data.gov

```r
brfss_smart2010 = 
  GET("https://chronicdata.cdc.gov/resource/acme-vg9e.csv",
      query = list("$limit" = 5000)) %>% 
  content("parsed")
```

```
## Rows: 5000 Columns: 23
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
## lgl  (1): locationid
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
brfss_smart2010
```

```
## # A tibble: 5,000 × 23
##     year locationa…¹ locat…² class topic quest…³ respo…⁴ sampl…⁵ data_…⁶ confi…⁷
##    <dbl> <chr>       <chr>   <chr> <chr> <chr>   <chr>     <dbl>   <dbl>   <dbl>
##  1  2010 AL          AL - M… Heal… Over… How is… Excell…      91    15.6    11  
##  2  2010 AL          AL - J… Heal… Over… How is… Excell…      94    18.9    14.1
##  3  2010 AL          AL - T… Heal… Over… How is… Excell…      58    20.8    14.1
##  4  2010 AL          AL - J… Heal… Over… How is… Very g…     148    30      24.9
##  5  2010 AL          AL - T… Heal… Over… How is… Very g…     109    29.5    23.2
##  6  2010 AL          AL - M… Heal… Over… How is… Very g…     177    31.3    26  
##  7  2010 AL          AL - J… Heal… Over… How is… Good        208    33.1    28.2
##  8  2010 AL          AL - M… Heal… Over… How is… Good        224    31.2    26.1
##  9  2010 AL          AL - T… Heal… Over… How is… Good        171    33.8    27.7
## 10  2010 AL          AL - M… Heal… Over… How is… Fair        120    15.5    11.7
## # … with 4,990 more rows, 13 more variables: confidence_limit_high <dbl>,
## #   display_order <dbl>, data_value_unit <chr>, data_value_type <chr>,
## #   data_value_footnote_symbol <chr>, data_value_footnote <chr>,
## #   datasource <chr>, classid <chr>, topicid <chr>, locationid <lgl>,
## #   questionid <chr>, respid <chr>, geolocation <chr>, and abbreviated variable
## #   names ¹​locationabbr, ²​locationdesc, ³​question, ⁴​response, ⁵​sample_size,
## #   ⁶​data_value, ⁷​confidence_limit_low
```
By default, the CDC API limits data to the first 1000 rows. Here I’ve increased that by changing an element of the API query – I looked around the website describing the API to find the name of the argument, and then used the appropriate syntax for GET. To get the full data, I could increase this so that I get all the data at once or I could try iterating over chunks of a few thousand rows.

pokemon api (more complicated)

```r
poke = 
  GET("http://pokeapi.co/api/v2/pokemon/1") %>%
  content()
poke
```

```
## $abilities
## $abilities[[1]]
## $abilities[[1]]$ability
## $abilities[[1]]$ability$name
## [1] "overgrow"
## 
## $abilities[[1]]$ability$url
## [1] "https://pokeapi.co/api/v2/ability/65/"
## 
## 
## $abilities[[1]]$is_hidden
## [1] FALSE
## 
## $abilities[[1]]$slot
## [1] 1
## 
## 
## $abilities[[2]]
## $abilities[[2]]$ability
## $abilities[[2]]$ability$name
## [1] "chlorophyll"
## 
## $abilities[[2]]$ability$url
## [1] "https://pokeapi.co/api/v2/ability/34/"
## 
## 
## $abilities[[2]]$is_hidden
## [1] TRUE
## 
## $abilities[[2]]$slot
## [1] 3
## 
## 
## 
## $base_experience
## [1] 64
## 
## $forms
## $forms[[1]]
## $forms[[1]]$name
## [1] "bulbasaur"
## 
## $forms[[1]]$url
## [1] "https://pokeapi.co/api/v2/pokemon-form/1/"
## 
## 
## 
## $game_indices
## $game_indices[[1]]
## $game_indices[[1]]$game_index
## [1] 153
## 
## $game_indices[[1]]$version
## $game_indices[[1]]$version$name
## [1] "red"
## 
## $game_indices[[1]]$version$url
## [1] "https://pokeapi.co/api/v2/version/1/"
## 
## 
## 
## $game_indices[[2]]
## $game_indices[[2]]$game_index
## [1] 153
## 
## $game_indices[[2]]$version
## $game_indices[[2]]$version$name
## [1] "blue"
## 
## $game_indices[[2]]$version$url
## [1] "https://pokeapi.co/api/v2/version/2/"
## 
## 
## 
## $game_indices[[3]]
## $game_indices[[3]]$game_index
## [1] 153
## 
## $game_indices[[3]]$version
## $game_indices[[3]]$version$name
## [1] "yellow"
## 
## $game_indices[[3]]$version$url
## [1] "https://pokeapi.co/api/v2/version/3/"
## 
## 
## 
## $game_indices[[4]]
## $game_indices[[4]]$game_index
## [1] 1
## 
## $game_indices[[4]]$version
## $game_indices[[4]]$version$name
## [1] "gold"
## 
## $game_indices[[4]]$version$url
## [1] "https://pokeapi.co/api/v2/version/4/"
## 
## 
## 
## $game_indices[[5]]
## $game_indices[[5]]$game_index
## [1] 1
## 
## $game_indices[[5]]$version
## $game_indices[[5]]$version$name
## [1] "silver"
## 
## $game_indices[[5]]$version$url
## [1] "https://pokeapi.co/api/v2/version/5/"
## 
## 
## 
## $game_indices[[6]]
## $game_indices[[6]]$game_index
## [1] 1
## 
## $game_indices[[6]]$version
## $game_indices[[6]]$version$name
## [1] "crystal"
## 
## $game_indices[[6]]$version$url
## [1] "https://pokeapi.co/api/v2/version/6/"
## 
## 
## 
## $game_indices[[7]]
## $game_indices[[7]]$game_index
## [1] 1
## 
## $game_indices[[7]]$version
## $game_indices[[7]]$version$name
## [1] "ruby"
## 
## $game_indices[[7]]$version$url
## [1] "https://pokeapi.co/api/v2/version/7/"
## 
## 
## 
## $game_indices[[8]]
## $game_indices[[8]]$game_index
## [1] 1
## 
## $game_indices[[8]]$version
## $game_indices[[8]]$version$name
## [1] "sapphire"
## 
## $game_indices[[8]]$version$url
## [1] "https://pokeapi.co/api/v2/version/8/"
## 
## 
## 
## $game_indices[[9]]
## $game_indices[[9]]$game_index
## [1] 1
## 
## $game_indices[[9]]$version
## $game_indices[[9]]$version$name
## [1] "emerald"
## 
## $game_indices[[9]]$version$url
## [1] "https://pokeapi.co/api/v2/version/9/"
## 
## 
## 
## $game_indices[[10]]
## $game_indices[[10]]$game_index
## [1] 1
## 
## $game_indices[[10]]$version
## $game_indices[[10]]$version$name
## [1] "firered"
## 
## $game_indices[[10]]$version$url
## [1] "https://pokeapi.co/api/v2/version/10/"
## 
## 
## 
## $game_indices[[11]]
## $game_indices[[11]]$game_index
## [1] 1
## 
## $game_indices[[11]]$version
## $game_indices[[11]]$version$name
## [1] "leafgreen"
## 
## $game_indices[[11]]$version$url
## [1] "https://pokeapi.co/api/v2/version/11/"
## 
## 
## 
## $game_indices[[12]]
## $game_indices[[12]]$game_index
## [1] 1
## 
## $game_indices[[12]]$version
## $game_indices[[12]]$version$name
## [1] "diamond"
## 
## $game_indices[[12]]$version$url
## [1] "https://pokeapi.co/api/v2/version/12/"
## 
## 
## 
## $game_indices[[13]]
## $game_indices[[13]]$game_index
## [1] 1
## 
## $game_indices[[13]]$version
## $game_indices[[13]]$version$name
## [1] "pearl"
## 
## $game_indices[[13]]$version$url
## [1] "https://pokeapi.co/api/v2/version/13/"
## 
## 
## 
## $game_indices[[14]]
## $game_indices[[14]]$game_index
## [1] 1
## 
## $game_indices[[14]]$version
## $game_indices[[14]]$version$name
## [1] "platinum"
## 
## $game_indices[[14]]$version$url
## [1] "https://pokeapi.co/api/v2/version/14/"
## 
## 
## 
## $game_indices[[15]]
## $game_indices[[15]]$game_index
## [1] 1
## 
## $game_indices[[15]]$version
## $game_indices[[15]]$version$name
## [1] "heartgold"
## 
## $game_indices[[15]]$version$url
## [1] "https://pokeapi.co/api/v2/version/15/"
## 
## 
## 
## $game_indices[[16]]
## $game_indices[[16]]$game_index
## [1] 1
## 
## $game_indices[[16]]$version
## $game_indices[[16]]$version$name
## [1] "soulsilver"
## 
## $game_indices[[16]]$version$url
## [1] "https://pokeapi.co/api/v2/version/16/"
## 
## 
## 
## $game_indices[[17]]
## $game_indices[[17]]$game_index
## [1] 1
## 
## $game_indices[[17]]$version
## $game_indices[[17]]$version$name
## [1] "black"
## 
## $game_indices[[17]]$version$url
## [1] "https://pokeapi.co/api/v2/version/17/"
## 
## 
## 
## $game_indices[[18]]
## $game_indices[[18]]$game_index
## [1] 1
## 
## $game_indices[[18]]$version
## $game_indices[[18]]$version$name
## [1] "white"
## 
## $game_indices[[18]]$version$url
## [1] "https://pokeapi.co/api/v2/version/18/"
## 
## 
## 
## $game_indices[[19]]
## $game_indices[[19]]$game_index
## [1] 1
## 
## $game_indices[[19]]$version
## $game_indices[[19]]$version$name
## [1] "black-2"
## 
## $game_indices[[19]]$version$url
## [1] "https://pokeapi.co/api/v2/version/21/"
## 
## 
## 
## $game_indices[[20]]
## $game_indices[[20]]$game_index
## [1] 1
## 
## $game_indices[[20]]$version
## $game_indices[[20]]$version$name
## [1] "white-2"
## 
## $game_indices[[20]]$version$url
## [1] "https://pokeapi.co/api/v2/version/22/"
## 
## 
## 
## 
## $height
## [1] 7
## 
## $held_items
## list()
## 
## $id
## [1] 1
## 
## $is_default
## [1] TRUE
## 
## $location_area_encounters
## [1] "https://pokeapi.co/api/v2/pokemon/1/encounters"
## 
## $moves
## $moves[[1]]
## $moves[[1]]$move
## $moves[[1]]$move$name
## [1] "razor-wind"
## 
## $moves[[1]]$move$url
## [1] "https://pokeapi.co/api/v2/move/13/"
## 
## 
## $moves[[1]]$version_group_details
## $moves[[1]]$version_group_details[[1]]
## $moves[[1]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[1]]$version_group_details[[1]]$move_learn_method
## $moves[[1]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[1]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[1]]$version_group_details[[1]]$version_group
## $moves[[1]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[1]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[1]]$version_group_details[[2]]
## $moves[[1]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[1]]$version_group_details[[2]]$move_learn_method
## $moves[[1]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[1]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[1]]$version_group_details[[2]]$version_group
## $moves[[1]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[1]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## 
## 
## $moves[[2]]
## $moves[[2]]$move
## $moves[[2]]$move$name
## [1] "swords-dance"
## 
## $moves[[2]]$move$url
## [1] "https://pokeapi.co/api/v2/move/14/"
## 
## 
## $moves[[2]]$version_group_details
## $moves[[2]]$version_group_details[[1]]
## $moves[[2]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[1]]$move_learn_method
## $moves[[2]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[1]]$version_group
## $moves[[2]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[2]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[2]]$version_group_details[[2]]
## $moves[[2]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[2]]$move_learn_method
## $moves[[2]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[2]]$version_group
## $moves[[2]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[2]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[2]]$version_group_details[[3]]
## $moves[[2]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[3]]$move_learn_method
## $moves[[2]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[2]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[2]]$version_group_details[[3]]$version_group
## $moves[[2]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[2]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[2]]$version_group_details[[4]]
## $moves[[2]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[4]]$move_learn_method
## $moves[[2]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[2]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[2]]$version_group_details[[4]]$version_group
## $moves[[2]]$version_group_details[[4]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[2]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[2]]$version_group_details[[5]]
## $moves[[2]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[5]]$move_learn_method
## $moves[[2]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[5]]$version_group
## $moves[[2]]$version_group_details[[5]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[2]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[2]]$version_group_details[[6]]
## $moves[[2]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[6]]$move_learn_method
## $moves[[2]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[6]]$version_group
## $moves[[2]]$version_group_details[[6]]$version_group$name
## [1] "platinum"
## 
## $moves[[2]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[2]]$version_group_details[[7]]
## $moves[[2]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[7]]$move_learn_method
## $moves[[2]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[7]]$version_group
## $moves[[2]]$version_group_details[[7]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[2]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[2]]$version_group_details[[8]]
## $moves[[2]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[8]]$move_learn_method
## $moves[[2]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[8]]$version_group
## $moves[[2]]$version_group_details[[8]]$version_group$name
## [1] "black-white"
## 
## $moves[[2]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[2]]$version_group_details[[9]]
## $moves[[2]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[9]]$move_learn_method
## $moves[[2]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[9]]$version_group
## $moves[[2]]$version_group_details[[9]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[2]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[2]]$version_group_details[[10]]
## $moves[[2]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[10]]$move_learn_method
## $moves[[2]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[10]]$version_group
## $moves[[2]]$version_group_details[[10]]$version_group$name
## [1] "x-y"
## 
## $moves[[2]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[2]]$version_group_details[[11]]
## $moves[[2]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[11]]$move_learn_method
## $moves[[2]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[11]]$version_group
## $moves[[2]]$version_group_details[[11]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[2]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[2]]$version_group_details[[12]]
## $moves[[2]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[12]]$move_learn_method
## $moves[[2]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[12]]$version_group
## $moves[[2]]$version_group_details[[12]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[2]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[2]]$version_group_details[[13]]
## $moves[[2]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[13]]$move_learn_method
## $moves[[2]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[13]]$version_group
## $moves[[2]]$version_group_details[[13]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[2]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[2]]$version_group_details[[14]]
## $moves[[2]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[2]]$version_group_details[[14]]$move_learn_method
## $moves[[2]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[2]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[2]]$version_group_details[[14]]$version_group
## $moves[[2]]$version_group_details[[14]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[2]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[3]]
## $moves[[3]]$move
## $moves[[3]]$move$name
## [1] "cut"
## 
## $moves[[3]]$move$url
## [1] "https://pokeapi.co/api/v2/move/15/"
## 
## 
## $moves[[3]]$version_group_details
## $moves[[3]]$version_group_details[[1]]
## $moves[[3]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[1]]$move_learn_method
## $moves[[3]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[1]]$version_group
## $moves[[3]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[3]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[3]]$version_group_details[[2]]
## $moves[[3]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[2]]$move_learn_method
## $moves[[3]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[2]]$version_group
## $moves[[3]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[3]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[3]]$version_group_details[[3]]
## $moves[[3]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[3]]$move_learn_method
## $moves[[3]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[3]]$version_group
## $moves[[3]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[3]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[3]]$version_group_details[[4]]
## $moves[[3]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[4]]$move_learn_method
## $moves[[3]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[4]]$version_group
## $moves[[3]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[3]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[3]]$version_group_details[[5]]
## $moves[[3]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[5]]$move_learn_method
## $moves[[3]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[5]]$version_group
## $moves[[3]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[3]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[3]]$version_group_details[[6]]
## $moves[[3]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[6]]$move_learn_method
## $moves[[3]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[6]]$version_group
## $moves[[3]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[3]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[3]]$version_group_details[[7]]
## $moves[[3]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[7]]$move_learn_method
## $moves[[3]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[7]]$version_group
## $moves[[3]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[3]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[3]]$version_group_details[[8]]
## $moves[[3]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[8]]$move_learn_method
## $moves[[3]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[8]]$version_group
## $moves[[3]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[3]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[3]]$version_group_details[[9]]
## $moves[[3]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[9]]$move_learn_method
## $moves[[3]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[9]]$version_group
## $moves[[3]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[3]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[3]]$version_group_details[[10]]
## $moves[[3]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[10]]$move_learn_method
## $moves[[3]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[10]]$version_group
## $moves[[3]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[3]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[3]]$version_group_details[[11]]
## $moves[[3]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[11]]$move_learn_method
## $moves[[3]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[11]]$version_group
## $moves[[3]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[3]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[3]]$version_group_details[[12]]
## $moves[[3]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[12]]$move_learn_method
## $moves[[3]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[12]]$version_group
## $moves[[3]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[3]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[3]]$version_group_details[[13]]
## $moves[[3]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[13]]$move_learn_method
## $moves[[3]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[13]]$version_group
## $moves[[3]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[3]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[3]]$version_group_details[[14]]
## $moves[[3]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[14]]$move_learn_method
## $moves[[3]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[14]]$version_group
## $moves[[3]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[3]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[3]]$version_group_details[[15]]
## $moves[[3]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[15]]$move_learn_method
## $moves[[3]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[15]]$version_group
## $moves[[3]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[3]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[3]]$version_group_details[[16]]
## $moves[[3]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[3]]$version_group_details[[16]]$move_learn_method
## $moves[[3]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[3]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[3]]$version_group_details[[16]]$version_group
## $moves[[3]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[3]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## 
## 
## $moves[[4]]
## $moves[[4]]$move
## $moves[[4]]$move$name
## [1] "bind"
## 
## $moves[[4]]$move$url
## [1] "https://pokeapi.co/api/v2/move/20/"
## 
## 
## $moves[[4]]$version_group_details
## $moves[[4]]$version_group_details[[1]]
## $moves[[4]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[4]]$version_group_details[[1]]$move_learn_method
## $moves[[4]]$version_group_details[[1]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[4]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[4]]$version_group_details[[1]]$version_group
## $moves[[4]]$version_group_details[[1]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[4]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[4]]$version_group_details[[2]]
## $moves[[4]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[4]]$version_group_details[[2]]$move_learn_method
## $moves[[4]]$version_group_details[[2]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[4]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[4]]$version_group_details[[2]]$version_group
## $moves[[4]]$version_group_details[[2]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[4]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[4]]$version_group_details[[3]]
## $moves[[4]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[4]]$version_group_details[[3]]$move_learn_method
## $moves[[4]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[4]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[4]]$version_group_details[[3]]$version_group
## $moves[[4]]$version_group_details[[3]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[4]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[5]]
## $moves[[5]]$move
## $moves[[5]]$move$name
## [1] "vine-whip"
## 
## $moves[[5]]$move$url
## [1] "https://pokeapi.co/api/v2/move/22/"
## 
## 
## $moves[[5]]$version_group_details
## $moves[[5]]$version_group_details[[1]]
## $moves[[5]]$version_group_details[[1]]$level_learned_at
## [1] 13
## 
## $moves[[5]]$version_group_details[[1]]$move_learn_method
## $moves[[5]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[1]]$version_group
## $moves[[5]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[5]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[5]]$version_group_details[[2]]
## $moves[[5]]$version_group_details[[2]]$level_learned_at
## [1] 13
## 
## $moves[[5]]$version_group_details[[2]]$move_learn_method
## $moves[[5]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[2]]$version_group
## $moves[[5]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[5]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[5]]$version_group_details[[3]]
## $moves[[5]]$version_group_details[[3]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[3]]$move_learn_method
## $moves[[5]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[3]]$version_group
## $moves[[5]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[5]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[5]]$version_group_details[[4]]
## $moves[[5]]$version_group_details[[4]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[4]]$move_learn_method
## $moves[[5]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[4]]$version_group
## $moves[[5]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[5]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[5]]$version_group_details[[5]]
## $moves[[5]]$version_group_details[[5]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[5]]$move_learn_method
## $moves[[5]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[5]]$version_group
## $moves[[5]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[5]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[5]]$version_group_details[[6]]
## $moves[[5]]$version_group_details[[6]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[6]]$move_learn_method
## $moves[[5]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[6]]$version_group
## $moves[[5]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[5]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[5]]$version_group_details[[7]]
## $moves[[5]]$version_group_details[[7]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[7]]$move_learn_method
## $moves[[5]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[7]]$version_group
## $moves[[5]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[5]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[5]]$version_group_details[[8]]
## $moves[[5]]$version_group_details[[8]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[8]]$move_learn_method
## $moves[[5]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[8]]$version_group
## $moves[[5]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[5]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[5]]$version_group_details[[9]]
## $moves[[5]]$version_group_details[[9]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[9]]$move_learn_method
## $moves[[5]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[9]]$version_group
## $moves[[5]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[5]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[5]]$version_group_details[[10]]
## $moves[[5]]$version_group_details[[10]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[10]]$move_learn_method
## $moves[[5]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[10]]$version_group
## $moves[[5]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[5]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[5]]$version_group_details[[11]]
## $moves[[5]]$version_group_details[[11]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[11]]$move_learn_method
## $moves[[5]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[11]]$version_group
## $moves[[5]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[5]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[5]]$version_group_details[[12]]
## $moves[[5]]$version_group_details[[12]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[12]]$move_learn_method
## $moves[[5]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[12]]$version_group
## $moves[[5]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[5]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[5]]$version_group_details[[13]]
## $moves[[5]]$version_group_details[[13]]$level_learned_at
## [1] 10
## 
## $moves[[5]]$version_group_details[[13]]$move_learn_method
## $moves[[5]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[13]]$version_group
## $moves[[5]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[5]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[5]]$version_group_details[[14]]
## $moves[[5]]$version_group_details[[14]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[14]]$move_learn_method
## $moves[[5]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[14]]$version_group
## $moves[[5]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[5]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[5]]$version_group_details[[15]]
## $moves[[5]]$version_group_details[[15]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[15]]$move_learn_method
## $moves[[5]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[15]]$version_group
## $moves[[5]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[5]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[5]]$version_group_details[[16]]
## $moves[[5]]$version_group_details[[16]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[16]]$move_learn_method
## $moves[[5]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[16]]$version_group
## $moves[[5]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[5]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[5]]$version_group_details[[17]]
## $moves[[5]]$version_group_details[[17]]$level_learned_at
## [1] 7
## 
## $moves[[5]]$version_group_details[[17]]$move_learn_method
## $moves[[5]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[17]]$version_group
## $moves[[5]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[5]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[5]]$version_group_details[[18]]
## $moves[[5]]$version_group_details[[18]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[18]]$move_learn_method
## $moves[[5]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[18]]$version_group
## $moves[[5]]$version_group_details[[18]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[5]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[5]]$version_group_details[[19]]
## $moves[[5]]$version_group_details[[19]]$level_learned_at
## [1] 9
## 
## $moves[[5]]$version_group_details[[19]]$move_learn_method
## $moves[[5]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[19]]$version_group
## $moves[[5]]$version_group_details[[19]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[5]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[5]]$version_group_details[[20]]
## $moves[[5]]$version_group_details[[20]]$level_learned_at
## [1] 5
## 
## $moves[[5]]$version_group_details[[20]]$move_learn_method
## $moves[[5]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[20]]$version_group
## $moves[[5]]$version_group_details[[20]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[5]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[5]]$version_group_details[[21]]
## $moves[[5]]$version_group_details[[21]]$level_learned_at
## [1] 3
## 
## $moves[[5]]$version_group_details[[21]]$move_learn_method
## $moves[[5]]$version_group_details[[21]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[5]]$version_group_details[[21]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[5]]$version_group_details[[21]]$version_group
## $moves[[5]]$version_group_details[[21]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[5]]$version_group_details[[21]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[6]]
## $moves[[6]]$move
## $moves[[6]]$move$name
## [1] "headbutt"
## 
## $moves[[6]]$move$url
## [1] "https://pokeapi.co/api/v2/move/29/"
## 
## 
## $moves[[6]]$version_group_details
## $moves[[6]]$version_group_details[[1]]
## $moves[[6]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[6]]$version_group_details[[1]]$move_learn_method
## $moves[[6]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[6]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[6]]$version_group_details[[1]]$version_group
## $moves[[6]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[6]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[6]]$version_group_details[[2]]
## $moves[[6]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[6]]$version_group_details[[2]]$move_learn_method
## $moves[[6]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[6]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[6]]$version_group_details[[2]]$version_group
## $moves[[6]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[6]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[6]]$version_group_details[[3]]
## $moves[[6]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[6]]$version_group_details[[3]]$move_learn_method
## $moves[[6]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[6]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[6]]$version_group_details[[3]]$version_group
## $moves[[6]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[6]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[6]]$version_group_details[[4]]
## $moves[[6]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[6]]$version_group_details[[4]]$move_learn_method
## $moves[[6]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[6]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[6]]$version_group_details[[4]]$version_group
## $moves[[6]]$version_group_details[[4]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[6]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## 
## 
## $moves[[7]]
## $moves[[7]]$move
## $moves[[7]]$move$name
## [1] "tackle"
## 
## $moves[[7]]$move$url
## [1] "https://pokeapi.co/api/v2/move/33/"
## 
## 
## $moves[[7]]$version_group_details
## $moves[[7]]$version_group_details[[1]]
## $moves[[7]]$version_group_details[[1]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[1]]$move_learn_method
## $moves[[7]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[1]]$version_group
## $moves[[7]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[7]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[7]]$version_group_details[[2]]
## $moves[[7]]$version_group_details[[2]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[2]]$move_learn_method
## $moves[[7]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[2]]$version_group
## $moves[[7]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[7]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[7]]$version_group_details[[3]]
## $moves[[7]]$version_group_details[[3]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[3]]$move_learn_method
## $moves[[7]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[3]]$version_group
## $moves[[7]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[7]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[7]]$version_group_details[[4]]
## $moves[[7]]$version_group_details[[4]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[4]]$move_learn_method
## $moves[[7]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[4]]$version_group
## $moves[[7]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[7]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[7]]$version_group_details[[5]]
## $moves[[7]]$version_group_details[[5]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[5]]$move_learn_method
## $moves[[7]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[5]]$version_group
## $moves[[7]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[7]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[7]]$version_group_details[[6]]
## $moves[[7]]$version_group_details[[6]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[6]]$move_learn_method
## $moves[[7]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[6]]$version_group
## $moves[[7]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[7]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[7]]$version_group_details[[7]]
## $moves[[7]]$version_group_details[[7]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[7]]$move_learn_method
## $moves[[7]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[7]]$version_group
## $moves[[7]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[7]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[7]]$version_group_details[[8]]
## $moves[[7]]$version_group_details[[8]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[8]]$move_learn_method
## $moves[[7]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[8]]$version_group
## $moves[[7]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[7]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[7]]$version_group_details[[9]]
## $moves[[7]]$version_group_details[[9]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[9]]$move_learn_method
## $moves[[7]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[9]]$version_group
## $moves[[7]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[7]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[7]]$version_group_details[[10]]
## $moves[[7]]$version_group_details[[10]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[10]]$move_learn_method
## $moves[[7]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[10]]$version_group
## $moves[[7]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[7]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[7]]$version_group_details[[11]]
## $moves[[7]]$version_group_details[[11]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[11]]$move_learn_method
## $moves[[7]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[11]]$version_group
## $moves[[7]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[7]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[7]]$version_group_details[[12]]
## $moves[[7]]$version_group_details[[12]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[12]]$move_learn_method
## $moves[[7]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[12]]$version_group
## $moves[[7]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[7]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[7]]$version_group_details[[13]]
## $moves[[7]]$version_group_details[[13]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[13]]$move_learn_method
## $moves[[7]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[13]]$version_group
## $moves[[7]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[7]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[7]]$version_group_details[[14]]
## $moves[[7]]$version_group_details[[14]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[14]]$move_learn_method
## $moves[[7]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[14]]$version_group
## $moves[[7]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[7]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[7]]$version_group_details[[15]]
## $moves[[7]]$version_group_details[[15]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[15]]$move_learn_method
## $moves[[7]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[15]]$version_group
## $moves[[7]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[7]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[7]]$version_group_details[[16]]
## $moves[[7]]$version_group_details[[16]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[16]]$move_learn_method
## $moves[[7]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[16]]$version_group
## $moves[[7]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[7]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[7]]$version_group_details[[17]]
## $moves[[7]]$version_group_details[[17]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[17]]$move_learn_method
## $moves[[7]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[17]]$version_group
## $moves[[7]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[7]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[7]]$version_group_details[[18]]
## $moves[[7]]$version_group_details[[18]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[18]]$move_learn_method
## $moves[[7]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[18]]$version_group
## $moves[[7]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[7]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[7]]$version_group_details[[19]]
## $moves[[7]]$version_group_details[[19]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[19]]$move_learn_method
## $moves[[7]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[19]]$version_group
## $moves[[7]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[7]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[7]]$version_group_details[[20]]
## $moves[[7]]$version_group_details[[20]]$level_learned_at
## [1] 1
## 
## $moves[[7]]$version_group_details[[20]]$move_learn_method
## $moves[[7]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[7]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[7]]$version_group_details[[20]]$version_group
## $moves[[7]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[7]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[8]]
## $moves[[8]]$move
## $moves[[8]]$move$name
## [1] "body-slam"
## 
## $moves[[8]]$move$url
## [1] "https://pokeapi.co/api/v2/move/34/"
## 
## 
## $moves[[8]]$version_group_details
## $moves[[8]]$version_group_details[[1]]
## $moves[[8]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[8]]$version_group_details[[1]]$move_learn_method
## $moves[[8]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[8]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[8]]$version_group_details[[1]]$version_group
## $moves[[8]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[8]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[8]]$version_group_details[[2]]
## $moves[[8]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[8]]$version_group_details[[2]]$move_learn_method
## $moves[[8]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[8]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[8]]$version_group_details[[2]]$version_group
## $moves[[8]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[8]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[8]]$version_group_details[[3]]
## $moves[[8]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[8]]$version_group_details[[3]]$move_learn_method
## $moves[[8]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[8]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[8]]$version_group_details[[3]]$version_group
## $moves[[8]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[8]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[8]]$version_group_details[[4]]
## $moves[[8]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[8]]$version_group_details[[4]]$move_learn_method
## $moves[[8]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[8]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[8]]$version_group_details[[4]]$version_group
## $moves[[8]]$version_group_details[[4]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[8]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[8]]$version_group_details[[5]]
## $moves[[8]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[8]]$version_group_details[[5]]$move_learn_method
## $moves[[8]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[8]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[8]]$version_group_details[[5]]$version_group
## $moves[[8]]$version_group_details[[5]]$version_group$name
## [1] "xd"
## 
## $moves[[8]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[8]]$version_group_details[[6]]
## $moves[[8]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[8]]$version_group_details[[6]]$move_learn_method
## $moves[[8]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[8]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[8]]$version_group_details[[6]]$version_group
## $moves[[8]]$version_group_details[[6]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[8]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[9]]
## $moves[[9]]$move
## $moves[[9]]$move$name
## [1] "take-down"
## 
## $moves[[9]]$move$url
## [1] "https://pokeapi.co/api/v2/move/36/"
## 
## 
## $moves[[9]]$version_group_details
## $moves[[9]]$version_group_details[[1]]
## $moves[[9]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[9]]$version_group_details[[1]]$move_learn_method
## $moves[[9]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[9]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[9]]$version_group_details[[1]]$version_group
## $moves[[9]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[9]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[9]]$version_group_details[[2]]
## $moves[[9]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[9]]$version_group_details[[2]]$move_learn_method
## $moves[[9]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[9]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[9]]$version_group_details[[2]]$version_group
## $moves[[9]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[9]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[9]]$version_group_details[[3]]
## $moves[[9]]$version_group_details[[3]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[3]]$move_learn_method
## $moves[[9]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[3]]$version_group
## $moves[[9]]$version_group_details[[3]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[9]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[9]]$version_group_details[[4]]
## $moves[[9]]$version_group_details[[4]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[4]]$move_learn_method
## $moves[[9]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[4]]$version_group
## $moves[[9]]$version_group_details[[4]]$version_group$name
## [1] "platinum"
## 
## $moves[[9]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[9]]$version_group_details[[5]]
## $moves[[9]]$version_group_details[[5]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[5]]$move_learn_method
## $moves[[9]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[5]]$version_group
## $moves[[9]]$version_group_details[[5]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[9]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[9]]$version_group_details[[6]]
## $moves[[9]]$version_group_details[[6]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[6]]$move_learn_method
## $moves[[9]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[6]]$version_group
## $moves[[9]]$version_group_details[[6]]$version_group$name
## [1] "black-white"
## 
## $moves[[9]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[9]]$version_group_details[[7]]
## $moves[[9]]$version_group_details[[7]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[7]]$move_learn_method
## $moves[[9]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[7]]$version_group
## $moves[[9]]$version_group_details[[7]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[9]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[9]]$version_group_details[[8]]
## $moves[[9]]$version_group_details[[8]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[8]]$move_learn_method
## $moves[[9]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[8]]$version_group
## $moves[[9]]$version_group_details[[8]]$version_group$name
## [1] "x-y"
## 
## $moves[[9]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[9]]$version_group_details[[9]]
## $moves[[9]]$version_group_details[[9]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[9]]$move_learn_method
## $moves[[9]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[9]]$version_group
## $moves[[9]]$version_group_details[[9]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[9]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[9]]$version_group_details[[10]]
## $moves[[9]]$version_group_details[[10]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[10]]$move_learn_method
## $moves[[9]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[10]]$version_group
## $moves[[9]]$version_group_details[[10]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[9]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[9]]$version_group_details[[11]]
## $moves[[9]]$version_group_details[[11]]$level_learned_at
## [1] 15
## 
## $moves[[9]]$version_group_details[[11]]$move_learn_method
## $moves[[9]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[11]]$version_group
## $moves[[9]]$version_group_details[[11]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[9]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[9]]$version_group_details[[12]]
## $moves[[9]]$version_group_details[[12]]$level_learned_at
## [1] 18
## 
## $moves[[9]]$version_group_details[[12]]$move_learn_method
## $moves[[9]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[12]]$version_group
## $moves[[9]]$version_group_details[[12]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[9]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[9]]$version_group_details[[13]]
## $moves[[9]]$version_group_details[[13]]$level_learned_at
## [1] 21
## 
## $moves[[9]]$version_group_details[[13]]$move_learn_method
## $moves[[9]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[9]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[9]]$version_group_details[[13]]$version_group
## $moves[[9]]$version_group_details[[13]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[9]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[10]]
## $moves[[10]]$move
## $moves[[10]]$move$name
## [1] "double-edge"
## 
## $moves[[10]]$move$url
## [1] "https://pokeapi.co/api/v2/move/38/"
## 
## 
## $moves[[10]]$version_group_details
## $moves[[10]]$version_group_details[[1]]
## $moves[[10]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[10]]$version_group_details[[1]]$move_learn_method
## $moves[[10]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[10]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[10]]$version_group_details[[1]]$version_group
## $moves[[10]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[10]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[10]]$version_group_details[[2]]
## $moves[[10]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[10]]$version_group_details[[2]]$move_learn_method
## $moves[[10]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[10]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[10]]$version_group_details[[2]]$version_group
## $moves[[10]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[10]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[10]]$version_group_details[[3]]
## $moves[[10]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[10]]$version_group_details[[3]]$move_learn_method
## $moves[[10]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[10]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[10]]$version_group_details[[3]]$version_group
## $moves[[10]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[10]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[10]]$version_group_details[[4]]
## $moves[[10]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[10]]$version_group_details[[4]]$move_learn_method
## $moves[[10]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[10]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[10]]$version_group_details[[4]]$version_group
## $moves[[10]]$version_group_details[[4]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[10]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[10]]$version_group_details[[5]]
## $moves[[10]]$version_group_details[[5]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[5]]$move_learn_method
## $moves[[10]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[5]]$version_group
## $moves[[10]]$version_group_details[[5]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[10]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[10]]$version_group_details[[6]]
## $moves[[10]]$version_group_details[[6]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[6]]$move_learn_method
## $moves[[10]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[6]]$version_group
## $moves[[10]]$version_group_details[[6]]$version_group$name
## [1] "platinum"
## 
## $moves[[10]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[10]]$version_group_details[[7]]
## $moves[[10]]$version_group_details[[7]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[7]]$move_learn_method
## $moves[[10]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[7]]$version_group
## $moves[[10]]$version_group_details[[7]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[10]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[10]]$version_group_details[[8]]
## $moves[[10]]$version_group_details[[8]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[8]]$move_learn_method
## $moves[[10]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[8]]$version_group
## $moves[[10]]$version_group_details[[8]]$version_group$name
## [1] "black-white"
## 
## $moves[[10]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[10]]$version_group_details[[9]]
## $moves[[10]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[10]]$version_group_details[[9]]$move_learn_method
## $moves[[10]]$version_group_details[[9]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[10]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[10]]$version_group_details[[9]]$version_group
## $moves[[10]]$version_group_details[[9]]$version_group$name
## [1] "xd"
## 
## $moves[[10]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[10]]$version_group_details[[10]]
## $moves[[10]]$version_group_details[[10]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[10]]$move_learn_method
## $moves[[10]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[10]]$version_group
## $moves[[10]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[10]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[10]]$version_group_details[[11]]
## $moves[[10]]$version_group_details[[11]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[11]]$move_learn_method
## $moves[[10]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[11]]$version_group
## $moves[[10]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[10]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[10]]$version_group_details[[12]]
## $moves[[10]]$version_group_details[[12]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[12]]$move_learn_method
## $moves[[10]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[12]]$version_group
## $moves[[10]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[10]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[10]]$version_group_details[[13]]
## $moves[[10]]$version_group_details[[13]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[13]]$move_learn_method
## $moves[[10]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[13]]$version_group
## $moves[[10]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[10]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[10]]$version_group_details[[14]]
## $moves[[10]]$version_group_details[[14]]$level_learned_at
## [1] 27
## 
## $moves[[10]]$version_group_details[[14]]$move_learn_method
## $moves[[10]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[14]]$version_group
## $moves[[10]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[10]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[10]]$version_group_details[[15]]
## $moves[[10]]$version_group_details[[15]]$level_learned_at
## [1] 32
## 
## $moves[[10]]$version_group_details[[15]]$move_learn_method
## $moves[[10]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[15]]$version_group
## $moves[[10]]$version_group_details[[15]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[10]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[10]]$version_group_details[[16]]
## $moves[[10]]$version_group_details[[16]]$level_learned_at
## [1] 33
## 
## $moves[[10]]$version_group_details[[16]]$move_learn_method
## $moves[[10]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[10]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[10]]$version_group_details[[16]]$version_group
## $moves[[10]]$version_group_details[[16]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[10]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[11]]
## $moves[[11]]$move
## $moves[[11]]$move$name
## [1] "growl"
## 
## $moves[[11]]$move$url
## [1] "https://pokeapi.co/api/v2/move/45/"
## 
## 
## $moves[[11]]$version_group_details
## $moves[[11]]$version_group_details[[1]]
## $moves[[11]]$version_group_details[[1]]$level_learned_at
## [1] 1
## 
## $moves[[11]]$version_group_details[[1]]$move_learn_method
## $moves[[11]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[1]]$version_group
## $moves[[11]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[11]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[11]]$version_group_details[[2]]
## $moves[[11]]$version_group_details[[2]]$level_learned_at
## [1] 1
## 
## $moves[[11]]$version_group_details[[2]]$move_learn_method
## $moves[[11]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[2]]$version_group
## $moves[[11]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[11]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[11]]$version_group_details[[3]]
## $moves[[11]]$version_group_details[[3]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[3]]$move_learn_method
## $moves[[11]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[3]]$version_group
## $moves[[11]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[11]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[11]]$version_group_details[[4]]
## $moves[[11]]$version_group_details[[4]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[4]]$move_learn_method
## $moves[[11]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[4]]$version_group
## $moves[[11]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[11]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[11]]$version_group_details[[5]]
## $moves[[11]]$version_group_details[[5]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[5]]$move_learn_method
## $moves[[11]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[5]]$version_group
## $moves[[11]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[11]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[11]]$version_group_details[[6]]
## $moves[[11]]$version_group_details[[6]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[6]]$move_learn_method
## $moves[[11]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[6]]$version_group
## $moves[[11]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[11]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[11]]$version_group_details[[7]]
## $moves[[11]]$version_group_details[[7]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[7]]$move_learn_method
## $moves[[11]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[7]]$version_group
## $moves[[11]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[11]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[11]]$version_group_details[[8]]
## $moves[[11]]$version_group_details[[8]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[8]]$move_learn_method
## $moves[[11]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[8]]$version_group
## $moves[[11]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[11]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[11]]$version_group_details[[9]]
## $moves[[11]]$version_group_details[[9]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[9]]$move_learn_method
## $moves[[11]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[9]]$version_group
## $moves[[11]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[11]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[11]]$version_group_details[[10]]
## $moves[[11]]$version_group_details[[10]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[10]]$move_learn_method
## $moves[[11]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[10]]$version_group
## $moves[[11]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[11]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[11]]$version_group_details[[11]]
## $moves[[11]]$version_group_details[[11]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[11]]$move_learn_method
## $moves[[11]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[11]]$version_group
## $moves[[11]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[11]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[11]]$version_group_details[[12]]
## $moves[[11]]$version_group_details[[12]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[12]]$move_learn_method
## $moves[[11]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[12]]$version_group
## $moves[[11]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[11]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[11]]$version_group_details[[13]]
## $moves[[11]]$version_group_details[[13]]$level_learned_at
## [1] 4
## 
## $moves[[11]]$version_group_details[[13]]$move_learn_method
## $moves[[11]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[13]]$version_group
## $moves[[11]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[11]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[11]]$version_group_details[[14]]
## $moves[[11]]$version_group_details[[14]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[14]]$move_learn_method
## $moves[[11]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[14]]$version_group
## $moves[[11]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[11]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[11]]$version_group_details[[15]]
## $moves[[11]]$version_group_details[[15]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[15]]$move_learn_method
## $moves[[11]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[15]]$version_group
## $moves[[11]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[11]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[11]]$version_group_details[[16]]
## $moves[[11]]$version_group_details[[16]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[16]]$move_learn_method
## $moves[[11]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[16]]$version_group
## $moves[[11]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[11]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[11]]$version_group_details[[17]]
## $moves[[11]]$version_group_details[[17]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[17]]$move_learn_method
## $moves[[11]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[17]]$version_group
## $moves[[11]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[11]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[11]]$version_group_details[[18]]
## $moves[[11]]$version_group_details[[18]]$level_learned_at
## [1] 3
## 
## $moves[[11]]$version_group_details[[18]]$move_learn_method
## $moves[[11]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[18]]$version_group
## $moves[[11]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[11]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[11]]$version_group_details[[19]]
## $moves[[11]]$version_group_details[[19]]$level_learned_at
## [1] 1
## 
## $moves[[11]]$version_group_details[[19]]$move_learn_method
## $moves[[11]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[19]]$version_group
## $moves[[11]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[11]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[11]]$version_group_details[[20]]
## $moves[[11]]$version_group_details[[20]]$level_learned_at
## [1] 1
## 
## $moves[[11]]$version_group_details[[20]]$move_learn_method
## $moves[[11]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[11]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[11]]$version_group_details[[20]]$version_group
## $moves[[11]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[11]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[12]]
## $moves[[12]]$move
## $moves[[12]]$move$name
## [1] "strength"
## 
## $moves[[12]]$move$url
## [1] "https://pokeapi.co/api/v2/move/70/"
## 
## 
## $moves[[12]]$version_group_details
## $moves[[12]]$version_group_details[[1]]
## $moves[[12]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[1]]$move_learn_method
## $moves[[12]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[1]]$version_group
## $moves[[12]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[12]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[12]]$version_group_details[[2]]
## $moves[[12]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[2]]$move_learn_method
## $moves[[12]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[2]]$version_group
## $moves[[12]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[12]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[12]]$version_group_details[[3]]
## $moves[[12]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[3]]$move_learn_method
## $moves[[12]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[3]]$version_group
## $moves[[12]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[12]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[12]]$version_group_details[[4]]
## $moves[[12]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[4]]$move_learn_method
## $moves[[12]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[4]]$version_group
## $moves[[12]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[12]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[12]]$version_group_details[[5]]
## $moves[[12]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[5]]$move_learn_method
## $moves[[12]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[5]]$version_group
## $moves[[12]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[12]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[12]]$version_group_details[[6]]
## $moves[[12]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[6]]$move_learn_method
## $moves[[12]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[6]]$version_group
## $moves[[12]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[12]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[12]]$version_group_details[[7]]
## $moves[[12]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[7]]$move_learn_method
## $moves[[12]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[7]]$version_group
## $moves[[12]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[12]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[12]]$version_group_details[[8]]
## $moves[[12]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[8]]$move_learn_method
## $moves[[12]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[8]]$version_group
## $moves[[12]]$version_group_details[[8]]$version_group$name
## [1] "colosseum"
## 
## $moves[[12]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[12]]$version_group_details[[9]]
## $moves[[12]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[9]]$move_learn_method
## $moves[[12]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[9]]$version_group
## $moves[[12]]$version_group_details[[9]]$version_group$name
## [1] "xd"
## 
## $moves[[12]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[12]]$version_group_details[[10]]
## $moves[[12]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[10]]$move_learn_method
## $moves[[12]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[10]]$version_group
## $moves[[12]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[12]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[12]]$version_group_details[[11]]
## $moves[[12]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[11]]$move_learn_method
## $moves[[12]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[11]]$version_group
## $moves[[12]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[12]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[12]]$version_group_details[[12]]
## $moves[[12]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[12]]$version_group_details[[12]]$move_learn_method
## $moves[[12]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[12]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[12]]$version_group_details[[12]]$version_group
## $moves[[12]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[12]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## 
## 
## $moves[[13]]
## $moves[[13]]$move
## $moves[[13]]$move$name
## [1] "mega-drain"
## 
## $moves[[13]]$move$url
## [1] "https://pokeapi.co/api/v2/move/72/"
## 
## 
## $moves[[13]]$version_group_details
## $moves[[13]]$version_group_details[[1]]
## $moves[[13]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[13]]$version_group_details[[1]]$move_learn_method
## $moves[[13]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[13]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[13]]$version_group_details[[1]]$version_group
## $moves[[13]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[13]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[13]]$version_group_details[[2]]
## $moves[[13]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[13]]$version_group_details[[2]]$move_learn_method
## $moves[[13]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[13]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[13]]$version_group_details[[2]]$version_group
## $moves[[13]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[13]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[13]]$version_group_details[[3]]
## $moves[[13]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[13]]$version_group_details[[3]]$move_learn_method
## $moves[[13]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[13]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[13]]$version_group_details[[3]]$version_group
## $moves[[13]]$version_group_details[[3]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[13]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## 
## 
## $moves[[14]]
## $moves[[14]]$move
## $moves[[14]]$move$name
## [1] "leech-seed"
## 
## $moves[[14]]$move$url
## [1] "https://pokeapi.co/api/v2/move/73/"
## 
## 
## $moves[[14]]$version_group_details
## $moves[[14]]$version_group_details[[1]]
## $moves[[14]]$version_group_details[[1]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[1]]$move_learn_method
## $moves[[14]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[1]]$version_group
## $moves[[14]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[14]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[14]]$version_group_details[[2]]
## $moves[[14]]$version_group_details[[2]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[2]]$move_learn_method
## $moves[[14]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[2]]$version_group
## $moves[[14]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[14]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[14]]$version_group_details[[3]]
## $moves[[14]]$version_group_details[[3]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[3]]$move_learn_method
## $moves[[14]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[3]]$version_group
## $moves[[14]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[14]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[14]]$version_group_details[[4]]
## $moves[[14]]$version_group_details[[4]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[4]]$move_learn_method
## $moves[[14]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[4]]$version_group
## $moves[[14]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[14]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[14]]$version_group_details[[5]]
## $moves[[14]]$version_group_details[[5]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[5]]$move_learn_method
## $moves[[14]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[5]]$version_group
## $moves[[14]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[14]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[14]]$version_group_details[[6]]
## $moves[[14]]$version_group_details[[6]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[6]]$move_learn_method
## $moves[[14]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[6]]$version_group
## $moves[[14]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[14]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[14]]$version_group_details[[7]]
## $moves[[14]]$version_group_details[[7]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[7]]$move_learn_method
## $moves[[14]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[7]]$version_group
## $moves[[14]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[14]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[14]]$version_group_details[[8]]
## $moves[[14]]$version_group_details[[8]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[8]]$move_learn_method
## $moves[[14]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[8]]$version_group
## $moves[[14]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[14]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[14]]$version_group_details[[9]]
## $moves[[14]]$version_group_details[[9]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[9]]$move_learn_method
## $moves[[14]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[9]]$version_group
## $moves[[14]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[14]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[14]]$version_group_details[[10]]
## $moves[[14]]$version_group_details[[10]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[10]]$move_learn_method
## $moves[[14]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[10]]$version_group
## $moves[[14]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[14]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[14]]$version_group_details[[11]]
## $moves[[14]]$version_group_details[[11]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[11]]$move_learn_method
## $moves[[14]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[11]]$version_group
## $moves[[14]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[14]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[14]]$version_group_details[[12]]
## $moves[[14]]$version_group_details[[12]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[12]]$move_learn_method
## $moves[[14]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[12]]$version_group
## $moves[[14]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[14]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[14]]$version_group_details[[13]]
## $moves[[14]]$version_group_details[[13]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[13]]$move_learn_method
## $moves[[14]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[13]]$version_group
## $moves[[14]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[14]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[14]]$version_group_details[[14]]
## $moves[[14]]$version_group_details[[14]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[14]]$move_learn_method
## $moves[[14]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[14]]$version_group
## $moves[[14]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[14]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[14]]$version_group_details[[15]]
## $moves[[14]]$version_group_details[[15]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[15]]$move_learn_method
## $moves[[14]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[15]]$version_group
## $moves[[14]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[14]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[14]]$version_group_details[[16]]
## $moves[[14]]$version_group_details[[16]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[16]]$move_learn_method
## $moves[[14]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[16]]$version_group
## $moves[[14]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[14]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[14]]$version_group_details[[17]]
## $moves[[14]]$version_group_details[[17]]$level_learned_at
## [1] 7
## 
## $moves[[14]]$version_group_details[[17]]$move_learn_method
## $moves[[14]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[17]]$version_group
## $moves[[14]]$version_group_details[[17]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[14]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[14]]$version_group_details[[18]]
## $moves[[14]]$version_group_details[[18]]$level_learned_at
## [1] 9
## 
## $moves[[14]]$version_group_details[[18]]$move_learn_method
## $moves[[14]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[18]]$version_group
## $moves[[14]]$version_group_details[[18]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[14]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[14]]$version_group_details[[19]]
## $moves[[14]]$version_group_details[[19]]$level_learned_at
## [1] 9
## 
## $moves[[14]]$version_group_details[[19]]$move_learn_method
## $moves[[14]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[14]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[14]]$version_group_details[[19]]$version_group
## $moves[[14]]$version_group_details[[19]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[14]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[15]]
## $moves[[15]]$move
## $moves[[15]]$move$name
## [1] "growth"
## 
## $moves[[15]]$move$url
## [1] "https://pokeapi.co/api/v2/move/74/"
## 
## 
## $moves[[15]]$version_group_details
## $moves[[15]]$version_group_details[[1]]
## $moves[[15]]$version_group_details[[1]]$level_learned_at
## [1] 34
## 
## $moves[[15]]$version_group_details[[1]]$move_learn_method
## $moves[[15]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[1]]$version_group
## $moves[[15]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[15]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[15]]$version_group_details[[2]]
## $moves[[15]]$version_group_details[[2]]$level_learned_at
## [1] 34
## 
## $moves[[15]]$version_group_details[[2]]$move_learn_method
## $moves[[15]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[2]]$version_group
## $moves[[15]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[15]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[15]]$version_group_details[[3]]
## $moves[[15]]$version_group_details[[3]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[3]]$move_learn_method
## $moves[[15]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[3]]$version_group
## $moves[[15]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[15]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[15]]$version_group_details[[4]]
## $moves[[15]]$version_group_details[[4]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[4]]$move_learn_method
## $moves[[15]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[4]]$version_group
## $moves[[15]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[15]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[15]]$version_group_details[[5]]
## $moves[[15]]$version_group_details[[5]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[5]]$move_learn_method
## $moves[[15]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[5]]$version_group
## $moves[[15]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[15]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[15]]$version_group_details[[6]]
## $moves[[15]]$version_group_details[[6]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[6]]$move_learn_method
## $moves[[15]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[6]]$version_group
## $moves[[15]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[15]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[15]]$version_group_details[[7]]
## $moves[[15]]$version_group_details[[7]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[7]]$move_learn_method
## $moves[[15]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[7]]$version_group
## $moves[[15]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[15]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[15]]$version_group_details[[8]]
## $moves[[15]]$version_group_details[[8]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[8]]$move_learn_method
## $moves[[15]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[8]]$version_group
## $moves[[15]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[15]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[15]]$version_group_details[[9]]
## $moves[[15]]$version_group_details[[9]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[9]]$move_learn_method
## $moves[[15]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[9]]$version_group
## $moves[[15]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[15]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[15]]$version_group_details[[10]]
## $moves[[15]]$version_group_details[[10]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[10]]$move_learn_method
## $moves[[15]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[10]]$version_group
## $moves[[15]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[15]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[15]]$version_group_details[[11]]
## $moves[[15]]$version_group_details[[11]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[11]]$move_learn_method
## $moves[[15]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[11]]$version_group
## $moves[[15]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[15]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[15]]$version_group_details[[12]]
## $moves[[15]]$version_group_details[[12]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[12]]$move_learn_method
## $moves[[15]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[12]]$version_group
## $moves[[15]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[15]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[15]]$version_group_details[[13]]
## $moves[[15]]$version_group_details[[13]]$level_learned_at
## [1] 32
## 
## $moves[[15]]$version_group_details[[13]]$move_learn_method
## $moves[[15]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[13]]$version_group
## $moves[[15]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[15]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[15]]$version_group_details[[14]]
## $moves[[15]]$version_group_details[[14]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[14]]$move_learn_method
## $moves[[15]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[14]]$version_group
## $moves[[15]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[15]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[15]]$version_group_details[[15]]
## $moves[[15]]$version_group_details[[15]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[15]]$move_learn_method
## $moves[[15]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[15]]$version_group
## $moves[[15]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[15]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[15]]$version_group_details[[16]]
## $moves[[15]]$version_group_details[[16]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[16]]$move_learn_method
## $moves[[15]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[16]]$version_group
## $moves[[15]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[15]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[15]]$version_group_details[[17]]
## $moves[[15]]$version_group_details[[17]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[17]]$move_learn_method
## $moves[[15]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[17]]$version_group
## $moves[[15]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[15]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[15]]$version_group_details[[18]]
## $moves[[15]]$version_group_details[[18]]$level_learned_at
## [1] 25
## 
## $moves[[15]]$version_group_details[[18]]$move_learn_method
## $moves[[15]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[18]]$version_group
## $moves[[15]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[15]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[15]]$version_group_details[[19]]
## $moves[[15]]$version_group_details[[19]]$level_learned_at
## [1] 27
## 
## $moves[[15]]$version_group_details[[19]]$move_learn_method
## $moves[[15]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[19]]$version_group
## $moves[[15]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[15]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[15]]$version_group_details[[20]]
## $moves[[15]]$version_group_details[[20]]$level_learned_at
## [1] 6
## 
## $moves[[15]]$version_group_details[[20]]$move_learn_method
## $moves[[15]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[15]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[15]]$version_group_details[[20]]$version_group
## $moves[[15]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[15]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[16]]
## $moves[[16]]$move
## $moves[[16]]$move$name
## [1] "razor-leaf"
## 
## $moves[[16]]$move$url
## [1] "https://pokeapi.co/api/v2/move/75/"
## 
## 
## $moves[[16]]$version_group_details
## $moves[[16]]$version_group_details[[1]]
## $moves[[16]]$version_group_details[[1]]$level_learned_at
## [1] 27
## 
## $moves[[16]]$version_group_details[[1]]$move_learn_method
## $moves[[16]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[1]]$version_group
## $moves[[16]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[16]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[16]]$version_group_details[[2]]
## $moves[[16]]$version_group_details[[2]]$level_learned_at
## [1] 27
## 
## $moves[[16]]$version_group_details[[2]]$move_learn_method
## $moves[[16]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[2]]$version_group
## $moves[[16]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[16]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[16]]$version_group_details[[3]]
## $moves[[16]]$version_group_details[[3]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[3]]$move_learn_method
## $moves[[16]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[3]]$version_group
## $moves[[16]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[16]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[16]]$version_group_details[[4]]
## $moves[[16]]$version_group_details[[4]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[4]]$move_learn_method
## $moves[[16]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[4]]$version_group
## $moves[[16]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[16]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[16]]$version_group_details[[5]]
## $moves[[16]]$version_group_details[[5]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[5]]$move_learn_method
## $moves[[16]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[5]]$version_group
## $moves[[16]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[16]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[16]]$version_group_details[[6]]
## $moves[[16]]$version_group_details[[6]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[6]]$move_learn_method
## $moves[[16]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[6]]$version_group
## $moves[[16]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[16]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[16]]$version_group_details[[7]]
## $moves[[16]]$version_group_details[[7]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[7]]$move_learn_method
## $moves[[16]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[7]]$version_group
## $moves[[16]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[16]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[16]]$version_group_details[[8]]
## $moves[[16]]$version_group_details[[8]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[8]]$move_learn_method
## $moves[[16]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[8]]$version_group
## $moves[[16]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[16]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[16]]$version_group_details[[9]]
## $moves[[16]]$version_group_details[[9]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[9]]$move_learn_method
## $moves[[16]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[9]]$version_group
## $moves[[16]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[16]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[16]]$version_group_details[[10]]
## $moves[[16]]$version_group_details[[10]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[10]]$move_learn_method
## $moves[[16]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[10]]$version_group
## $moves[[16]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[16]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[16]]$version_group_details[[11]]
## $moves[[16]]$version_group_details[[11]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[11]]$move_learn_method
## $moves[[16]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[11]]$version_group
## $moves[[16]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[16]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[16]]$version_group_details[[12]]
## $moves[[16]]$version_group_details[[12]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[12]]$move_learn_method
## $moves[[16]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[12]]$version_group
## $moves[[16]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[16]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[16]]$version_group_details[[13]]
## $moves[[16]]$version_group_details[[13]]$level_learned_at
## [1] 20
## 
## $moves[[16]]$version_group_details[[13]]$move_learn_method
## $moves[[16]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[13]]$version_group
## $moves[[16]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[16]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[16]]$version_group_details[[14]]
## $moves[[16]]$version_group_details[[14]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[14]]$move_learn_method
## $moves[[16]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[14]]$version_group
## $moves[[16]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[16]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[16]]$version_group_details[[15]]
## $moves[[16]]$version_group_details[[15]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[15]]$move_learn_method
## $moves[[16]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[15]]$version_group
## $moves[[16]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[16]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[16]]$version_group_details[[16]]
## $moves[[16]]$version_group_details[[16]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[16]]$move_learn_method
## $moves[[16]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[16]]$version_group
## $moves[[16]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[16]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[16]]$version_group_details[[17]]
## $moves[[16]]$version_group_details[[17]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[17]]$move_learn_method
## $moves[[16]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[17]]$version_group
## $moves[[16]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[16]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[16]]$version_group_details[[18]]
## $moves[[16]]$version_group_details[[18]]$level_learned_at
## [1] 19
## 
## $moves[[16]]$version_group_details[[18]]$move_learn_method
## $moves[[16]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[18]]$version_group
## $moves[[16]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[16]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[16]]$version_group_details[[19]]
## $moves[[16]]$version_group_details[[19]]$level_learned_at
## [1] 23
## 
## $moves[[16]]$version_group_details[[19]]$move_learn_method
## $moves[[16]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[19]]$version_group
## $moves[[16]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[16]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[16]]$version_group_details[[20]]
## $moves[[16]]$version_group_details[[20]]$level_learned_at
## [1] 12
## 
## $moves[[16]]$version_group_details[[20]]$move_learn_method
## $moves[[16]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[16]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[16]]$version_group_details[[20]]$version_group
## $moves[[16]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[16]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[17]]
## $moves[[17]]$move
## $moves[[17]]$move$name
## [1] "solar-beam"
## 
## $moves[[17]]$move$url
## [1] "https://pokeapi.co/api/v2/move/76/"
## 
## 
## $moves[[17]]$version_group_details
## $moves[[17]]$version_group_details[[1]]
## $moves[[17]]$version_group_details[[1]]$level_learned_at
## [1] 48
## 
## $moves[[17]]$version_group_details[[1]]$move_learn_method
## $moves[[17]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[1]]$version_group
## $moves[[17]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[17]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[17]]$version_group_details[[2]]
## $moves[[17]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[2]]$move_learn_method
## $moves[[17]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[2]]$version_group
## $moves[[17]]$version_group_details[[2]]$version_group$name
## [1] "red-blue"
## 
## $moves[[17]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[17]]$version_group_details[[3]]
## $moves[[17]]$version_group_details[[3]]$level_learned_at
## [1] 48
## 
## $moves[[17]]$version_group_details[[3]]$move_learn_method
## $moves[[17]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[3]]$version_group
## $moves[[17]]$version_group_details[[3]]$version_group$name
## [1] "yellow"
## 
## $moves[[17]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[17]]$version_group_details[[4]]
## $moves[[17]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[4]]$move_learn_method
## $moves[[17]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[4]]$version_group
## $moves[[17]]$version_group_details[[4]]$version_group$name
## [1] "yellow"
## 
## $moves[[17]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[17]]$version_group_details[[5]]
## $moves[[17]]$version_group_details[[5]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[5]]$move_learn_method
## $moves[[17]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[5]]$version_group
## $moves[[17]]$version_group_details[[5]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[17]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[17]]$version_group_details[[6]]
## $moves[[17]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[6]]$move_learn_method
## $moves[[17]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[6]]$version_group
## $moves[[17]]$version_group_details[[6]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[17]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[17]]$version_group_details[[7]]
## $moves[[17]]$version_group_details[[7]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[7]]$move_learn_method
## $moves[[17]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[7]]$version_group
## $moves[[17]]$version_group_details[[7]]$version_group$name
## [1] "crystal"
## 
## $moves[[17]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[17]]$version_group_details[[8]]
## $moves[[17]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[8]]$move_learn_method
## $moves[[17]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[8]]$version_group
## $moves[[17]]$version_group_details[[8]]$version_group$name
## [1] "crystal"
## 
## $moves[[17]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[17]]$version_group_details[[9]]
## $moves[[17]]$version_group_details[[9]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[9]]$move_learn_method
## $moves[[17]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[9]]$version_group
## $moves[[17]]$version_group_details[[9]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[17]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[17]]$version_group_details[[10]]
## $moves[[17]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[10]]$move_learn_method
## $moves[[17]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[10]]$version_group
## $moves[[17]]$version_group_details[[10]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[17]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[17]]$version_group_details[[11]]
## $moves[[17]]$version_group_details[[11]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[11]]$move_learn_method
## $moves[[17]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[11]]$version_group
## $moves[[17]]$version_group_details[[11]]$version_group$name
## [1] "emerald"
## 
## $moves[[17]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[17]]$version_group_details[[12]]
## $moves[[17]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[12]]$move_learn_method
## $moves[[17]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[12]]$version_group
## $moves[[17]]$version_group_details[[12]]$version_group$name
## [1] "emerald"
## 
## $moves[[17]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[17]]$version_group_details[[13]]
## $moves[[17]]$version_group_details[[13]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[13]]$move_learn_method
## $moves[[17]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[13]]$version_group
## $moves[[17]]$version_group_details[[13]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[17]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[17]]$version_group_details[[14]]
## $moves[[17]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[14]]$move_learn_method
## $moves[[17]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[14]]$version_group
## $moves[[17]]$version_group_details[[14]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[17]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[17]]$version_group_details[[15]]
## $moves[[17]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[15]]$move_learn_method
## $moves[[17]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[15]]$version_group
## $moves[[17]]$version_group_details[[15]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[17]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[17]]$version_group_details[[16]]
## $moves[[17]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[16]]$move_learn_method
## $moves[[17]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[16]]$version_group
## $moves[[17]]$version_group_details[[16]]$version_group$name
## [1] "platinum"
## 
## $moves[[17]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[17]]$version_group_details[[17]]
## $moves[[17]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[17]]$move_learn_method
## $moves[[17]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[17]]$version_group
## $moves[[17]]$version_group_details[[17]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[17]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[17]]$version_group_details[[18]]
## $moves[[17]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[18]]$move_learn_method
## $moves[[17]]$version_group_details[[18]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[18]]$version_group
## $moves[[17]]$version_group_details[[18]]$version_group$name
## [1] "black-white"
## 
## $moves[[17]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[17]]$version_group_details[[19]]
## $moves[[17]]$version_group_details[[19]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[19]]$move_learn_method
## $moves[[17]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[19]]$version_group
## $moves[[17]]$version_group_details[[19]]$version_group$name
## [1] "colosseum"
## 
## $moves[[17]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[17]]$version_group_details[[20]]
## $moves[[17]]$version_group_details[[20]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[20]]$move_learn_method
## $moves[[17]]$version_group_details[[20]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[20]]$version_group
## $moves[[17]]$version_group_details[[20]]$version_group$name
## [1] "colosseum"
## 
## $moves[[17]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[17]]$version_group_details[[21]]
## $moves[[17]]$version_group_details[[21]]$level_learned_at
## [1] 46
## 
## $moves[[17]]$version_group_details[[21]]$move_learn_method
## $moves[[17]]$version_group_details[[21]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[21]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[21]]$version_group
## $moves[[17]]$version_group_details[[21]]$version_group$name
## [1] "xd"
## 
## $moves[[17]]$version_group_details[[21]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[17]]$version_group_details[[22]]
## $moves[[17]]$version_group_details[[22]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[22]]$move_learn_method
## $moves[[17]]$version_group_details[[22]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[22]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[22]]$version_group
## $moves[[17]]$version_group_details[[22]]$version_group$name
## [1] "xd"
## 
## $moves[[17]]$version_group_details[[22]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[17]]$version_group_details[[23]]
## $moves[[17]]$version_group_details[[23]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[23]]$move_learn_method
## $moves[[17]]$version_group_details[[23]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[23]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[23]]$version_group
## $moves[[17]]$version_group_details[[23]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[17]]$version_group_details[[23]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[17]]$version_group_details[[24]]
## $moves[[17]]$version_group_details[[24]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[24]]$move_learn_method
## $moves[[17]]$version_group_details[[24]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[24]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[24]]$version_group
## $moves[[17]]$version_group_details[[24]]$version_group$name
## [1] "x-y"
## 
## $moves[[17]]$version_group_details[[24]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[17]]$version_group_details[[25]]
## $moves[[17]]$version_group_details[[25]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[25]]$move_learn_method
## $moves[[17]]$version_group_details[[25]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[25]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[25]]$version_group
## $moves[[17]]$version_group_details[[25]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[17]]$version_group_details[[25]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[17]]$version_group_details[[26]]
## $moves[[17]]$version_group_details[[26]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[26]]$move_learn_method
## $moves[[17]]$version_group_details[[26]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[26]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[26]]$version_group
## $moves[[17]]$version_group_details[[26]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[17]]$version_group_details[[26]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[17]]$version_group_details[[27]]
## $moves[[17]]$version_group_details[[27]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[27]]$move_learn_method
## $moves[[17]]$version_group_details[[27]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[27]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[27]]$version_group
## $moves[[17]]$version_group_details[[27]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[17]]$version_group_details[[27]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[17]]$version_group_details[[28]]
## $moves[[17]]$version_group_details[[28]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[28]]$move_learn_method
## $moves[[17]]$version_group_details[[28]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[28]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[28]]$version_group
## $moves[[17]]$version_group_details[[28]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[17]]$version_group_details[[28]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[17]]$version_group_details[[29]]
## $moves[[17]]$version_group_details[[29]]$level_learned_at
## [1] 36
## 
## $moves[[17]]$version_group_details[[29]]$move_learn_method
## $moves[[17]]$version_group_details[[29]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[17]]$version_group_details[[29]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[17]]$version_group_details[[29]]$version_group
## $moves[[17]]$version_group_details[[29]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[17]]$version_group_details[[29]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## $moves[[17]]$version_group_details[[30]]
## $moves[[17]]$version_group_details[[30]]$level_learned_at
## [1] 0
## 
## $moves[[17]]$version_group_details[[30]]$move_learn_method
## $moves[[17]]$version_group_details[[30]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[17]]$version_group_details[[30]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[17]]$version_group_details[[30]]$version_group
## $moves[[17]]$version_group_details[[30]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[17]]$version_group_details[[30]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[18]]
## $moves[[18]]$move
## $moves[[18]]$move$name
## [1] "poison-powder"
## 
## $moves[[18]]$move$url
## [1] "https://pokeapi.co/api/v2/move/77/"
## 
## 
## $moves[[18]]$version_group_details
## $moves[[18]]$version_group_details[[1]]
## $moves[[18]]$version_group_details[[1]]$level_learned_at
## [1] 20
## 
## $moves[[18]]$version_group_details[[1]]$move_learn_method
## $moves[[18]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[1]]$version_group
## $moves[[18]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[18]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[18]]$version_group_details[[2]]
## $moves[[18]]$version_group_details[[2]]$level_learned_at
## [1] 20
## 
## $moves[[18]]$version_group_details[[2]]$move_learn_method
## $moves[[18]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[2]]$version_group
## $moves[[18]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[18]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[18]]$version_group_details[[3]]
## $moves[[18]]$version_group_details[[3]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[3]]$move_learn_method
## $moves[[18]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[3]]$version_group
## $moves[[18]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[18]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[18]]$version_group_details[[4]]
## $moves[[18]]$version_group_details[[4]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[4]]$move_learn_method
## $moves[[18]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[4]]$version_group
## $moves[[18]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[18]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[18]]$version_group_details[[5]]
## $moves[[18]]$version_group_details[[5]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[5]]$move_learn_method
## $moves[[18]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[5]]$version_group
## $moves[[18]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[18]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[18]]$version_group_details[[6]]
## $moves[[18]]$version_group_details[[6]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[6]]$move_learn_method
## $moves[[18]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[6]]$version_group
## $moves[[18]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[18]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[18]]$version_group_details[[7]]
## $moves[[18]]$version_group_details[[7]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[7]]$move_learn_method
## $moves[[18]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[7]]$version_group
## $moves[[18]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[18]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[18]]$version_group_details[[8]]
## $moves[[18]]$version_group_details[[8]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[8]]$move_learn_method
## $moves[[18]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[8]]$version_group
## $moves[[18]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[18]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[18]]$version_group_details[[9]]
## $moves[[18]]$version_group_details[[9]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[9]]$move_learn_method
## $moves[[18]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[9]]$version_group
## $moves[[18]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[18]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[18]]$version_group_details[[10]]
## $moves[[18]]$version_group_details[[10]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[10]]$move_learn_method
## $moves[[18]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[10]]$version_group
## $moves[[18]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[18]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[18]]$version_group_details[[11]]
## $moves[[18]]$version_group_details[[11]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[11]]$move_learn_method
## $moves[[18]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[11]]$version_group
## $moves[[18]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[18]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[18]]$version_group_details[[12]]
## $moves[[18]]$version_group_details[[12]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[12]]$move_learn_method
## $moves[[18]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[12]]$version_group
## $moves[[18]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[18]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[18]]$version_group_details[[13]]
## $moves[[18]]$version_group_details[[13]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[13]]$move_learn_method
## $moves[[18]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[13]]$version_group
## $moves[[18]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[18]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[18]]$version_group_details[[14]]
## $moves[[18]]$version_group_details[[14]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[14]]$move_learn_method
## $moves[[18]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[14]]$version_group
## $moves[[18]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[18]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[18]]$version_group_details[[15]]
## $moves[[18]]$version_group_details[[15]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[15]]$move_learn_method
## $moves[[18]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[15]]$version_group
## $moves[[18]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[18]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[18]]$version_group_details[[16]]
## $moves[[18]]$version_group_details[[16]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[16]]$move_learn_method
## $moves[[18]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[16]]$version_group
## $moves[[18]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[18]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[18]]$version_group_details[[17]]
## $moves[[18]]$version_group_details[[17]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[17]]$move_learn_method
## $moves[[18]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[17]]$version_group
## $moves[[18]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[18]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[18]]$version_group_details[[18]]
## $moves[[18]]$version_group_details[[18]]$level_learned_at
## [1] 13
## 
## $moves[[18]]$version_group_details[[18]]$move_learn_method
## $moves[[18]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[18]]$version_group
## $moves[[18]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[18]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[18]]$version_group_details[[19]]
## $moves[[18]]$version_group_details[[19]]$level_learned_at
## [1] 14
## 
## $moves[[18]]$version_group_details[[19]]$move_learn_method
## $moves[[18]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[19]]$version_group
## $moves[[18]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[18]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[18]]$version_group_details[[20]]
## $moves[[18]]$version_group_details[[20]]$level_learned_at
## [1] 15
## 
## $moves[[18]]$version_group_details[[20]]$move_learn_method
## $moves[[18]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[18]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[18]]$version_group_details[[20]]$version_group
## $moves[[18]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[18]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[19]]
## $moves[[19]]$move
## $moves[[19]]$move$name
## [1] "sleep-powder"
## 
## $moves[[19]]$move$url
## [1] "https://pokeapi.co/api/v2/move/79/"
## 
## 
## $moves[[19]]$version_group_details
## $moves[[19]]$version_group_details[[1]]
## $moves[[19]]$version_group_details[[1]]$level_learned_at
## [1] 41
## 
## $moves[[19]]$version_group_details[[1]]$move_learn_method
## $moves[[19]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[1]]$version_group
## $moves[[19]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[19]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[19]]$version_group_details[[2]]
## $moves[[19]]$version_group_details[[2]]$level_learned_at
## [1] 41
## 
## $moves[[19]]$version_group_details[[2]]$move_learn_method
## $moves[[19]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[2]]$version_group
## $moves[[19]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[19]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[19]]$version_group_details[[3]]
## $moves[[19]]$version_group_details[[3]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[3]]$move_learn_method
## $moves[[19]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[3]]$version_group
## $moves[[19]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[19]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[19]]$version_group_details[[4]]
## $moves[[19]]$version_group_details[[4]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[4]]$move_learn_method
## $moves[[19]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[4]]$version_group
## $moves[[19]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[19]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[19]]$version_group_details[[5]]
## $moves[[19]]$version_group_details[[5]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[5]]$move_learn_method
## $moves[[19]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[5]]$version_group
## $moves[[19]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[19]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[19]]$version_group_details[[6]]
## $moves[[19]]$version_group_details[[6]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[6]]$move_learn_method
## $moves[[19]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[6]]$version_group
## $moves[[19]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[19]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[19]]$version_group_details[[7]]
## $moves[[19]]$version_group_details[[7]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[7]]$move_learn_method
## $moves[[19]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[7]]$version_group
## $moves[[19]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[19]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[19]]$version_group_details[[8]]
## $moves[[19]]$version_group_details[[8]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[8]]$move_learn_method
## $moves[[19]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[8]]$version_group
## $moves[[19]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[19]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[19]]$version_group_details[[9]]
## $moves[[19]]$version_group_details[[9]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[9]]$move_learn_method
## $moves[[19]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[9]]$version_group
## $moves[[19]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[19]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[19]]$version_group_details[[10]]
## $moves[[19]]$version_group_details[[10]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[10]]$move_learn_method
## $moves[[19]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[10]]$version_group
## $moves[[19]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[19]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[19]]$version_group_details[[11]]
## $moves[[19]]$version_group_details[[11]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[11]]$move_learn_method
## $moves[[19]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[11]]$version_group
## $moves[[19]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[19]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[19]]$version_group_details[[12]]
## $moves[[19]]$version_group_details[[12]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[12]]$move_learn_method
## $moves[[19]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[12]]$version_group
## $moves[[19]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[19]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[19]]$version_group_details[[13]]
## $moves[[19]]$version_group_details[[13]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[13]]$move_learn_method
## $moves[[19]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[13]]$version_group
## $moves[[19]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[19]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[19]]$version_group_details[[14]]
## $moves[[19]]$version_group_details[[14]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[14]]$move_learn_method
## $moves[[19]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[14]]$version_group
## $moves[[19]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[19]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[19]]$version_group_details[[15]]
## $moves[[19]]$version_group_details[[15]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[15]]$move_learn_method
## $moves[[19]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[15]]$version_group
## $moves[[19]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[19]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[19]]$version_group_details[[16]]
## $moves[[19]]$version_group_details[[16]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[16]]$move_learn_method
## $moves[[19]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[16]]$version_group
## $moves[[19]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[19]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[19]]$version_group_details[[17]]
## $moves[[19]]$version_group_details[[17]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[17]]$move_learn_method
## $moves[[19]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[17]]$version_group
## $moves[[19]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[19]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[19]]$version_group_details[[18]]
## $moves[[19]]$version_group_details[[18]]$level_learned_at
## [1] 13
## 
## $moves[[19]]$version_group_details[[18]]$move_learn_method
## $moves[[19]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[18]]$version_group
## $moves[[19]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[19]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[19]]$version_group_details[[19]]
## $moves[[19]]$version_group_details[[19]]$level_learned_at
## [1] 14
## 
## $moves[[19]]$version_group_details[[19]]$move_learn_method
## $moves[[19]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[19]]$version_group
## $moves[[19]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[19]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[19]]$version_group_details[[20]]
## $moves[[19]]$version_group_details[[20]]$level_learned_at
## [1] 15
## 
## $moves[[19]]$version_group_details[[20]]$move_learn_method
## $moves[[19]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[19]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[19]]$version_group_details[[20]]$version_group
## $moves[[19]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[19]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[20]]
## $moves[[20]]$move
## $moves[[20]]$move$name
## [1] "petal-dance"
## 
## $moves[[20]]$move$url
## [1] "https://pokeapi.co/api/v2/move/80/"
## 
## 
## $moves[[20]]$version_group_details
## $moves[[20]]$version_group_details[[1]]
## $moves[[20]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[1]]$move_learn_method
## $moves[[20]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[1]]$version_group
## $moves[[20]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[20]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[20]]$version_group_details[[2]]
## $moves[[20]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[2]]$move_learn_method
## $moves[[20]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[2]]$version_group
## $moves[[20]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[20]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[20]]$version_group_details[[3]]
## $moves[[20]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[3]]$move_learn_method
## $moves[[20]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[3]]$version_group
## $moves[[20]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[20]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[20]]$version_group_details[[4]]
## $moves[[20]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[4]]$move_learn_method
## $moves[[20]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[4]]$version_group
## $moves[[20]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[20]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[20]]$version_group_details[[5]]
## $moves[[20]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[5]]$move_learn_method
## $moves[[20]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[5]]$version_group
## $moves[[20]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[20]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[20]]$version_group_details[[6]]
## $moves[[20]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[6]]$move_learn_method
## $moves[[20]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[6]]$version_group
## $moves[[20]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[20]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[20]]$version_group_details[[7]]
## $moves[[20]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[7]]$move_learn_method
## $moves[[20]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[7]]$version_group
## $moves[[20]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[20]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[20]]$version_group_details[[8]]
## $moves[[20]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[8]]$move_learn_method
## $moves[[20]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[8]]$version_group
## $moves[[20]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[20]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[20]]$version_group_details[[9]]
## $moves[[20]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[9]]$move_learn_method
## $moves[[20]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[9]]$version_group
## $moves[[20]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[20]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[20]]$version_group_details[[10]]
## $moves[[20]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[10]]$move_learn_method
## $moves[[20]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[10]]$version_group
## $moves[[20]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[20]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[20]]$version_group_details[[11]]
## $moves[[20]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[11]]$move_learn_method
## $moves[[20]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[11]]$version_group
## $moves[[20]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[20]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[20]]$version_group_details[[12]]
## $moves[[20]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[12]]$move_learn_method
## $moves[[20]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[12]]$version_group
## $moves[[20]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[20]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[20]]$version_group_details[[13]]
## $moves[[20]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[13]]$move_learn_method
## $moves[[20]]$version_group_details[[13]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[13]]$version_group
## $moves[[20]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[20]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[20]]$version_group_details[[14]]
## $moves[[20]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[14]]$move_learn_method
## $moves[[20]]$version_group_details[[14]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[14]]$version_group
## $moves[[20]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[20]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[20]]$version_group_details[[15]]
## $moves[[20]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[20]]$version_group_details[[15]]$move_learn_method
## $moves[[20]]$version_group_details[[15]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[20]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[20]]$version_group_details[[15]]$version_group
## $moves[[20]]$version_group_details[[15]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[20]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[21]]
## $moves[[21]]$move
## $moves[[21]]$move$name
## [1] "string-shot"
## 
## $moves[[21]]$move$url
## [1] "https://pokeapi.co/api/v2/move/81/"
## 
## 
## $moves[[21]]$version_group_details
## $moves[[21]]$version_group_details[[1]]
## $moves[[21]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[21]]$version_group_details[[1]]$move_learn_method
## $moves[[21]]$version_group_details[[1]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[21]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[21]]$version_group_details[[1]]$version_group
## $moves[[21]]$version_group_details[[1]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[21]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## 
## 
## $moves[[22]]
## $moves[[22]]$move
## $moves[[22]]$move$name
## [1] "toxic"
## 
## $moves[[22]]$move$url
## [1] "https://pokeapi.co/api/v2/move/92/"
## 
## 
## $moves[[22]]$version_group_details
## $moves[[22]]$version_group_details[[1]]
## $moves[[22]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[1]]$move_learn_method
## $moves[[22]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[1]]$version_group
## $moves[[22]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[22]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[22]]$version_group_details[[2]]
## $moves[[22]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[2]]$move_learn_method
## $moves[[22]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[2]]$version_group
## $moves[[22]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[22]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[22]]$version_group_details[[3]]
## $moves[[22]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[3]]$move_learn_method
## $moves[[22]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[3]]$version_group
## $moves[[22]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[22]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[22]]$version_group_details[[4]]
## $moves[[22]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[4]]$move_learn_method
## $moves[[22]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[4]]$version_group
## $moves[[22]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[22]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[22]]$version_group_details[[5]]
## $moves[[22]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[5]]$move_learn_method
## $moves[[22]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[5]]$version_group
## $moves[[22]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[22]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[22]]$version_group_details[[6]]
## $moves[[22]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[6]]$move_learn_method
## $moves[[22]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[6]]$version_group
## $moves[[22]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[22]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[22]]$version_group_details[[7]]
## $moves[[22]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[7]]$move_learn_method
## $moves[[22]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[7]]$version_group
## $moves[[22]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[22]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[22]]$version_group_details[[8]]
## $moves[[22]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[8]]$move_learn_method
## $moves[[22]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[8]]$version_group
## $moves[[22]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[22]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[22]]$version_group_details[[9]]
## $moves[[22]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[9]]$move_learn_method
## $moves[[22]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[9]]$version_group
## $moves[[22]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[22]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[22]]$version_group_details[[10]]
## $moves[[22]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[10]]$move_learn_method
## $moves[[22]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[10]]$version_group
## $moves[[22]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[22]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[22]]$version_group_details[[11]]
## $moves[[22]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[11]]$move_learn_method
## $moves[[22]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[11]]$version_group
## $moves[[22]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[22]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[22]]$version_group_details[[12]]
## $moves[[22]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[12]]$move_learn_method
## $moves[[22]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[12]]$version_group
## $moves[[22]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[22]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[22]]$version_group_details[[13]]
## $moves[[22]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[13]]$move_learn_method
## $moves[[22]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[13]]$version_group
## $moves[[22]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[22]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[22]]$version_group_details[[14]]
## $moves[[22]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[14]]$move_learn_method
## $moves[[22]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[14]]$version_group
## $moves[[22]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[22]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[22]]$version_group_details[[15]]
## $moves[[22]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[15]]$move_learn_method
## $moves[[22]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[15]]$version_group
## $moves[[22]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[22]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[22]]$version_group_details[[16]]
## $moves[[22]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[16]]$move_learn_method
## $moves[[22]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[16]]$version_group
## $moves[[22]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[22]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[22]]$version_group_details[[17]]
## $moves[[22]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[17]]$move_learn_method
## $moves[[22]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[17]]$version_group
## $moves[[22]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[22]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[22]]$version_group_details[[18]]
## $moves[[22]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[18]]$move_learn_method
## $moves[[22]]$version_group_details[[18]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[18]]$version_group
## $moves[[22]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[22]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[22]]$version_group_details[[19]]
## $moves[[22]]$version_group_details[[19]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[19]]$move_learn_method
## $moves[[22]]$version_group_details[[19]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[22]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[22]]$version_group_details[[19]]$version_group
## $moves[[22]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[22]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[22]]$version_group_details[[20]]
## $moves[[22]]$version_group_details[[20]]$level_learned_at
## [1] 0
## 
## $moves[[22]]$version_group_details[[20]]$move_learn_method
## $moves[[22]]$version_group_details[[20]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[22]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[22]]$version_group_details[[20]]$version_group
## $moves[[22]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[22]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[23]]
## $moves[[23]]$move
## $moves[[23]]$move$name
## [1] "rage"
## 
## $moves[[23]]$move$url
## [1] "https://pokeapi.co/api/v2/move/99/"
## 
## 
## $moves[[23]]$version_group_details
## $moves[[23]]$version_group_details[[1]]
## $moves[[23]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[23]]$version_group_details[[1]]$move_learn_method
## $moves[[23]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[23]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[23]]$version_group_details[[1]]$version_group
## $moves[[23]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[23]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[23]]$version_group_details[[2]]
## $moves[[23]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[23]]$version_group_details[[2]]$move_learn_method
## $moves[[23]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[23]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[23]]$version_group_details[[2]]$version_group
## $moves[[23]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[23]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## 
## 
## $moves[[24]]
## $moves[[24]]$move
## $moves[[24]]$move$name
## [1] "mimic"
## 
## $moves[[24]]$move$url
## [1] "https://pokeapi.co/api/v2/move/102/"
## 
## 
## $moves[[24]]$version_group_details
## $moves[[24]]$version_group_details[[1]]
## $moves[[24]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[24]]$version_group_details[[1]]$move_learn_method
## $moves[[24]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[24]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[24]]$version_group_details[[1]]$version_group
## $moves[[24]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[24]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[24]]$version_group_details[[2]]
## $moves[[24]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[24]]$version_group_details[[2]]$move_learn_method
## $moves[[24]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[24]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[24]]$version_group_details[[2]]$version_group
## $moves[[24]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[24]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[24]]$version_group_details[[3]]
## $moves[[24]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[24]]$version_group_details[[3]]$move_learn_method
## $moves[[24]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[24]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[24]]$version_group_details[[3]]$version_group
## $moves[[24]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[24]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[24]]$version_group_details[[4]]
## $moves[[24]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[24]]$version_group_details[[4]]$move_learn_method
## $moves[[24]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[24]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[24]]$version_group_details[[4]]$version_group
## $moves[[24]]$version_group_details[[4]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[24]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[24]]$version_group_details[[5]]
## $moves[[24]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[24]]$version_group_details[[5]]$move_learn_method
## $moves[[24]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[24]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[24]]$version_group_details[[5]]$version_group
## $moves[[24]]$version_group_details[[5]]$version_group$name
## [1] "xd"
## 
## $moves[[24]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## 
## 
## $moves[[25]]
## $moves[[25]]$move
## $moves[[25]]$move$name
## [1] "double-team"
## 
## $moves[[25]]$move$url
## [1] "https://pokeapi.co/api/v2/move/104/"
## 
## 
## $moves[[25]]$version_group_details
## $moves[[25]]$version_group_details[[1]]
## $moves[[25]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[1]]$move_learn_method
## $moves[[25]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[1]]$version_group
## $moves[[25]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[25]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[25]]$version_group_details[[2]]
## $moves[[25]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[2]]$move_learn_method
## $moves[[25]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[2]]$version_group
## $moves[[25]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[25]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[25]]$version_group_details[[3]]
## $moves[[25]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[3]]$move_learn_method
## $moves[[25]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[3]]$version_group
## $moves[[25]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[25]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[25]]$version_group_details[[4]]
## $moves[[25]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[4]]$move_learn_method
## $moves[[25]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[4]]$version_group
## $moves[[25]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[25]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[25]]$version_group_details[[5]]
## $moves[[25]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[5]]$move_learn_method
## $moves[[25]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[5]]$version_group
## $moves[[25]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[25]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[25]]$version_group_details[[6]]
## $moves[[25]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[6]]$move_learn_method
## $moves[[25]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[6]]$version_group
## $moves[[25]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[25]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[25]]$version_group_details[[7]]
## $moves[[25]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[7]]$move_learn_method
## $moves[[25]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[7]]$version_group
## $moves[[25]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[25]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[25]]$version_group_details[[8]]
## $moves[[25]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[8]]$move_learn_method
## $moves[[25]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[8]]$version_group
## $moves[[25]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[25]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[25]]$version_group_details[[9]]
## $moves[[25]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[9]]$move_learn_method
## $moves[[25]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[9]]$version_group
## $moves[[25]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[25]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[25]]$version_group_details[[10]]
## $moves[[25]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[10]]$move_learn_method
## $moves[[25]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[10]]$version_group
## $moves[[25]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[25]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[25]]$version_group_details[[11]]
## $moves[[25]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[11]]$move_learn_method
## $moves[[25]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[11]]$version_group
## $moves[[25]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[25]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[25]]$version_group_details[[12]]
## $moves[[25]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[12]]$move_learn_method
## $moves[[25]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[12]]$version_group
## $moves[[25]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[25]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[25]]$version_group_details[[13]]
## $moves[[25]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[13]]$move_learn_method
## $moves[[25]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[13]]$version_group
## $moves[[25]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[25]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[25]]$version_group_details[[14]]
## $moves[[25]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[14]]$move_learn_method
## $moves[[25]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[14]]$version_group
## $moves[[25]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[25]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[25]]$version_group_details[[15]]
## $moves[[25]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[15]]$move_learn_method
## $moves[[25]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[15]]$version_group
## $moves[[25]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[25]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[25]]$version_group_details[[16]]
## $moves[[25]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[16]]$move_learn_method
## $moves[[25]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[16]]$version_group
## $moves[[25]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[25]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[25]]$version_group_details[[17]]
## $moves[[25]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[17]]$move_learn_method
## $moves[[25]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[17]]$version_group
## $moves[[25]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[25]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[25]]$version_group_details[[18]]
## $moves[[25]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[25]]$version_group_details[[18]]$move_learn_method
## $moves[[25]]$version_group_details[[18]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[25]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[25]]$version_group_details[[18]]$version_group
## $moves[[25]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[25]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[26]]
## $moves[[26]]$move
## $moves[[26]]$move$name
## [1] "defense-curl"
## 
## $moves[[26]]$move$url
## [1] "https://pokeapi.co/api/v2/move/111/"
## 
## 
## $moves[[26]]$version_group_details
## $moves[[26]]$version_group_details[[1]]
## $moves[[26]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[26]]$version_group_details[[1]]$move_learn_method
## $moves[[26]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[26]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[26]]$version_group_details[[1]]$version_group
## $moves[[26]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[26]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[26]]$version_group_details[[2]]
## $moves[[26]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[26]]$version_group_details[[2]]$move_learn_method
## $moves[[26]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[26]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[26]]$version_group_details[[2]]$version_group
## $moves[[26]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[26]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[26]]$version_group_details[[3]]
## $moves[[26]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[26]]$version_group_details[[3]]$move_learn_method
## $moves[[26]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[26]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[26]]$version_group_details[[3]]$version_group
## $moves[[26]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[26]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## 
## 
## $moves[[27]]
## $moves[[27]]$move
## $moves[[27]]$move$name
## [1] "light-screen"
## 
## $moves[[27]]$move$url
## [1] "https://pokeapi.co/api/v2/move/113/"
## 
## 
## $moves[[27]]$version_group_details
## $moves[[27]]$version_group_details[[1]]
## $moves[[27]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[1]]$move_learn_method
## $moves[[27]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[1]]$version_group
## $moves[[27]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[27]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[27]]$version_group_details[[2]]
## $moves[[27]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[2]]$move_learn_method
## $moves[[27]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[2]]$version_group
## $moves[[27]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[27]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[27]]$version_group_details[[3]]
## $moves[[27]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[3]]$move_learn_method
## $moves[[27]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[3]]$version_group
## $moves[[27]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[27]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[27]]$version_group_details[[4]]
## $moves[[27]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[4]]$move_learn_method
## $moves[[27]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[4]]$version_group
## $moves[[27]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[27]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[27]]$version_group_details[[5]]
## $moves[[27]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[5]]$move_learn_method
## $moves[[27]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[5]]$version_group
## $moves[[27]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[27]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[27]]$version_group_details[[6]]
## $moves[[27]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[6]]$move_learn_method
## $moves[[27]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[6]]$version_group
## $moves[[27]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[27]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[27]]$version_group_details[[7]]
## $moves[[27]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[7]]$move_learn_method
## $moves[[27]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[7]]$version_group
## $moves[[27]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[27]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[27]]$version_group_details[[8]]
## $moves[[27]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[8]]$move_learn_method
## $moves[[27]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[27]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[27]]$version_group_details[[8]]$version_group
## $moves[[27]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[27]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[27]]$version_group_details[[9]]
## $moves[[27]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[9]]$move_learn_method
## $moves[[27]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[9]]$version_group
## $moves[[27]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[27]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[27]]$version_group_details[[10]]
## $moves[[27]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[10]]$move_learn_method
## $moves[[27]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[10]]$version_group
## $moves[[27]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[27]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[27]]$version_group_details[[11]]
## $moves[[27]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[11]]$move_learn_method
## $moves[[27]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[11]]$version_group
## $moves[[27]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[27]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[27]]$version_group_details[[12]]
## $moves[[27]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[12]]$move_learn_method
## $moves[[27]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[12]]$version_group
## $moves[[27]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[27]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[27]]$version_group_details[[13]]
## $moves[[27]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[13]]$move_learn_method
## $moves[[27]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[13]]$version_group
## $moves[[27]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[27]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[27]]$version_group_details[[14]]
## $moves[[27]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[14]]$move_learn_method
## $moves[[27]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[14]]$version_group
## $moves[[27]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[27]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[27]]$version_group_details[[15]]
## $moves[[27]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[15]]$move_learn_method
## $moves[[27]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[15]]$version_group
## $moves[[27]]$version_group_details[[15]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[27]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[27]]$version_group_details[[16]]
## $moves[[27]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[27]]$version_group_details[[16]]$move_learn_method
## $moves[[27]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[27]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[27]]$version_group_details[[16]]$version_group
## $moves[[27]]$version_group_details[[16]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[27]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[28]]
## $moves[[28]]$move
## $moves[[28]]$move$name
## [1] "reflect"
## 
## $moves[[28]]$move$url
## [1] "https://pokeapi.co/api/v2/move/115/"
## 
## 
## $moves[[28]]$version_group_details
## $moves[[28]]$version_group_details[[1]]
## $moves[[28]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[28]]$version_group_details[[1]]$move_learn_method
## $moves[[28]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[28]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[28]]$version_group_details[[1]]$version_group
## $moves[[28]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[28]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[28]]$version_group_details[[2]]
## $moves[[28]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[28]]$version_group_details[[2]]$move_learn_method
## $moves[[28]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[28]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[28]]$version_group_details[[2]]$version_group
## $moves[[28]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[28]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[28]]$version_group_details[[3]]
## $moves[[28]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[28]]$version_group_details[[3]]$move_learn_method
## $moves[[28]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[28]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[28]]$version_group_details[[3]]$version_group
## $moves[[28]]$version_group_details[[3]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[28]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## 
## 
## $moves[[29]]
## $moves[[29]]$move
## $moves[[29]]$move$name
## [1] "bide"
## 
## $moves[[29]]$move$url
## [1] "https://pokeapi.co/api/v2/move/117/"
## 
## 
## $moves[[29]]$version_group_details
## $moves[[29]]$version_group_details[[1]]
## $moves[[29]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[29]]$version_group_details[[1]]$move_learn_method
## $moves[[29]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[29]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[29]]$version_group_details[[1]]$version_group
## $moves[[29]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[29]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[29]]$version_group_details[[2]]
## $moves[[29]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[29]]$version_group_details[[2]]$move_learn_method
## $moves[[29]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[29]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[29]]$version_group_details[[2]]$version_group
## $moves[[29]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[29]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## 
## 
## $moves[[30]]
## $moves[[30]]$move
## $moves[[30]]$move$name
## [1] "sludge"
## 
## $moves[[30]]$move$url
## [1] "https://pokeapi.co/api/v2/move/124/"
## 
## 
## $moves[[30]]$version_group_details
## $moves[[30]]$version_group_details[[1]]
## $moves[[30]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[1]]$move_learn_method
## $moves[[30]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[1]]$version_group
## $moves[[30]]$version_group_details[[1]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[30]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[30]]$version_group_details[[2]]
## $moves[[30]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[2]]$move_learn_method
## $moves[[30]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[2]]$version_group
## $moves[[30]]$version_group_details[[2]]$version_group$name
## [1] "black-white"
## 
## $moves[[30]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[30]]$version_group_details[[3]]
## $moves[[30]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[3]]$move_learn_method
## $moves[[30]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[3]]$version_group
## $moves[[30]]$version_group_details[[3]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[30]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[30]]$version_group_details[[4]]
## $moves[[30]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[4]]$move_learn_method
## $moves[[30]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[4]]$version_group
## $moves[[30]]$version_group_details[[4]]$version_group$name
## [1] "x-y"
## 
## $moves[[30]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[30]]$version_group_details[[5]]
## $moves[[30]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[5]]$move_learn_method
## $moves[[30]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[5]]$version_group
## $moves[[30]]$version_group_details[[5]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[30]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[30]]$version_group_details[[6]]
## $moves[[30]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[6]]$move_learn_method
## $moves[[30]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[6]]$version_group
## $moves[[30]]$version_group_details[[6]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[30]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[30]]$version_group_details[[7]]
## $moves[[30]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[30]]$version_group_details[[7]]$move_learn_method
## $moves[[30]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[30]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[30]]$version_group_details[[7]]$version_group
## $moves[[30]]$version_group_details[[7]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[30]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[31]]
## $moves[[31]]$move
## $moves[[31]]$move$name
## [1] "skull-bash"
## 
## $moves[[31]]$move$url
## [1] "https://pokeapi.co/api/v2/move/130/"
## 
## 
## $moves[[31]]$version_group_details
## $moves[[31]]$version_group_details[[1]]
## $moves[[31]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[1]]$move_learn_method
## $moves[[31]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[1]]$version_group
## $moves[[31]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[31]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[31]]$version_group_details[[2]]
## $moves[[31]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[2]]$move_learn_method
## $moves[[31]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[2]]$version_group
## $moves[[31]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[31]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[31]]$version_group_details[[3]]
## $moves[[31]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[3]]$move_learn_method
## $moves[[31]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[3]]$version_group
## $moves[[31]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[31]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[31]]$version_group_details[[4]]
## $moves[[31]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[4]]$move_learn_method
## $moves[[31]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[4]]$version_group
## $moves[[31]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[31]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[31]]$version_group_details[[5]]
## $moves[[31]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[5]]$move_learn_method
## $moves[[31]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[5]]$version_group
## $moves[[31]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[31]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[31]]$version_group_details[[6]]
## $moves[[31]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[6]]$move_learn_method
## $moves[[31]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[6]]$version_group
## $moves[[31]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[31]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[31]]$version_group_details[[7]]
## $moves[[31]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[7]]$move_learn_method
## $moves[[31]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[7]]$version_group
## $moves[[31]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[31]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[31]]$version_group_details[[8]]
## $moves[[31]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[8]]$move_learn_method
## $moves[[31]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[8]]$version_group
## $moves[[31]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[31]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[31]]$version_group_details[[9]]
## $moves[[31]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[9]]$move_learn_method
## $moves[[31]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[9]]$version_group
## $moves[[31]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[31]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[31]]$version_group_details[[10]]
## $moves[[31]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[10]]$move_learn_method
## $moves[[31]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[10]]$version_group
## $moves[[31]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[31]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[31]]$version_group_details[[11]]
## $moves[[31]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[11]]$move_learn_method
## $moves[[31]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[11]]$version_group
## $moves[[31]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[31]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[31]]$version_group_details[[12]]
## $moves[[31]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[12]]$move_learn_method
## $moves[[31]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[12]]$version_group
## $moves[[31]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[31]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[31]]$version_group_details[[13]]
## $moves[[31]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[13]]$move_learn_method
## $moves[[31]]$version_group_details[[13]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[13]]$version_group
## $moves[[31]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[31]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[31]]$version_group_details[[14]]
## $moves[[31]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[14]]$move_learn_method
## $moves[[31]]$version_group_details[[14]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[14]]$version_group
## $moves[[31]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[31]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[31]]$version_group_details[[15]]
## $moves[[31]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[31]]$version_group_details[[15]]$move_learn_method
## $moves[[31]]$version_group_details[[15]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[31]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[31]]$version_group_details[[15]]$version_group
## $moves[[31]]$version_group_details[[15]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[31]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[32]]
## $moves[[32]]$move
## $moves[[32]]$move$name
## [1] "amnesia"
## 
## $moves[[32]]$move$url
## [1] "https://pokeapi.co/api/v2/move/133/"
## 
## 
## $moves[[32]]$version_group_details
## $moves[[32]]$version_group_details[[1]]
## $moves[[32]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[1]]$move_learn_method
## $moves[[32]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[1]]$version_group
## $moves[[32]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[32]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[32]]$version_group_details[[2]]
## $moves[[32]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[2]]$move_learn_method
## $moves[[32]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[2]]$version_group
## $moves[[32]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[32]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[32]]$version_group_details[[3]]
## $moves[[32]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[3]]$move_learn_method
## $moves[[32]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[3]]$version_group
## $moves[[32]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[32]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[32]]$version_group_details[[4]]
## $moves[[32]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[4]]$move_learn_method
## $moves[[32]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[4]]$version_group
## $moves[[32]]$version_group_details[[4]]$version_group$name
## [1] "black-white"
## 
## $moves[[32]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[32]]$version_group_details[[5]]
## $moves[[32]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[5]]$move_learn_method
## $moves[[32]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[5]]$version_group
## $moves[[32]]$version_group_details[[5]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[32]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[32]]$version_group_details[[6]]
## $moves[[32]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[6]]$move_learn_method
## $moves[[32]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[6]]$version_group
## $moves[[32]]$version_group_details[[6]]$version_group$name
## [1] "x-y"
## 
## $moves[[32]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[32]]$version_group_details[[7]]
## $moves[[32]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[7]]$move_learn_method
## $moves[[32]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[7]]$version_group
## $moves[[32]]$version_group_details[[7]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[32]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[32]]$version_group_details[[8]]
## $moves[[32]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[8]]$move_learn_method
## $moves[[32]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[8]]$version_group
## $moves[[32]]$version_group_details[[8]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[32]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[32]]$version_group_details[[9]]
## $moves[[32]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[9]]$move_learn_method
## $moves[[32]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[32]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[32]]$version_group_details[[9]]$version_group
## $moves[[32]]$version_group_details[[9]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[32]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[32]]$version_group_details[[10]]
## $moves[[32]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[32]]$version_group_details[[10]]$move_learn_method
## $moves[[32]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[32]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[32]]$version_group_details[[10]]$version_group
## $moves[[32]]$version_group_details[[10]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[32]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[33]]
## $moves[[33]]$move
## $moves[[33]]$move$name
## [1] "flash"
## 
## $moves[[33]]$move$url
## [1] "https://pokeapi.co/api/v2/move/148/"
## 
## 
## $moves[[33]]$version_group_details
## $moves[[33]]$version_group_details[[1]]
## $moves[[33]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[1]]$move_learn_method
## $moves[[33]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[1]]$version_group
## $moves[[33]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[33]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[33]]$version_group_details[[2]]
## $moves[[33]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[2]]$move_learn_method
## $moves[[33]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[2]]$version_group
## $moves[[33]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[33]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[33]]$version_group_details[[3]]
## $moves[[33]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[3]]$move_learn_method
## $moves[[33]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[3]]$version_group
## $moves[[33]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[33]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[33]]$version_group_details[[4]]
## $moves[[33]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[4]]$move_learn_method
## $moves[[33]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[4]]$version_group
## $moves[[33]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[33]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[33]]$version_group_details[[5]]
## $moves[[33]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[5]]$move_learn_method
## $moves[[33]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[5]]$version_group
## $moves[[33]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[33]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[33]]$version_group_details[[6]]
## $moves[[33]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[6]]$move_learn_method
## $moves[[33]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[6]]$version_group
## $moves[[33]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[33]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[33]]$version_group_details[[7]]
## $moves[[33]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[7]]$move_learn_method
## $moves[[33]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[7]]$version_group
## $moves[[33]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[33]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[33]]$version_group_details[[8]]
## $moves[[33]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[8]]$move_learn_method
## $moves[[33]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[8]]$version_group
## $moves[[33]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[33]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[33]]$version_group_details[[9]]
## $moves[[33]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[9]]$move_learn_method
## $moves[[33]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[9]]$version_group
## $moves[[33]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[33]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[33]]$version_group_details[[10]]
## $moves[[33]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[10]]$move_learn_method
## $moves[[33]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[10]]$version_group
## $moves[[33]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[33]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[33]]$version_group_details[[11]]
## $moves[[33]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[11]]$move_learn_method
## $moves[[33]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[11]]$version_group
## $moves[[33]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[33]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[33]]$version_group_details[[12]]
## $moves[[33]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[12]]$move_learn_method
## $moves[[33]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[12]]$version_group
## $moves[[33]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[33]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[33]]$version_group_details[[13]]
## $moves[[33]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[13]]$move_learn_method
## $moves[[33]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[13]]$version_group
## $moves[[33]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[33]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[33]]$version_group_details[[14]]
## $moves[[33]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[33]]$version_group_details[[14]]$move_learn_method
## $moves[[33]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[33]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[33]]$version_group_details[[14]]$version_group
## $moves[[33]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[33]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## 
## 
## $moves[[34]]
## $moves[[34]]$move
## $moves[[34]]$move$name
## [1] "rest"
## 
## $moves[[34]]$move$url
## [1] "https://pokeapi.co/api/v2/move/156/"
## 
## 
## $moves[[34]]$version_group_details
## $moves[[34]]$version_group_details[[1]]
## $moves[[34]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[1]]$move_learn_method
## $moves[[34]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[1]]$version_group
## $moves[[34]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[34]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[34]]$version_group_details[[2]]
## $moves[[34]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[2]]$move_learn_method
## $moves[[34]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[2]]$version_group
## $moves[[34]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[34]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[34]]$version_group_details[[3]]
## $moves[[34]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[3]]$move_learn_method
## $moves[[34]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[3]]$version_group
## $moves[[34]]$version_group_details[[3]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[34]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[34]]$version_group_details[[4]]
## $moves[[34]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[4]]$move_learn_method
## $moves[[34]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[4]]$version_group
## $moves[[34]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[34]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[34]]$version_group_details[[5]]
## $moves[[34]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[5]]$move_learn_method
## $moves[[34]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[5]]$version_group
## $moves[[34]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[34]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[34]]$version_group_details[[6]]
## $moves[[34]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[6]]$move_learn_method
## $moves[[34]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[6]]$version_group
## $moves[[34]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[34]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[34]]$version_group_details[[7]]
## $moves[[34]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[7]]$move_learn_method
## $moves[[34]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[7]]$version_group
## $moves[[34]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[34]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[34]]$version_group_details[[8]]
## $moves[[34]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[8]]$move_learn_method
## $moves[[34]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[8]]$version_group
## $moves[[34]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[34]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[34]]$version_group_details[[9]]
## $moves[[34]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[9]]$move_learn_method
## $moves[[34]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[9]]$version_group
## $moves[[34]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[34]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[34]]$version_group_details[[10]]
## $moves[[34]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[10]]$move_learn_method
## $moves[[34]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[10]]$version_group
## $moves[[34]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[34]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[34]]$version_group_details[[11]]
## $moves[[34]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[11]]$move_learn_method
## $moves[[34]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[11]]$version_group
## $moves[[34]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[34]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[34]]$version_group_details[[12]]
## $moves[[34]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[12]]$move_learn_method
## $moves[[34]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[12]]$version_group
## $moves[[34]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[34]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[34]]$version_group_details[[13]]
## $moves[[34]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[13]]$move_learn_method
## $moves[[34]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[13]]$version_group
## $moves[[34]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[34]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[34]]$version_group_details[[14]]
## $moves[[34]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[14]]$move_learn_method
## $moves[[34]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[14]]$version_group
## $moves[[34]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[34]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[34]]$version_group_details[[15]]
## $moves[[34]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[15]]$move_learn_method
## $moves[[34]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[15]]$version_group
## $moves[[34]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[34]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[34]]$version_group_details[[16]]
## $moves[[34]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[16]]$move_learn_method
## $moves[[34]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[16]]$version_group
## $moves[[34]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[34]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[34]]$version_group_details[[17]]
## $moves[[34]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[17]]$move_learn_method
## $moves[[34]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[17]]$version_group
## $moves[[34]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[34]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[34]]$version_group_details[[18]]
## $moves[[34]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[18]]$move_learn_method
## $moves[[34]]$version_group_details[[18]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[18]]$version_group
## $moves[[34]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[34]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[34]]$version_group_details[[19]]
## $moves[[34]]$version_group_details[[19]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[19]]$move_learn_method
## $moves[[34]]$version_group_details[[19]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[19]]$version_group
## $moves[[34]]$version_group_details[[19]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[34]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[34]]$version_group_details[[20]]
## $moves[[34]]$version_group_details[[20]]$level_learned_at
## [1] 0
## 
## $moves[[34]]$version_group_details[[20]]$move_learn_method
## $moves[[34]]$version_group_details[[20]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[34]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[34]]$version_group_details[[20]]$version_group
## $moves[[34]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[34]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[35]]
## $moves[[35]]$move
## $moves[[35]]$move$name
## [1] "substitute"
## 
## $moves[[35]]$move$url
## [1] "https://pokeapi.co/api/v2/move/164/"
## 
## 
## $moves[[35]]$version_group_details
## $moves[[35]]$version_group_details[[1]]
## $moves[[35]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[1]]$move_learn_method
## $moves[[35]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[1]]$version_group
## $moves[[35]]$version_group_details[[1]]$version_group$name
## [1] "red-blue"
## 
## $moves[[35]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/1/"
## 
## 
## 
## $moves[[35]]$version_group_details[[2]]
## $moves[[35]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[2]]$move_learn_method
## $moves[[35]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[2]]$version_group
## $moves[[35]]$version_group_details[[2]]$version_group$name
## [1] "yellow"
## 
## $moves[[35]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/2/"
## 
## 
## 
## $moves[[35]]$version_group_details[[3]]
## $moves[[35]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[3]]$move_learn_method
## $moves[[35]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[35]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[35]]$version_group_details[[3]]$version_group
## $moves[[35]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[35]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[35]]$version_group_details[[4]]
## $moves[[35]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[4]]$move_learn_method
## $moves[[35]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[35]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[35]]$version_group_details[[4]]$version_group
## $moves[[35]]$version_group_details[[4]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[35]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[35]]$version_group_details[[5]]
## $moves[[35]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[5]]$move_learn_method
## $moves[[35]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[5]]$version_group
## $moves[[35]]$version_group_details[[5]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[35]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[35]]$version_group_details[[6]]
## $moves[[35]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[6]]$move_learn_method
## $moves[[35]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[6]]$version_group
## $moves[[35]]$version_group_details[[6]]$version_group$name
## [1] "platinum"
## 
## $moves[[35]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[35]]$version_group_details[[7]]
## $moves[[35]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[7]]$move_learn_method
## $moves[[35]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[7]]$version_group
## $moves[[35]]$version_group_details[[7]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[35]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[35]]$version_group_details[[8]]
## $moves[[35]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[8]]$move_learn_method
## $moves[[35]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[8]]$version_group
## $moves[[35]]$version_group_details[[8]]$version_group$name
## [1] "black-white"
## 
## $moves[[35]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[35]]$version_group_details[[9]]
## $moves[[35]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[9]]$move_learn_method
## $moves[[35]]$version_group_details[[9]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[35]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[35]]$version_group_details[[9]]$version_group
## $moves[[35]]$version_group_details[[9]]$version_group$name
## [1] "xd"
## 
## $moves[[35]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[35]]$version_group_details[[10]]
## $moves[[35]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[10]]$move_learn_method
## $moves[[35]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[10]]$version_group
## $moves[[35]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[35]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[35]]$version_group_details[[11]]
## $moves[[35]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[11]]$move_learn_method
## $moves[[35]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[11]]$version_group
## $moves[[35]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[35]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[35]]$version_group_details[[12]]
## $moves[[35]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[12]]$move_learn_method
## $moves[[35]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[12]]$version_group
## $moves[[35]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[35]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[35]]$version_group_details[[13]]
## $moves[[35]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[13]]$move_learn_method
## $moves[[35]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[13]]$version_group
## $moves[[35]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[35]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[35]]$version_group_details[[14]]
## $moves[[35]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[14]]$move_learn_method
## $moves[[35]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[14]]$version_group
## $moves[[35]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[35]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[35]]$version_group_details[[15]]
## $moves[[35]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[15]]$move_learn_method
## $moves[[35]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[15]]$version_group
## $moves[[35]]$version_group_details[[15]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[35]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[35]]$version_group_details[[16]]
## $moves[[35]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[35]]$version_group_details[[16]]$move_learn_method
## $moves[[35]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[35]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[35]]$version_group_details[[16]]$version_group
## $moves[[35]]$version_group_details[[16]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[35]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[36]]
## $moves[[36]]$move
## $moves[[36]]$move$name
## [1] "snore"
## 
## $moves[[36]]$move$url
## [1] "https://pokeapi.co/api/v2/move/173/"
## 
## 
## $moves[[36]]$version_group_details
## $moves[[36]]$version_group_details[[1]]
## $moves[[36]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[1]]$move_learn_method
## $moves[[36]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[36]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[36]]$version_group_details[[1]]$version_group
## $moves[[36]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[36]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[36]]$version_group_details[[2]]
## $moves[[36]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[2]]$move_learn_method
## $moves[[36]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[36]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[36]]$version_group_details[[2]]$version_group
## $moves[[36]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[36]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[36]]$version_group_details[[3]]
## $moves[[36]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[3]]$move_learn_method
## $moves[[36]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[36]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[36]]$version_group_details[[3]]$version_group
## $moves[[36]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[36]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[36]]$version_group_details[[4]]
## $moves[[36]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[4]]$move_learn_method
## $moves[[36]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[36]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[36]]$version_group_details[[4]]$version_group
## $moves[[36]]$version_group_details[[4]]$version_group$name
## [1] "platinum"
## 
## $moves[[36]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[36]]$version_group_details[[5]]
## $moves[[36]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[5]]$move_learn_method
## $moves[[36]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[36]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[36]]$version_group_details[[5]]$version_group
## $moves[[36]]$version_group_details[[5]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[36]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[36]]$version_group_details[[6]]
## $moves[[36]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[6]]$move_learn_method
## $moves[[36]]$version_group_details[[6]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[36]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[36]]$version_group_details[[6]]$version_group
## $moves[[36]]$version_group_details[[6]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[36]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[36]]$version_group_details[[7]]
## $moves[[36]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[7]]$move_learn_method
## $moves[[36]]$version_group_details[[7]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[36]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[36]]$version_group_details[[7]]$version_group
## $moves[[36]]$version_group_details[[7]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[36]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[36]]$version_group_details[[8]]
## $moves[[36]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[8]]$move_learn_method
## $moves[[36]]$version_group_details[[8]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[36]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[36]]$version_group_details[[8]]$version_group
## $moves[[36]]$version_group_details[[8]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[36]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[36]]$version_group_details[[9]]
## $moves[[36]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[36]]$version_group_details[[9]]$move_learn_method
## $moves[[36]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[36]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[36]]$version_group_details[[9]]$version_group
## $moves[[36]]$version_group_details[[9]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[36]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[37]]
## $moves[[37]]$move
## $moves[[37]]$move$name
## [1] "curse"
## 
## $moves[[37]]$move$url
## [1] "https://pokeapi.co/api/v2/move/174/"
## 
## 
## $moves[[37]]$version_group_details
## $moves[[37]]$version_group_details[[1]]
## $moves[[37]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[1]]$move_learn_method
## $moves[[37]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[37]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[37]]$version_group_details[[1]]$version_group
## $moves[[37]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[37]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[37]]$version_group_details[[2]]
## $moves[[37]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[2]]$move_learn_method
## $moves[[37]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[37]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[37]]$version_group_details[[2]]$version_group
## $moves[[37]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[37]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[37]]$version_group_details[[3]]
## $moves[[37]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[3]]$move_learn_method
## $moves[[37]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[3]]$version_group
## $moves[[37]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[37]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[37]]$version_group_details[[4]]
## $moves[[37]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[4]]$move_learn_method
## $moves[[37]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[4]]$version_group
## $moves[[37]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[37]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[37]]$version_group_details[[5]]
## $moves[[37]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[5]]$move_learn_method
## $moves[[37]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[5]]$version_group
## $moves[[37]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[37]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[37]]$version_group_details[[6]]
## $moves[[37]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[6]]$move_learn_method
## $moves[[37]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[6]]$version_group
## $moves[[37]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[37]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[37]]$version_group_details[[7]]
## $moves[[37]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[7]]$move_learn_method
## $moves[[37]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[7]]$version_group
## $moves[[37]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[37]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[37]]$version_group_details[[8]]
## $moves[[37]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[8]]$move_learn_method
## $moves[[37]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[8]]$version_group
## $moves[[37]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[37]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[37]]$version_group_details[[9]]
## $moves[[37]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[9]]$move_learn_method
## $moves[[37]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[9]]$version_group
## $moves[[37]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[37]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[37]]$version_group_details[[10]]
## $moves[[37]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[10]]$move_learn_method
## $moves[[37]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[10]]$version_group
## $moves[[37]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[37]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[37]]$version_group_details[[11]]
## $moves[[37]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[11]]$move_learn_method
## $moves[[37]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[11]]$version_group
## $moves[[37]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[37]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[37]]$version_group_details[[12]]
## $moves[[37]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[12]]$move_learn_method
## $moves[[37]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[12]]$version_group
## $moves[[37]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[37]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[37]]$version_group_details[[13]]
## $moves[[37]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[13]]$move_learn_method
## $moves[[37]]$version_group_details[[13]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[13]]$version_group
## $moves[[37]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[37]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[37]]$version_group_details[[14]]
## $moves[[37]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[14]]$move_learn_method
## $moves[[37]]$version_group_details[[14]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[14]]$version_group
## $moves[[37]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[37]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[37]]$version_group_details[[15]]
## $moves[[37]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[37]]$version_group_details[[15]]$move_learn_method
## $moves[[37]]$version_group_details[[15]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[37]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[37]]$version_group_details[[15]]$version_group
## $moves[[37]]$version_group_details[[15]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[37]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[38]]
## $moves[[38]]$move
## $moves[[38]]$move$name
## [1] "protect"
## 
## $moves[[38]]$move$url
## [1] "https://pokeapi.co/api/v2/move/182/"
## 
## 
## $moves[[38]]$version_group_details
## $moves[[38]]$version_group_details[[1]]
## $moves[[38]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[1]]$move_learn_method
## $moves[[38]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[1]]$version_group
## $moves[[38]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[38]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[38]]$version_group_details[[2]]
## $moves[[38]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[2]]$move_learn_method
## $moves[[38]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[2]]$version_group
## $moves[[38]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[38]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[38]]$version_group_details[[3]]
## $moves[[38]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[3]]$move_learn_method
## $moves[[38]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[3]]$version_group
## $moves[[38]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[38]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[38]]$version_group_details[[4]]
## $moves[[38]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[4]]$move_learn_method
## $moves[[38]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[4]]$version_group
## $moves[[38]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[38]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[38]]$version_group_details[[5]]
## $moves[[38]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[5]]$move_learn_method
## $moves[[38]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[5]]$version_group
## $moves[[38]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[38]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[38]]$version_group_details[[6]]
## $moves[[38]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[6]]$move_learn_method
## $moves[[38]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[6]]$version_group
## $moves[[38]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[38]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[38]]$version_group_details[[7]]
## $moves[[38]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[7]]$move_learn_method
## $moves[[38]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[7]]$version_group
## $moves[[38]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[38]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[38]]$version_group_details[[8]]
## $moves[[38]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[8]]$move_learn_method
## $moves[[38]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[8]]$version_group
## $moves[[38]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[38]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[38]]$version_group_details[[9]]
## $moves[[38]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[9]]$move_learn_method
## $moves[[38]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[9]]$version_group
## $moves[[38]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[38]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[38]]$version_group_details[[10]]
## $moves[[38]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[10]]$move_learn_method
## $moves[[38]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[10]]$version_group
## $moves[[38]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[38]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[38]]$version_group_details[[11]]
## $moves[[38]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[11]]$move_learn_method
## $moves[[38]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[11]]$version_group
## $moves[[38]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[38]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[38]]$version_group_details[[12]]
## $moves[[38]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[12]]$move_learn_method
## $moves[[38]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[12]]$version_group
## $moves[[38]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[38]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[38]]$version_group_details[[13]]
## $moves[[38]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[13]]$move_learn_method
## $moves[[38]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[13]]$version_group
## $moves[[38]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[38]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[38]]$version_group_details[[14]]
## $moves[[38]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[14]]$move_learn_method
## $moves[[38]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[14]]$version_group
## $moves[[38]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[38]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[38]]$version_group_details[[15]]
## $moves[[38]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[15]]$move_learn_method
## $moves[[38]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[15]]$version_group
## $moves[[38]]$version_group_details[[15]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[38]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[38]]$version_group_details[[16]]
## $moves[[38]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[16]]$move_learn_method
## $moves[[38]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[16]]$version_group
## $moves[[38]]$version_group_details[[16]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[38]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[38]]$version_group_details[[17]]
## $moves[[38]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[17]]$move_learn_method
## $moves[[38]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[17]]$version_group
## $moves[[38]]$version_group_details[[17]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[38]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[38]]$version_group_details[[18]]
## $moves[[38]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[38]]$version_group_details[[18]]$move_learn_method
## $moves[[38]]$version_group_details[[18]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[38]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[38]]$version_group_details[[18]]$version_group
## $moves[[38]]$version_group_details[[18]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[38]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[39]]
## $moves[[39]]$move
## $moves[[39]]$move$name
## [1] "sludge-bomb"
## 
## $moves[[39]]$move$url
## [1] "https://pokeapi.co/api/v2/move/188/"
## 
## 
## $moves[[39]]$version_group_details
## $moves[[39]]$version_group_details[[1]]
## $moves[[39]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[1]]$move_learn_method
## $moves[[39]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[1]]$version_group
## $moves[[39]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[39]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[39]]$version_group_details[[2]]
## $moves[[39]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[2]]$move_learn_method
## $moves[[39]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[2]]$version_group
## $moves[[39]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[39]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[39]]$version_group_details[[3]]
## $moves[[39]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[3]]$move_learn_method
## $moves[[39]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[3]]$version_group
## $moves[[39]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[39]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[39]]$version_group_details[[4]]
## $moves[[39]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[4]]$move_learn_method
## $moves[[39]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[4]]$version_group
## $moves[[39]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[39]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[39]]$version_group_details[[5]]
## $moves[[39]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[5]]$move_learn_method
## $moves[[39]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[5]]$version_group
## $moves[[39]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[39]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[39]]$version_group_details[[6]]
## $moves[[39]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[6]]$move_learn_method
## $moves[[39]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[6]]$version_group
## $moves[[39]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[39]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[39]]$version_group_details[[7]]
## $moves[[39]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[7]]$move_learn_method
## $moves[[39]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[7]]$version_group
## $moves[[39]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[39]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[39]]$version_group_details[[8]]
## $moves[[39]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[8]]$move_learn_method
## $moves[[39]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[8]]$version_group
## $moves[[39]]$version_group_details[[8]]$version_group$name
## [1] "colosseum"
## 
## $moves[[39]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[39]]$version_group_details[[9]]
## $moves[[39]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[9]]$move_learn_method
## $moves[[39]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[9]]$version_group
## $moves[[39]]$version_group_details[[9]]$version_group$name
## [1] "xd"
## 
## $moves[[39]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[39]]$version_group_details[[10]]
## $moves[[39]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[10]]$move_learn_method
## $moves[[39]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[10]]$version_group
## $moves[[39]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[39]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[39]]$version_group_details[[11]]
## $moves[[39]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[11]]$move_learn_method
## $moves[[39]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[11]]$version_group
## $moves[[39]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[39]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[39]]$version_group_details[[12]]
## $moves[[39]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[12]]$move_learn_method
## $moves[[39]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[12]]$version_group
## $moves[[39]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[39]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[39]]$version_group_details[[13]]
## $moves[[39]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[13]]$move_learn_method
## $moves[[39]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[13]]$version_group
## $moves[[39]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[39]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[39]]$version_group_details[[14]]
## $moves[[39]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[14]]$move_learn_method
## $moves[[39]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[14]]$version_group
## $moves[[39]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[39]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[39]]$version_group_details[[15]]
## $moves[[39]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[15]]$move_learn_method
## $moves[[39]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[15]]$version_group
## $moves[[39]]$version_group_details[[15]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[39]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[39]]$version_group_details[[16]]
## $moves[[39]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[39]]$version_group_details[[16]]$move_learn_method
## $moves[[39]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[39]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[39]]$version_group_details[[16]]$version_group
## $moves[[39]]$version_group_details[[16]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[39]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[40]]
## $moves[[40]]$move
## $moves[[40]]$move$name
## [1] "mud-slap"
## 
## $moves[[40]]$move$url
## [1] "https://pokeapi.co/api/v2/move/189/"
## 
## 
## $moves[[40]]$version_group_details
## $moves[[40]]$version_group_details[[1]]
## $moves[[40]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[40]]$version_group_details[[1]]$move_learn_method
## $moves[[40]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[40]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[40]]$version_group_details[[1]]$version_group
## $moves[[40]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[40]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[40]]$version_group_details[[2]]
## $moves[[40]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[40]]$version_group_details[[2]]$move_learn_method
## $moves[[40]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[40]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[40]]$version_group_details[[2]]$version_group
## $moves[[40]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[40]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[40]]$version_group_details[[3]]
## $moves[[40]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[40]]$version_group_details[[3]]$move_learn_method
## $moves[[40]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[40]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[40]]$version_group_details[[3]]$version_group
## $moves[[40]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[40]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[40]]$version_group_details[[4]]
## $moves[[40]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[40]]$version_group_details[[4]]$move_learn_method
## $moves[[40]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[40]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[40]]$version_group_details[[4]]$version_group
## $moves[[40]]$version_group_details[[4]]$version_group$name
## [1] "platinum"
## 
## $moves[[40]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[40]]$version_group_details[[5]]
## $moves[[40]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[40]]$version_group_details[[5]]$move_learn_method
## $moves[[40]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[40]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[40]]$version_group_details[[5]]$version_group
## $moves[[40]]$version_group_details[[5]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[40]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## 
## 
## $moves[[41]]
## $moves[[41]]$move
## $moves[[41]]$move$name
## [1] "outrage"
## 
## $moves[[41]]$move$url
## [1] "https://pokeapi.co/api/v2/move/200/"
## 
## 
## $moves[[41]]$version_group_details
## $moves[[41]]$version_group_details[[1]]
## $moves[[41]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[41]]$version_group_details[[1]]$move_learn_method
## $moves[[41]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[41]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[41]]$version_group_details[[1]]$version_group
## $moves[[41]]$version_group_details[[1]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[41]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## 
## 
## $moves[[42]]
## $moves[[42]]$move
## $moves[[42]]$move$name
## [1] "giga-drain"
## 
## $moves[[42]]$move$url
## [1] "https://pokeapi.co/api/v2/move/202/"
## 
## 
## $moves[[42]]$version_group_details
## $moves[[42]]$version_group_details[[1]]
## $moves[[42]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[1]]$move_learn_method
## $moves[[42]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[1]]$version_group
## $moves[[42]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[42]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[42]]$version_group_details[[2]]
## $moves[[42]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[2]]$move_learn_method
## $moves[[42]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[2]]$version_group
## $moves[[42]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[42]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[42]]$version_group_details[[3]]
## $moves[[42]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[3]]$move_learn_method
## $moves[[42]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[3]]$version_group
## $moves[[42]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[42]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[42]]$version_group_details[[4]]
## $moves[[42]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[4]]$move_learn_method
## $moves[[42]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[4]]$version_group
## $moves[[42]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[42]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[42]]$version_group_details[[5]]
## $moves[[42]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[5]]$move_learn_method
## $moves[[42]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[5]]$version_group
## $moves[[42]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[42]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[42]]$version_group_details[[6]]
## $moves[[42]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[6]]$move_learn_method
## $moves[[42]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[6]]$version_group
## $moves[[42]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[42]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[42]]$version_group_details[[7]]
## $moves[[42]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[7]]$move_learn_method
## $moves[[42]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[7]]$version_group
## $moves[[42]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[42]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[42]]$version_group_details[[8]]
## $moves[[42]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[8]]$move_learn_method
## $moves[[42]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[8]]$version_group
## $moves[[42]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[42]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[42]]$version_group_details[[9]]
## $moves[[42]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[9]]$move_learn_method
## $moves[[42]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[42]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[42]]$version_group_details[[9]]$version_group
## $moves[[42]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[42]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[42]]$version_group_details[[10]]
## $moves[[42]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[10]]$move_learn_method
## $moves[[42]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[10]]$version_group
## $moves[[42]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[42]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[42]]$version_group_details[[11]]
## $moves[[42]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[11]]$move_learn_method
## $moves[[42]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[11]]$version_group
## $moves[[42]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[42]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[42]]$version_group_details[[12]]
## $moves[[42]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[12]]$move_learn_method
## $moves[[42]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[42]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[42]]$version_group_details[[12]]$version_group
## $moves[[42]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[42]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[42]]$version_group_details[[13]]
## $moves[[42]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[13]]$move_learn_method
## $moves[[42]]$version_group_details[[13]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[42]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[42]]$version_group_details[[13]]$version_group
## $moves[[42]]$version_group_details[[13]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[42]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[42]]$version_group_details[[14]]
## $moves[[42]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[14]]$move_learn_method
## $moves[[42]]$version_group_details[[14]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[42]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[42]]$version_group_details[[14]]$version_group
## $moves[[42]]$version_group_details[[14]]$version_group$name
## [1] "x-y"
## 
## $moves[[42]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[42]]$version_group_details[[15]]
## $moves[[42]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[15]]$move_learn_method
## $moves[[42]]$version_group_details[[15]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[42]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[42]]$version_group_details[[15]]$version_group
## $moves[[42]]$version_group_details[[15]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[42]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[42]]$version_group_details[[16]]
## $moves[[42]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[16]]$move_learn_method
## $moves[[42]]$version_group_details[[16]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[42]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[42]]$version_group_details[[16]]$version_group
## $moves[[42]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[42]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[42]]$version_group_details[[17]]
## $moves[[42]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[17]]$move_learn_method
## $moves[[42]]$version_group_details[[17]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[42]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[42]]$version_group_details[[17]]$version_group
## $moves[[42]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[42]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[42]]$version_group_details[[18]]
## $moves[[42]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[18]]$move_learn_method
## $moves[[42]]$version_group_details[[18]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[42]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[42]]$version_group_details[[18]]$version_group
## $moves[[42]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[42]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[42]]$version_group_details[[19]]
## $moves[[42]]$version_group_details[[19]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[19]]$move_learn_method
## $moves[[42]]$version_group_details[[19]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[42]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[42]]$version_group_details[[19]]$version_group
## $moves[[42]]$version_group_details[[19]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[42]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[42]]$version_group_details[[20]]
## $moves[[42]]$version_group_details[[20]]$level_learned_at
## [1] 0
## 
## $moves[[42]]$version_group_details[[20]]$move_learn_method
## $moves[[42]]$version_group_details[[20]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[42]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[42]]$version_group_details[[20]]$version_group
## $moves[[42]]$version_group_details[[20]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[42]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[43]]
## $moves[[43]]$move
## $moves[[43]]$move$name
## [1] "endure"
## 
## $moves[[43]]$move$url
## [1] "https://pokeapi.co/api/v2/move/203/"
## 
## 
## $moves[[43]]$version_group_details
## $moves[[43]]$version_group_details[[1]]
## $moves[[43]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[1]]$move_learn_method
## $moves[[43]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[43]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[43]]$version_group_details[[1]]$version_group
## $moves[[43]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[43]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[43]]$version_group_details[[2]]
## $moves[[43]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[2]]$move_learn_method
## $moves[[43]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[43]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[43]]$version_group_details[[2]]$version_group
## $moves[[43]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[43]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[43]]$version_group_details[[3]]
## $moves[[43]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[3]]$move_learn_method
## $moves[[43]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[43]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[43]]$version_group_details[[3]]$version_group
## $moves[[43]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[43]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[43]]$version_group_details[[4]]
## $moves[[43]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[4]]$move_learn_method
## $moves[[43]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[43]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[43]]$version_group_details[[4]]$version_group
## $moves[[43]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[43]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[43]]$version_group_details[[5]]
## $moves[[43]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[5]]$move_learn_method
## $moves[[43]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[43]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[43]]$version_group_details[[5]]$version_group
## $moves[[43]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[43]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[43]]$version_group_details[[6]]
## $moves[[43]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[6]]$move_learn_method
## $moves[[43]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[43]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[43]]$version_group_details[[6]]$version_group
## $moves[[43]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[43]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[43]]$version_group_details[[7]]
## $moves[[43]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[7]]$move_learn_method
## $moves[[43]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[43]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[43]]$version_group_details[[7]]$version_group
## $moves[[43]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[43]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[43]]$version_group_details[[8]]
## $moves[[43]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[8]]$move_learn_method
## $moves[[43]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[43]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[43]]$version_group_details[[8]]$version_group
## $moves[[43]]$version_group_details[[8]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[43]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[43]]$version_group_details[[9]]
## $moves[[43]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[9]]$move_learn_method
## $moves[[43]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[43]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[43]]$version_group_details[[9]]$version_group
## $moves[[43]]$version_group_details[[9]]$version_group$name
## [1] "x-y"
## 
## $moves[[43]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[43]]$version_group_details[[10]]
## $moves[[43]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[10]]$move_learn_method
## $moves[[43]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[43]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[43]]$version_group_details[[10]]$version_group
## $moves[[43]]$version_group_details[[10]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[43]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[43]]$version_group_details[[11]]
## $moves[[43]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[11]]$move_learn_method
## $moves[[43]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[43]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[43]]$version_group_details[[11]]$version_group
## $moves[[43]]$version_group_details[[11]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[43]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[43]]$version_group_details[[12]]
## $moves[[43]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[12]]$move_learn_method
## $moves[[43]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[43]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[43]]$version_group_details[[12]]$version_group
## $moves[[43]]$version_group_details[[12]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[43]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[43]]$version_group_details[[13]]
## $moves[[43]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[43]]$version_group_details[[13]]$move_learn_method
## $moves[[43]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[43]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[43]]$version_group_details[[13]]$version_group
## $moves[[43]]$version_group_details[[13]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[43]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[44]]
## $moves[[44]]$move
## $moves[[44]]$move$name
## [1] "charm"
## 
## $moves[[44]]$move$url
## [1] "https://pokeapi.co/api/v2/move/204/"
## 
## 
## $moves[[44]]$version_group_details
## $moves[[44]]$version_group_details[[1]]
## $moves[[44]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[1]]$move_learn_method
## $moves[[44]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[1]]$version_group
## $moves[[44]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[44]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[44]]$version_group_details[[2]]
## $moves[[44]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[2]]$move_learn_method
## $moves[[44]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[2]]$version_group
## $moves[[44]]$version_group_details[[2]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[44]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[44]]$version_group_details[[3]]
## $moves[[44]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[3]]$move_learn_method
## $moves[[44]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[3]]$version_group
## $moves[[44]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[44]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[44]]$version_group_details[[4]]
## $moves[[44]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[4]]$move_learn_method
## $moves[[44]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[4]]$version_group
## $moves[[44]]$version_group_details[[4]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[44]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[44]]$version_group_details[[5]]
## $moves[[44]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[5]]$move_learn_method
## $moves[[44]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[5]]$version_group
## $moves[[44]]$version_group_details[[5]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[44]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[44]]$version_group_details[[6]]
## $moves[[44]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[6]]$move_learn_method
## $moves[[44]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[6]]$version_group
## $moves[[44]]$version_group_details[[6]]$version_group$name
## [1] "platinum"
## 
## $moves[[44]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[44]]$version_group_details[[7]]
## $moves[[44]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[7]]$move_learn_method
## $moves[[44]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[7]]$version_group
## $moves[[44]]$version_group_details[[7]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[44]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[44]]$version_group_details[[8]]
## $moves[[44]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[8]]$move_learn_method
## $moves[[44]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[8]]$version_group
## $moves[[44]]$version_group_details[[8]]$version_group$name
## [1] "black-white"
## 
## $moves[[44]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[44]]$version_group_details[[9]]
## $moves[[44]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[9]]$move_learn_method
## $moves[[44]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[9]]$version_group
## $moves[[44]]$version_group_details[[9]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[44]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[44]]$version_group_details[[10]]
## $moves[[44]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[10]]$move_learn_method
## $moves[[44]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[10]]$version_group
## $moves[[44]]$version_group_details[[10]]$version_group$name
## [1] "x-y"
## 
## $moves[[44]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[44]]$version_group_details[[11]]
## $moves[[44]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[11]]$move_learn_method
## $moves[[44]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[11]]$version_group
## $moves[[44]]$version_group_details[[11]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[44]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[44]]$version_group_details[[12]]
## $moves[[44]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[12]]$move_learn_method
## $moves[[44]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[12]]$version_group
## $moves[[44]]$version_group_details[[12]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[44]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[44]]$version_group_details[[13]]
## $moves[[44]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[13]]$move_learn_method
## $moves[[44]]$version_group_details[[13]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[44]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[44]]$version_group_details[[13]]$version_group
## $moves[[44]]$version_group_details[[13]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[44]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[44]]$version_group_details[[14]]
## $moves[[44]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[44]]$version_group_details[[14]]$move_learn_method
## $moves[[44]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[44]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[44]]$version_group_details[[14]]$version_group
## $moves[[44]]$version_group_details[[14]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[44]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[45]]
## $moves[[45]]$move
## $moves[[45]]$move$name
## [1] "false-swipe"
## 
## $moves[[45]]$move$url
## [1] "https://pokeapi.co/api/v2/move/206/"
## 
## 
## $moves[[45]]$version_group_details
## $moves[[45]]$version_group_details[[1]]
## $moves[[45]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[45]]$version_group_details[[1]]$move_learn_method
## $moves[[45]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[45]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[45]]$version_group_details[[1]]$version_group
## $moves[[45]]$version_group_details[[1]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[45]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[46]]
## $moves[[46]]$move
## $moves[[46]]$move$name
## [1] "swagger"
## 
## $moves[[46]]$move$url
## [1] "https://pokeapi.co/api/v2/move/207/"
## 
## 
## $moves[[46]]$version_group_details
## $moves[[46]]$version_group_details[[1]]
## $moves[[46]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[1]]$move_learn_method
## $moves[[46]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[1]]$version_group
## $moves[[46]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[46]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[46]]$version_group_details[[2]]
## $moves[[46]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[2]]$move_learn_method
## $moves[[46]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[2]]$version_group
## $moves[[46]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[46]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[46]]$version_group_details[[3]]
## $moves[[46]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[3]]$move_learn_method
## $moves[[46]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[46]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[46]]$version_group_details[[3]]$version_group
## $moves[[46]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[46]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[46]]$version_group_details[[4]]
## $moves[[46]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[4]]$move_learn_method
## $moves[[46]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[4]]$version_group
## $moves[[46]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[46]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[46]]$version_group_details[[5]]
## $moves[[46]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[5]]$move_learn_method
## $moves[[46]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[5]]$version_group
## $moves[[46]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[46]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[46]]$version_group_details[[6]]
## $moves[[46]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[6]]$move_learn_method
## $moves[[46]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[6]]$version_group
## $moves[[46]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[46]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[46]]$version_group_details[[7]]
## $moves[[46]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[7]]$move_learn_method
## $moves[[46]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[7]]$version_group
## $moves[[46]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[46]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[46]]$version_group_details[[8]]
## $moves[[46]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[8]]$move_learn_method
## $moves[[46]]$version_group_details[[8]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[46]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[46]]$version_group_details[[8]]$version_group
## $moves[[46]]$version_group_details[[8]]$version_group$name
## [1] "xd"
## 
## $moves[[46]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[46]]$version_group_details[[9]]
## $moves[[46]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[9]]$move_learn_method
## $moves[[46]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[9]]$version_group
## $moves[[46]]$version_group_details[[9]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[46]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[46]]$version_group_details[[10]]
## $moves[[46]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[10]]$move_learn_method
## $moves[[46]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[10]]$version_group
## $moves[[46]]$version_group_details[[10]]$version_group$name
## [1] "x-y"
## 
## $moves[[46]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[46]]$version_group_details[[11]]
## $moves[[46]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[11]]$move_learn_method
## $moves[[46]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[11]]$version_group
## $moves[[46]]$version_group_details[[11]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[46]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[46]]$version_group_details[[12]]
## $moves[[46]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[12]]$move_learn_method
## $moves[[46]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[12]]$version_group
## $moves[[46]]$version_group_details[[12]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[46]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[46]]$version_group_details[[13]]
## $moves[[46]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[46]]$version_group_details[[13]]$move_learn_method
## $moves[[46]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[46]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[46]]$version_group_details[[13]]$version_group
## $moves[[46]]$version_group_details[[13]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[46]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[47]]
## $moves[[47]]$move
## $moves[[47]]$move$name
## [1] "fury-cutter"
## 
## $moves[[47]]$move$url
## [1] "https://pokeapi.co/api/v2/move/210/"
## 
## 
## $moves[[47]]$version_group_details
## $moves[[47]]$version_group_details[[1]]
## $moves[[47]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[47]]$version_group_details[[1]]$move_learn_method
## $moves[[47]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[47]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[47]]$version_group_details[[1]]$version_group
## $moves[[47]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[47]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[47]]$version_group_details[[2]]
## $moves[[47]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[47]]$version_group_details[[2]]$move_learn_method
## $moves[[47]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[47]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[47]]$version_group_details[[2]]$version_group
## $moves[[47]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[47]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[47]]$version_group_details[[3]]
## $moves[[47]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[47]]$version_group_details[[3]]$move_learn_method
## $moves[[47]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[47]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[47]]$version_group_details[[3]]$version_group
## $moves[[47]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[47]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[47]]$version_group_details[[4]]
## $moves[[47]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[47]]$version_group_details[[4]]$move_learn_method
## $moves[[47]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[47]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[47]]$version_group_details[[4]]$version_group
## $moves[[47]]$version_group_details[[4]]$version_group$name
## [1] "platinum"
## 
## $moves[[47]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[47]]$version_group_details[[5]]
## $moves[[47]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[47]]$version_group_details[[5]]$move_learn_method
## $moves[[47]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[47]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[47]]$version_group_details[[5]]$version_group
## $moves[[47]]$version_group_details[[5]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[47]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## 
## 
## $moves[[48]]
## $moves[[48]]$move
## $moves[[48]]$move$name
## [1] "attract"
## 
## $moves[[48]]$move$url
## [1] "https://pokeapi.co/api/v2/move/213/"
## 
## 
## $moves[[48]]$version_group_details
## $moves[[48]]$version_group_details[[1]]
## $moves[[48]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[1]]$move_learn_method
## $moves[[48]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[1]]$version_group
## $moves[[48]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[48]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[48]]$version_group_details[[2]]
## $moves[[48]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[2]]$move_learn_method
## $moves[[48]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[2]]$version_group
## $moves[[48]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[48]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[48]]$version_group_details[[3]]
## $moves[[48]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[3]]$move_learn_method
## $moves[[48]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[3]]$version_group
## $moves[[48]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[48]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[48]]$version_group_details[[4]]
## $moves[[48]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[4]]$move_learn_method
## $moves[[48]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[4]]$version_group
## $moves[[48]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[48]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[48]]$version_group_details[[5]]
## $moves[[48]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[5]]$move_learn_method
## $moves[[48]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[5]]$version_group
## $moves[[48]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[48]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[48]]$version_group_details[[6]]
## $moves[[48]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[6]]$move_learn_method
## $moves[[48]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[6]]$version_group
## $moves[[48]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[48]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[48]]$version_group_details[[7]]
## $moves[[48]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[7]]$move_learn_method
## $moves[[48]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[7]]$version_group
## $moves[[48]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[48]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[48]]$version_group_details[[8]]
## $moves[[48]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[8]]$move_learn_method
## $moves[[48]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[8]]$version_group
## $moves[[48]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[48]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[48]]$version_group_details[[9]]
## $moves[[48]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[9]]$move_learn_method
## $moves[[48]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[9]]$version_group
## $moves[[48]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[48]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[48]]$version_group_details[[10]]
## $moves[[48]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[10]]$move_learn_method
## $moves[[48]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[10]]$version_group
## $moves[[48]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[48]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[48]]$version_group_details[[11]]
## $moves[[48]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[11]]$move_learn_method
## $moves[[48]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[11]]$version_group
## $moves[[48]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[48]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[48]]$version_group_details[[12]]
## $moves[[48]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[12]]$move_learn_method
## $moves[[48]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[12]]$version_group
## $moves[[48]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[48]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[48]]$version_group_details[[13]]
## $moves[[48]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[13]]$move_learn_method
## $moves[[48]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[13]]$version_group
## $moves[[48]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[48]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[48]]$version_group_details[[14]]
## $moves[[48]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[14]]$move_learn_method
## $moves[[48]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[14]]$version_group
## $moves[[48]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[48]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[48]]$version_group_details[[15]]
## $moves[[48]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[15]]$move_learn_method
## $moves[[48]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[15]]$version_group
## $moves[[48]]$version_group_details[[15]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[48]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[48]]$version_group_details[[16]]
## $moves[[48]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[16]]$move_learn_method
## $moves[[48]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[16]]$version_group
## $moves[[48]]$version_group_details[[16]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[48]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[48]]$version_group_details[[17]]
## $moves[[48]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[48]]$version_group_details[[17]]$move_learn_method
## $moves[[48]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[48]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[48]]$version_group_details[[17]]$version_group
## $moves[[48]]$version_group_details[[17]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[48]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[49]]
## $moves[[49]]$move
## $moves[[49]]$move$name
## [1] "sleep-talk"
## 
## $moves[[49]]$move$url
## [1] "https://pokeapi.co/api/v2/move/214/"
## 
## 
## $moves[[49]]$version_group_details
## $moves[[49]]$version_group_details[[1]]
## $moves[[49]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[1]]$move_learn_method
## $moves[[49]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[1]]$version_group
## $moves[[49]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[49]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[49]]$version_group_details[[2]]
## $moves[[49]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[2]]$move_learn_method
## $moves[[49]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[2]]$version_group
## $moves[[49]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[49]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[49]]$version_group_details[[3]]
## $moves[[49]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[3]]$move_learn_method
## $moves[[49]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[49]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[49]]$version_group_details[[3]]$version_group
## $moves[[49]]$version_group_details[[3]]$version_group$name
## [1] "emerald"
## 
## $moves[[49]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[49]]$version_group_details[[4]]
## $moves[[49]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[4]]$move_learn_method
## $moves[[49]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[4]]$version_group
## $moves[[49]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[49]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[49]]$version_group_details[[5]]
## $moves[[49]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[5]]$move_learn_method
## $moves[[49]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[5]]$version_group
## $moves[[49]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[49]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[49]]$version_group_details[[6]]
## $moves[[49]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[6]]$move_learn_method
## $moves[[49]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[6]]$version_group
## $moves[[49]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[49]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[49]]$version_group_details[[7]]
## $moves[[49]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[7]]$move_learn_method
## $moves[[49]]$version_group_details[[7]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[49]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[49]]$version_group_details[[7]]$version_group
## $moves[[49]]$version_group_details[[7]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[49]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[49]]$version_group_details[[8]]
## $moves[[49]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[8]]$move_learn_method
## $moves[[49]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[8]]$version_group
## $moves[[49]]$version_group_details[[8]]$version_group$name
## [1] "x-y"
## 
## $moves[[49]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[49]]$version_group_details[[9]]
## $moves[[49]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[9]]$move_learn_method
## $moves[[49]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[9]]$version_group
## $moves[[49]]$version_group_details[[9]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[49]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[49]]$version_group_details[[10]]
## $moves[[49]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[10]]$move_learn_method
## $moves[[49]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[10]]$version_group
## $moves[[49]]$version_group_details[[10]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[49]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[49]]$version_group_details[[11]]
## $moves[[49]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[11]]$move_learn_method
## $moves[[49]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[11]]$version_group
## $moves[[49]]$version_group_details[[11]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[49]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[49]]$version_group_details[[12]]
## $moves[[49]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[49]]$version_group_details[[12]]$move_learn_method
## $moves[[49]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[49]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[49]]$version_group_details[[12]]$version_group
## $moves[[49]]$version_group_details[[12]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[49]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[50]]
## $moves[[50]]$move
## $moves[[50]]$move$name
## [1] "return"
## 
## $moves[[50]]$move$url
## [1] "https://pokeapi.co/api/v2/move/216/"
## 
## 
## $moves[[50]]$version_group_details
## $moves[[50]]$version_group_details[[1]]
## $moves[[50]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[1]]$move_learn_method
## $moves[[50]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[1]]$version_group
## $moves[[50]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[50]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[50]]$version_group_details[[2]]
## $moves[[50]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[2]]$move_learn_method
## $moves[[50]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[2]]$version_group
## $moves[[50]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[50]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[50]]$version_group_details[[3]]
## $moves[[50]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[3]]$move_learn_method
## $moves[[50]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[3]]$version_group
## $moves[[50]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[50]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[50]]$version_group_details[[4]]
## $moves[[50]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[4]]$move_learn_method
## $moves[[50]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[4]]$version_group
## $moves[[50]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[50]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[50]]$version_group_details[[5]]
## $moves[[50]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[5]]$move_learn_method
## $moves[[50]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[5]]$version_group
## $moves[[50]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[50]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[50]]$version_group_details[[6]]
## $moves[[50]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[6]]$move_learn_method
## $moves[[50]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[6]]$version_group
## $moves[[50]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[50]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[50]]$version_group_details[[7]]
## $moves[[50]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[7]]$move_learn_method
## $moves[[50]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[7]]$version_group
## $moves[[50]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[50]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[50]]$version_group_details[[8]]
## $moves[[50]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[8]]$move_learn_method
## $moves[[50]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[8]]$version_group
## $moves[[50]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[50]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[50]]$version_group_details[[9]]
## $moves[[50]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[9]]$move_learn_method
## $moves[[50]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[9]]$version_group
## $moves[[50]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[50]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[50]]$version_group_details[[10]]
## $moves[[50]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[10]]$move_learn_method
## $moves[[50]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[10]]$version_group
## $moves[[50]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[50]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[50]]$version_group_details[[11]]
## $moves[[50]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[11]]$move_learn_method
## $moves[[50]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[11]]$version_group
## $moves[[50]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[50]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[50]]$version_group_details[[12]]
## $moves[[50]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[12]]$move_learn_method
## $moves[[50]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[12]]$version_group
## $moves[[50]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[50]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[50]]$version_group_details[[13]]
## $moves[[50]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[13]]$move_learn_method
## $moves[[50]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[13]]$version_group
## $moves[[50]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[50]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[50]]$version_group_details[[14]]
## $moves[[50]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[14]]$move_learn_method
## $moves[[50]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[14]]$version_group
## $moves[[50]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[50]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[50]]$version_group_details[[15]]
## $moves[[50]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[15]]$move_learn_method
## $moves[[50]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[15]]$version_group
## $moves[[50]]$version_group_details[[15]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[50]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[50]]$version_group_details[[16]]
## $moves[[50]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[50]]$version_group_details[[16]]$move_learn_method
## $moves[[50]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[50]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[50]]$version_group_details[[16]]$version_group
## $moves[[50]]$version_group_details[[16]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[50]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[51]]
## $moves[[51]]$move
## $moves[[51]]$move$name
## [1] "frustration"
## 
## $moves[[51]]$move$url
## [1] "https://pokeapi.co/api/v2/move/218/"
## 
## 
## $moves[[51]]$version_group_details
## $moves[[51]]$version_group_details[[1]]
## $moves[[51]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[1]]$move_learn_method
## $moves[[51]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[1]]$version_group
## $moves[[51]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[51]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[51]]$version_group_details[[2]]
## $moves[[51]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[2]]$move_learn_method
## $moves[[51]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[2]]$version_group
## $moves[[51]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[51]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[51]]$version_group_details[[3]]
## $moves[[51]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[3]]$move_learn_method
## $moves[[51]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[3]]$version_group
## $moves[[51]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[51]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[51]]$version_group_details[[4]]
## $moves[[51]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[4]]$move_learn_method
## $moves[[51]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[4]]$version_group
## $moves[[51]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[51]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[51]]$version_group_details[[5]]
## $moves[[51]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[5]]$move_learn_method
## $moves[[51]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[5]]$version_group
## $moves[[51]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[51]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[51]]$version_group_details[[6]]
## $moves[[51]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[6]]$move_learn_method
## $moves[[51]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[6]]$version_group
## $moves[[51]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[51]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[51]]$version_group_details[[7]]
## $moves[[51]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[7]]$move_learn_method
## $moves[[51]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[7]]$version_group
## $moves[[51]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[51]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[51]]$version_group_details[[8]]
## $moves[[51]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[8]]$move_learn_method
## $moves[[51]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[8]]$version_group
## $moves[[51]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[51]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[51]]$version_group_details[[9]]
## $moves[[51]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[9]]$move_learn_method
## $moves[[51]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[9]]$version_group
## $moves[[51]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[51]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[51]]$version_group_details[[10]]
## $moves[[51]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[10]]$move_learn_method
## $moves[[51]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[10]]$version_group
## $moves[[51]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[51]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[51]]$version_group_details[[11]]
## $moves[[51]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[11]]$move_learn_method
## $moves[[51]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[11]]$version_group
## $moves[[51]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[51]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[51]]$version_group_details[[12]]
## $moves[[51]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[12]]$move_learn_method
## $moves[[51]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[12]]$version_group
## $moves[[51]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[51]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[51]]$version_group_details[[13]]
## $moves[[51]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[13]]$move_learn_method
## $moves[[51]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[13]]$version_group
## $moves[[51]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[51]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[51]]$version_group_details[[14]]
## $moves[[51]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[14]]$move_learn_method
## $moves[[51]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[14]]$version_group
## $moves[[51]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[51]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[51]]$version_group_details[[15]]
## $moves[[51]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[15]]$move_learn_method
## $moves[[51]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[15]]$version_group
## $moves[[51]]$version_group_details[[15]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[51]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[51]]$version_group_details[[16]]
## $moves[[51]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[51]]$version_group_details[[16]]$move_learn_method
## $moves[[51]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[51]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[51]]$version_group_details[[16]]$version_group
## $moves[[51]]$version_group_details[[16]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[51]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[52]]
## $moves[[52]]$move
## $moves[[52]]$move$name
## [1] "safeguard"
## 
## $moves[[52]]$move$url
## [1] "https://pokeapi.co/api/v2/move/219/"
## 
## 
## $moves[[52]]$version_group_details
## $moves[[52]]$version_group_details[[1]]
## $moves[[52]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[1]]$move_learn_method
## $moves[[52]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[1]]$version_group
## $moves[[52]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[52]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[52]]$version_group_details[[2]]
## $moves[[52]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[2]]$move_learn_method
## $moves[[52]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[2]]$version_group
## $moves[[52]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[52]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[52]]$version_group_details[[3]]
## $moves[[52]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[3]]$move_learn_method
## $moves[[52]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[3]]$version_group
## $moves[[52]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[52]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[52]]$version_group_details[[4]]
## $moves[[52]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[4]]$move_learn_method
## $moves[[52]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[4]]$version_group
## $moves[[52]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[52]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[52]]$version_group_details[[5]]
## $moves[[52]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[5]]$move_learn_method
## $moves[[52]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[5]]$version_group
## $moves[[52]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[52]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[52]]$version_group_details[[6]]
## $moves[[52]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[6]]$move_learn_method
## $moves[[52]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[6]]$version_group
## $moves[[52]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[52]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[52]]$version_group_details[[7]]
## $moves[[52]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[7]]$move_learn_method
## $moves[[52]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[7]]$version_group
## $moves[[52]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[52]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[52]]$version_group_details[[8]]
## $moves[[52]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[8]]$move_learn_method
## $moves[[52]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[52]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[52]]$version_group_details[[8]]$version_group
## $moves[[52]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[52]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[52]]$version_group_details[[9]]
## $moves[[52]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[9]]$move_learn_method
## $moves[[52]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[9]]$version_group
## $moves[[52]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[52]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[52]]$version_group_details[[10]]
## $moves[[52]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[10]]$move_learn_method
## $moves[[52]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[10]]$version_group
## $moves[[52]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[52]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[52]]$version_group_details[[11]]
## $moves[[52]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[11]]$move_learn_method
## $moves[[52]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[11]]$version_group
## $moves[[52]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[52]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[52]]$version_group_details[[12]]
## $moves[[52]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[12]]$move_learn_method
## $moves[[52]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[12]]$version_group
## $moves[[52]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[52]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[52]]$version_group_details[[13]]
## $moves[[52]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[13]]$move_learn_method
## $moves[[52]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[13]]$version_group
## $moves[[52]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[52]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[52]]$version_group_details[[14]]
## $moves[[52]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[14]]$move_learn_method
## $moves[[52]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[14]]$version_group
## $moves[[52]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[52]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[52]]$version_group_details[[15]]
## $moves[[52]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[52]]$version_group_details[[15]]$move_learn_method
## $moves[[52]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[52]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[52]]$version_group_details[[15]]$version_group
## $moves[[52]]$version_group_details[[15]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[52]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[53]]
## $moves[[53]]$move
## $moves[[53]]$move$name
## [1] "sweet-scent"
## 
## $moves[[53]]$move$url
## [1] "https://pokeapi.co/api/v2/move/230/"
## 
## 
## $moves[[53]]$version_group_details
## $moves[[53]]$version_group_details[[1]]
## $moves[[53]]$version_group_details[[1]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[1]]$move_learn_method
## $moves[[53]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[1]]$version_group
## $moves[[53]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[53]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[53]]$version_group_details[[2]]
## $moves[[53]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[53]]$version_group_details[[2]]$move_learn_method
## $moves[[53]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[53]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[53]]$version_group_details[[2]]$version_group
## $moves[[53]]$version_group_details[[2]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[53]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[53]]$version_group_details[[3]]
## $moves[[53]]$version_group_details[[3]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[3]]$move_learn_method
## $moves[[53]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[3]]$version_group
## $moves[[53]]$version_group_details[[3]]$version_group$name
## [1] "crystal"
## 
## $moves[[53]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[53]]$version_group_details[[4]]
## $moves[[53]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[53]]$version_group_details[[4]]$move_learn_method
## $moves[[53]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[53]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[53]]$version_group_details[[4]]$version_group
## $moves[[53]]$version_group_details[[4]]$version_group$name
## [1] "crystal"
## 
## $moves[[53]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[53]]$version_group_details[[5]]
## $moves[[53]]$version_group_details[[5]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[5]]$move_learn_method
## $moves[[53]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[5]]$version_group
## $moves[[53]]$version_group_details[[5]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[53]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[53]]$version_group_details[[6]]
## $moves[[53]]$version_group_details[[6]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[6]]$move_learn_method
## $moves[[53]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[6]]$version_group
## $moves[[53]]$version_group_details[[6]]$version_group$name
## [1] "emerald"
## 
## $moves[[53]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[53]]$version_group_details[[7]]
## $moves[[53]]$version_group_details[[7]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[7]]$move_learn_method
## $moves[[53]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[7]]$version_group
## $moves[[53]]$version_group_details[[7]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[53]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[53]]$version_group_details[[8]]
## $moves[[53]]$version_group_details[[8]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[8]]$move_learn_method
## $moves[[53]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[8]]$version_group
## $moves[[53]]$version_group_details[[8]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[53]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[53]]$version_group_details[[9]]
## $moves[[53]]$version_group_details[[9]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[9]]$move_learn_method
## $moves[[53]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[9]]$version_group
## $moves[[53]]$version_group_details[[9]]$version_group$name
## [1] "platinum"
## 
## $moves[[53]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[53]]$version_group_details[[10]]
## $moves[[53]]$version_group_details[[10]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[10]]$move_learn_method
## $moves[[53]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[10]]$version_group
## $moves[[53]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[53]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[53]]$version_group_details[[11]]
## $moves[[53]]$version_group_details[[11]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[11]]$move_learn_method
## $moves[[53]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[11]]$version_group
## $moves[[53]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[53]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[53]]$version_group_details[[12]]
## $moves[[53]]$version_group_details[[12]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[12]]$move_learn_method
## $moves[[53]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[12]]$version_group
## $moves[[53]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[53]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[53]]$version_group_details[[13]]
## $moves[[53]]$version_group_details[[13]]$level_learned_at
## [1] 25
## 
## $moves[[53]]$version_group_details[[13]]$move_learn_method
## $moves[[53]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[13]]$version_group
## $moves[[53]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[53]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[53]]$version_group_details[[14]]
## $moves[[53]]$version_group_details[[14]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[14]]$move_learn_method
## $moves[[53]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[14]]$version_group
## $moves[[53]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[53]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[53]]$version_group_details[[15]]
## $moves[[53]]$version_group_details[[15]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[15]]$move_learn_method
## $moves[[53]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[15]]$version_group
## $moves[[53]]$version_group_details[[15]]$version_group$name
## [1] "x-y"
## 
## $moves[[53]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[53]]$version_group_details[[16]]
## $moves[[53]]$version_group_details[[16]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[16]]$move_learn_method
## $moves[[53]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[16]]$version_group
## $moves[[53]]$version_group_details[[16]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[53]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[53]]$version_group_details[[17]]
## $moves[[53]]$version_group_details[[17]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[17]]$move_learn_method
## $moves[[53]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[17]]$version_group
## $moves[[53]]$version_group_details[[17]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[53]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[53]]$version_group_details[[18]]
## $moves[[53]]$version_group_details[[18]]$level_learned_at
## [1] 21
## 
## $moves[[53]]$version_group_details[[18]]$move_learn_method
## $moves[[53]]$version_group_details[[18]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[18]]$version_group
## $moves[[53]]$version_group_details[[18]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[53]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[53]]$version_group_details[[19]]
## $moves[[53]]$version_group_details[[19]]$level_learned_at
## [1] 24
## 
## $moves[[53]]$version_group_details[[19]]$move_learn_method
## $moves[[53]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[53]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[53]]$version_group_details[[19]]$version_group
## $moves[[53]]$version_group_details[[19]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[53]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[54]]
## $moves[[54]]$move
## $moves[[54]]$move$name
## [1] "synthesis"
## 
## $moves[[54]]$move$url
## [1] "https://pokeapi.co/api/v2/move/235/"
## 
## 
## $moves[[54]]$version_group_details
## $moves[[54]]$version_group_details[[1]]
## $moves[[54]]$version_group_details[[1]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[1]]$move_learn_method
## $moves[[54]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[1]]$version_group
## $moves[[54]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[54]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[54]]$version_group_details[[2]]
## $moves[[54]]$version_group_details[[2]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[2]]$move_learn_method
## $moves[[54]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[2]]$version_group
## $moves[[54]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[54]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[54]]$version_group_details[[3]]
## $moves[[54]]$version_group_details[[3]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[3]]$move_learn_method
## $moves[[54]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[3]]$version_group
## $moves[[54]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[54]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[54]]$version_group_details[[4]]
## $moves[[54]]$version_group_details[[4]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[4]]$move_learn_method
## $moves[[54]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[4]]$version_group
## $moves[[54]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[54]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[54]]$version_group_details[[5]]
## $moves[[54]]$version_group_details[[5]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[5]]$move_learn_method
## $moves[[54]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[5]]$version_group
## $moves[[54]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[54]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[54]]$version_group_details[[6]]
## $moves[[54]]$version_group_details[[6]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[6]]$move_learn_method
## $moves[[54]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[6]]$version_group
## $moves[[54]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[54]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[54]]$version_group_details[[7]]
## $moves[[54]]$version_group_details[[7]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[7]]$move_learn_method
## $moves[[54]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[7]]$version_group
## $moves[[54]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[54]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[54]]$version_group_details[[8]]
## $moves[[54]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[54]]$version_group_details[[8]]$move_learn_method
## $moves[[54]]$version_group_details[[8]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[54]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[54]]$version_group_details[[8]]$version_group
## $moves[[54]]$version_group_details[[8]]$version_group$name
## [1] "platinum"
## 
## $moves[[54]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[54]]$version_group_details[[9]]
## $moves[[54]]$version_group_details[[9]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[9]]$move_learn_method
## $moves[[54]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[9]]$version_group
## $moves[[54]]$version_group_details[[9]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[54]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[54]]$version_group_details[[10]]
## $moves[[54]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[54]]$version_group_details[[10]]$move_learn_method
## $moves[[54]]$version_group_details[[10]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[54]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[54]]$version_group_details[[10]]$version_group
## $moves[[54]]$version_group_details[[10]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[54]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[54]]$version_group_details[[11]]
## $moves[[54]]$version_group_details[[11]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[11]]$move_learn_method
## $moves[[54]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[11]]$version_group
## $moves[[54]]$version_group_details[[11]]$version_group$name
## [1] "black-white"
## 
## $moves[[54]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[54]]$version_group_details[[12]]
## $moves[[54]]$version_group_details[[12]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[12]]$move_learn_method
## $moves[[54]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[12]]$version_group
## $moves[[54]]$version_group_details[[12]]$version_group$name
## [1] "colosseum"
## 
## $moves[[54]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[54]]$version_group_details[[13]]
## $moves[[54]]$version_group_details[[13]]$level_learned_at
## [1] 39
## 
## $moves[[54]]$version_group_details[[13]]$move_learn_method
## $moves[[54]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[13]]$version_group
## $moves[[54]]$version_group_details[[13]]$version_group$name
## [1] "xd"
## 
## $moves[[54]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[54]]$version_group_details[[14]]
## $moves[[54]]$version_group_details[[14]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[14]]$move_learn_method
## $moves[[54]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[14]]$version_group
## $moves[[54]]$version_group_details[[14]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[54]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[54]]$version_group_details[[15]]
## $moves[[54]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[54]]$version_group_details[[15]]$move_learn_method
## $moves[[54]]$version_group_details[[15]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[54]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[54]]$version_group_details[[15]]$version_group
## $moves[[54]]$version_group_details[[15]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[54]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[54]]$version_group_details[[16]]
## $moves[[54]]$version_group_details[[16]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[16]]$move_learn_method
## $moves[[54]]$version_group_details[[16]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[16]]$version_group
## $moves[[54]]$version_group_details[[16]]$version_group$name
## [1] "x-y"
## 
## $moves[[54]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[54]]$version_group_details[[17]]
## $moves[[54]]$version_group_details[[17]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[17]]$move_learn_method
## $moves[[54]]$version_group_details[[17]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[17]]$version_group
## $moves[[54]]$version_group_details[[17]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[54]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[54]]$version_group_details[[18]]
## $moves[[54]]$version_group_details[[18]]$level_learned_at
## [1] 0
## 
## $moves[[54]]$version_group_details[[18]]$move_learn_method
## $moves[[54]]$version_group_details[[18]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[54]]$version_group_details[[18]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[54]]$version_group_details[[18]]$version_group
## $moves[[54]]$version_group_details[[18]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[54]]$version_group_details[[18]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[54]]$version_group_details[[19]]
## $moves[[54]]$version_group_details[[19]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[19]]$move_learn_method
## $moves[[54]]$version_group_details[[19]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[19]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[19]]$version_group
## $moves[[54]]$version_group_details[[19]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[54]]$version_group_details[[19]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[54]]$version_group_details[[20]]
## $moves[[54]]$version_group_details[[20]]$level_learned_at
## [1] 33
## 
## $moves[[54]]$version_group_details[[20]]$move_learn_method
## $moves[[54]]$version_group_details[[20]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[20]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[20]]$version_group
## $moves[[54]]$version_group_details[[20]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[54]]$version_group_details[[20]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[54]]$version_group_details[[21]]
## $moves[[54]]$version_group_details[[21]]$level_learned_at
## [1] 0
## 
## $moves[[54]]$version_group_details[[21]]$move_learn_method
## $moves[[54]]$version_group_details[[21]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[54]]$version_group_details[[21]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[54]]$version_group_details[[21]]$version_group
## $moves[[54]]$version_group_details[[21]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[54]]$version_group_details[[21]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[54]]$version_group_details[[22]]
## $moves[[54]]$version_group_details[[22]]$level_learned_at
## [1] 27
## 
## $moves[[54]]$version_group_details[[22]]$move_learn_method
## $moves[[54]]$version_group_details[[22]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[54]]$version_group_details[[22]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[54]]$version_group_details[[22]]$version_group
## $moves[[54]]$version_group_details[[22]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[54]]$version_group_details[[22]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[55]]
## $moves[[55]]$move
## $moves[[55]]$move$name
## [1] "hidden-power"
## 
## $moves[[55]]$move$url
## [1] "https://pokeapi.co/api/v2/move/237/"
## 
## 
## $moves[[55]]$version_group_details
## $moves[[55]]$version_group_details[[1]]
## $moves[[55]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[1]]$move_learn_method
## $moves[[55]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[1]]$version_group
## $moves[[55]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[55]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[55]]$version_group_details[[2]]
## $moves[[55]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[2]]$move_learn_method
## $moves[[55]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[2]]$version_group
## $moves[[55]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[55]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[55]]$version_group_details[[3]]
## $moves[[55]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[3]]$move_learn_method
## $moves[[55]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[3]]$version_group
## $moves[[55]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[55]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[55]]$version_group_details[[4]]
## $moves[[55]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[4]]$move_learn_method
## $moves[[55]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[4]]$version_group
## $moves[[55]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[55]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[55]]$version_group_details[[5]]
## $moves[[55]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[5]]$move_learn_method
## $moves[[55]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[5]]$version_group
## $moves[[55]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[55]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[55]]$version_group_details[[6]]
## $moves[[55]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[6]]$move_learn_method
## $moves[[55]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[6]]$version_group
## $moves[[55]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[55]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[55]]$version_group_details[[7]]
## $moves[[55]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[7]]$move_learn_method
## $moves[[55]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[7]]$version_group
## $moves[[55]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[55]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[55]]$version_group_details[[8]]
## $moves[[55]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[8]]$move_learn_method
## $moves[[55]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[8]]$version_group
## $moves[[55]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[55]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[55]]$version_group_details[[9]]
## $moves[[55]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[9]]$move_learn_method
## $moves[[55]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[9]]$version_group
## $moves[[55]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[55]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[55]]$version_group_details[[10]]
## $moves[[55]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[10]]$move_learn_method
## $moves[[55]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[10]]$version_group
## $moves[[55]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[55]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[55]]$version_group_details[[11]]
## $moves[[55]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[11]]$move_learn_method
## $moves[[55]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[11]]$version_group
## $moves[[55]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[55]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[55]]$version_group_details[[12]]
## $moves[[55]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[12]]$move_learn_method
## $moves[[55]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[12]]$version_group
## $moves[[55]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[55]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[55]]$version_group_details[[13]]
## $moves[[55]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[13]]$move_learn_method
## $moves[[55]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[13]]$version_group
## $moves[[55]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[55]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[55]]$version_group_details[[14]]
## $moves[[55]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[14]]$move_learn_method
## $moves[[55]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[14]]$version_group
## $moves[[55]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[55]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[55]]$version_group_details[[15]]
## $moves[[55]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[15]]$move_learn_method
## $moves[[55]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[15]]$version_group
## $moves[[55]]$version_group_details[[15]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[55]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[55]]$version_group_details[[16]]
## $moves[[55]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[55]]$version_group_details[[16]]$move_learn_method
## $moves[[55]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[55]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[55]]$version_group_details[[16]]$version_group
## $moves[[55]]$version_group_details[[16]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[55]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[56]]
## $moves[[56]]$move
## $moves[[56]]$move$name
## [1] "sunny-day"
## 
## $moves[[56]]$move$url
## [1] "https://pokeapi.co/api/v2/move/241/"
## 
## 
## $moves[[56]]$version_group_details
## $moves[[56]]$version_group_details[[1]]
## $moves[[56]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[1]]$move_learn_method
## $moves[[56]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[1]]$version_group
## $moves[[56]]$version_group_details[[1]]$version_group$name
## [1] "gold-silver"
## 
## $moves[[56]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/3/"
## 
## 
## 
## $moves[[56]]$version_group_details[[2]]
## $moves[[56]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[2]]$move_learn_method
## $moves[[56]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[2]]$version_group
## $moves[[56]]$version_group_details[[2]]$version_group$name
## [1] "crystal"
## 
## $moves[[56]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/4/"
## 
## 
## 
## $moves[[56]]$version_group_details[[3]]
## $moves[[56]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[3]]$move_learn_method
## $moves[[56]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[3]]$version_group
## $moves[[56]]$version_group_details[[3]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[56]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[56]]$version_group_details[[4]]
## $moves[[56]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[4]]$move_learn_method
## $moves[[56]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[4]]$version_group
## $moves[[56]]$version_group_details[[4]]$version_group$name
## [1] "emerald"
## 
## $moves[[56]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[56]]$version_group_details[[5]]
## $moves[[56]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[5]]$move_learn_method
## $moves[[56]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[5]]$version_group
## $moves[[56]]$version_group_details[[5]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[56]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[56]]$version_group_details[[6]]
## $moves[[56]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[6]]$move_learn_method
## $moves[[56]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[6]]$version_group
## $moves[[56]]$version_group_details[[6]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[56]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[56]]$version_group_details[[7]]
## $moves[[56]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[7]]$move_learn_method
## $moves[[56]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[7]]$version_group
## $moves[[56]]$version_group_details[[7]]$version_group$name
## [1] "platinum"
## 
## $moves[[56]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[56]]$version_group_details[[8]]
## $moves[[56]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[8]]$move_learn_method
## $moves[[56]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[8]]$version_group
## $moves[[56]]$version_group_details[[8]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[56]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[56]]$version_group_details[[9]]
## $moves[[56]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[9]]$move_learn_method
## $moves[[56]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[9]]$version_group
## $moves[[56]]$version_group_details[[9]]$version_group$name
## [1] "black-white"
## 
## $moves[[56]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[56]]$version_group_details[[10]]
## $moves[[56]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[10]]$move_learn_method
## $moves[[56]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[10]]$version_group
## $moves[[56]]$version_group_details[[10]]$version_group$name
## [1] "colosseum"
## 
## $moves[[56]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[56]]$version_group_details[[11]]
## $moves[[56]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[11]]$move_learn_method
## $moves[[56]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[11]]$version_group
## $moves[[56]]$version_group_details[[11]]$version_group$name
## [1] "xd"
## 
## $moves[[56]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[56]]$version_group_details[[12]]
## $moves[[56]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[12]]$move_learn_method
## $moves[[56]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[12]]$version_group
## $moves[[56]]$version_group_details[[12]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[56]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[56]]$version_group_details[[13]]
## $moves[[56]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[13]]$move_learn_method
## $moves[[56]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[13]]$version_group
## $moves[[56]]$version_group_details[[13]]$version_group$name
## [1] "x-y"
## 
## $moves[[56]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[56]]$version_group_details[[14]]
## $moves[[56]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[14]]$move_learn_method
## $moves[[56]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[14]]$version_group
## $moves[[56]]$version_group_details[[14]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[56]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[56]]$version_group_details[[15]]
## $moves[[56]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[15]]$move_learn_method
## $moves[[56]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[15]]$version_group
## $moves[[56]]$version_group_details[[15]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[56]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[56]]$version_group_details[[16]]
## $moves[[56]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[16]]$move_learn_method
## $moves[[56]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[16]]$version_group
## $moves[[56]]$version_group_details[[16]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[56]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[56]]$version_group_details[[17]]
## $moves[[56]]$version_group_details[[17]]$level_learned_at
## [1] 0
## 
## $moves[[56]]$version_group_details[[17]]$move_learn_method
## $moves[[56]]$version_group_details[[17]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[56]]$version_group_details[[17]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[56]]$version_group_details[[17]]$version_group
## $moves[[56]]$version_group_details[[17]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[56]]$version_group_details[[17]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[57]]
## $moves[[57]]$move
## $moves[[57]]$move$name
## [1] "rock-smash"
## 
## $moves[[57]]$move$url
## [1] "https://pokeapi.co/api/v2/move/249/"
## 
## 
## $moves[[57]]$version_group_details
## $moves[[57]]$version_group_details[[1]]
## $moves[[57]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[1]]$move_learn_method
## $moves[[57]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[1]]$version_group
## $moves[[57]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[57]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[57]]$version_group_details[[2]]
## $moves[[57]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[2]]$move_learn_method
## $moves[[57]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[2]]$version_group
## $moves[[57]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[57]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[57]]$version_group_details[[3]]
## $moves[[57]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[3]]$move_learn_method
## $moves[[57]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[3]]$version_group
## $moves[[57]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[57]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[57]]$version_group_details[[4]]
## $moves[[57]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[4]]$move_learn_method
## $moves[[57]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[4]]$version_group
## $moves[[57]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[57]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[57]]$version_group_details[[5]]
## $moves[[57]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[5]]$move_learn_method
## $moves[[57]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[5]]$version_group
## $moves[[57]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[57]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[57]]$version_group_details[[6]]
## $moves[[57]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[6]]$move_learn_method
## $moves[[57]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[6]]$version_group
## $moves[[57]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[57]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[57]]$version_group_details[[7]]
## $moves[[57]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[7]]$move_learn_method
## $moves[[57]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[7]]$version_group
## $moves[[57]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[57]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[57]]$version_group_details[[8]]
## $moves[[57]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[8]]$move_learn_method
## $moves[[57]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[8]]$version_group
## $moves[[57]]$version_group_details[[8]]$version_group$name
## [1] "colosseum"
## 
## $moves[[57]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[57]]$version_group_details[[9]]
## $moves[[57]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[9]]$move_learn_method
## $moves[[57]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[9]]$version_group
## $moves[[57]]$version_group_details[[9]]$version_group$name
## [1] "xd"
## 
## $moves[[57]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[57]]$version_group_details[[10]]
## $moves[[57]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[10]]$move_learn_method
## $moves[[57]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[10]]$version_group
## $moves[[57]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[57]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[57]]$version_group_details[[11]]
## $moves[[57]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[11]]$move_learn_method
## $moves[[57]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[11]]$version_group
## $moves[[57]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[57]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[57]]$version_group_details[[12]]
## $moves[[57]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[57]]$version_group_details[[12]]$move_learn_method
## $moves[[57]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[57]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[57]]$version_group_details[[12]]$version_group
## $moves[[57]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[57]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## 
## 
## $moves[[58]]
## $moves[[58]]$move
## $moves[[58]]$move$name
## [1] "facade"
## 
## $moves[[58]]$move$url
## [1] "https://pokeapi.co/api/v2/move/263/"
## 
## 
## $moves[[58]]$version_group_details
## $moves[[58]]$version_group_details[[1]]
## $moves[[58]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[1]]$move_learn_method
## $moves[[58]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[1]]$version_group
## $moves[[58]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[58]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[58]]$version_group_details[[2]]
## $moves[[58]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[2]]$move_learn_method
## $moves[[58]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[2]]$version_group
## $moves[[58]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[58]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[58]]$version_group_details[[3]]
## $moves[[58]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[3]]$move_learn_method
## $moves[[58]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[3]]$version_group
## $moves[[58]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[58]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[58]]$version_group_details[[4]]
## $moves[[58]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[4]]$move_learn_method
## $moves[[58]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[4]]$version_group
## $moves[[58]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[58]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[58]]$version_group_details[[5]]
## $moves[[58]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[5]]$move_learn_method
## $moves[[58]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[5]]$version_group
## $moves[[58]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[58]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[58]]$version_group_details[[6]]
## $moves[[58]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[6]]$move_learn_method
## $moves[[58]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[6]]$version_group
## $moves[[58]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[58]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[58]]$version_group_details[[7]]
## $moves[[58]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[7]]$move_learn_method
## $moves[[58]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[7]]$version_group
## $moves[[58]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[58]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[58]]$version_group_details[[8]]
## $moves[[58]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[8]]$move_learn_method
## $moves[[58]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[8]]$version_group
## $moves[[58]]$version_group_details[[8]]$version_group$name
## [1] "colosseum"
## 
## $moves[[58]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[58]]$version_group_details[[9]]
## $moves[[58]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[9]]$move_learn_method
## $moves[[58]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[9]]$version_group
## $moves[[58]]$version_group_details[[9]]$version_group$name
## [1] "xd"
## 
## $moves[[58]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[58]]$version_group_details[[10]]
## $moves[[58]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[10]]$move_learn_method
## $moves[[58]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[10]]$version_group
## $moves[[58]]$version_group_details[[10]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[58]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[58]]$version_group_details[[11]]
## $moves[[58]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[11]]$move_learn_method
## $moves[[58]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[11]]$version_group
## $moves[[58]]$version_group_details[[11]]$version_group$name
## [1] "x-y"
## 
## $moves[[58]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[58]]$version_group_details[[12]]
## $moves[[58]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[12]]$move_learn_method
## $moves[[58]]$version_group_details[[12]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[12]]$version_group
## $moves[[58]]$version_group_details[[12]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[58]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[58]]$version_group_details[[13]]
## $moves[[58]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[13]]$move_learn_method
## $moves[[58]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[13]]$version_group
## $moves[[58]]$version_group_details[[13]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[58]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[58]]$version_group_details[[14]]
## $moves[[58]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[14]]$move_learn_method
## $moves[[58]]$version_group_details[[14]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[14]]$version_group
## $moves[[58]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[58]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[58]]$version_group_details[[15]]
## $moves[[58]]$version_group_details[[15]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[15]]$move_learn_method
## $moves[[58]]$version_group_details[[15]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[15]]$version_group
## $moves[[58]]$version_group_details[[15]]$version_group$name
## [1] "lets-go-pikachu-lets-go-eevee"
## 
## $moves[[58]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/19/"
## 
## 
## 
## $moves[[58]]$version_group_details[[16]]
## $moves[[58]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[58]]$version_group_details[[16]]$move_learn_method
## $moves[[58]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[58]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[58]]$version_group_details[[16]]$version_group
## $moves[[58]]$version_group_details[[16]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[58]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[59]]
## $moves[[59]]$move
## $moves[[59]]$move$name
## [1] "nature-power"
## 
## $moves[[59]]$move$url
## [1] "https://pokeapi.co/api/v2/move/267/"
## 
## 
## $moves[[59]]$version_group_details
## $moves[[59]]$version_group_details[[1]]
## $moves[[59]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[1]]$move_learn_method
## $moves[[59]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[1]]$version_group
## $moves[[59]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[59]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[59]]$version_group_details[[2]]
## $moves[[59]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[2]]$move_learn_method
## $moves[[59]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[2]]$version_group
## $moves[[59]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[59]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[59]]$version_group_details[[3]]
## $moves[[59]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[3]]$move_learn_method
## $moves[[59]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[3]]$version_group
## $moves[[59]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[59]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[59]]$version_group_details[[4]]
## $moves[[59]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[4]]$move_learn_method
## $moves[[59]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[4]]$version_group
## $moves[[59]]$version_group_details[[4]]$version_group$name
## [1] "black-white"
## 
## $moves[[59]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[59]]$version_group_details[[5]]
## $moves[[59]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[5]]$move_learn_method
## $moves[[59]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[5]]$version_group
## $moves[[59]]$version_group_details[[5]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[59]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[59]]$version_group_details[[6]]
## $moves[[59]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[6]]$move_learn_method
## $moves[[59]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[6]]$version_group
## $moves[[59]]$version_group_details[[6]]$version_group$name
## [1] "x-y"
## 
## $moves[[59]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[59]]$version_group_details[[7]]
## $moves[[59]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[7]]$move_learn_method
## $moves[[59]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[59]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[59]]$version_group_details[[7]]$version_group
## $moves[[59]]$version_group_details[[7]]$version_group$name
## [1] "x-y"
## 
## $moves[[59]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[59]]$version_group_details[[8]]
## $moves[[59]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[8]]$move_learn_method
## $moves[[59]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[8]]$version_group
## $moves[[59]]$version_group_details[[8]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[59]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[59]]$version_group_details[[9]]
## $moves[[59]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[9]]$move_learn_method
## $moves[[59]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[59]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[59]]$version_group_details[[9]]$version_group
## $moves[[59]]$version_group_details[[9]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[59]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[59]]$version_group_details[[10]]
## $moves[[59]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[10]]$move_learn_method
## $moves[[59]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[10]]$version_group
## $moves[[59]]$version_group_details[[10]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[59]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[59]]$version_group_details[[11]]
## $moves[[59]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[11]]$move_learn_method
## $moves[[59]]$version_group_details[[11]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[59]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[59]]$version_group_details[[11]]$version_group
## $moves[[59]]$version_group_details[[11]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[59]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[59]]$version_group_details[[12]]
## $moves[[59]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[12]]$move_learn_method
## $moves[[59]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[12]]$version_group
## $moves[[59]]$version_group_details[[12]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[59]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[59]]$version_group_details[[13]]
## $moves[[59]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[13]]$move_learn_method
## $moves[[59]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[59]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[59]]$version_group_details[[13]]$version_group
## $moves[[59]]$version_group_details[[13]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[59]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[59]]$version_group_details[[14]]
## $moves[[59]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[59]]$version_group_details[[14]]$move_learn_method
## $moves[[59]]$version_group_details[[14]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[59]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[59]]$version_group_details[[14]]$version_group
## $moves[[59]]$version_group_details[[14]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[59]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[60]]
## $moves[[60]]$move
## $moves[[60]]$move$name
## [1] "helping-hand"
## 
## $moves[[60]]$move$url
## [1] "https://pokeapi.co/api/v2/move/270/"
## 
## 
## $moves[[60]]$version_group_details
## $moves[[60]]$version_group_details[[1]]
## $moves[[60]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[60]]$version_group_details[[1]]$move_learn_method
## $moves[[60]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[60]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[60]]$version_group_details[[1]]$version_group
## $moves[[60]]$version_group_details[[1]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[60]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[61]]
## $moves[[61]]$move
## $moves[[61]]$move$name
## [1] "ingrain"
## 
## $moves[[61]]$move$url
## [1] "https://pokeapi.co/api/v2/move/275/"
## 
## 
## $moves[[61]]$version_group_details
## $moves[[61]]$version_group_details[[1]]
## $moves[[61]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[1]]$move_learn_method
## $moves[[61]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[1]]$version_group
## $moves[[61]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[61]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[61]]$version_group_details[[2]]
## $moves[[61]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[2]]$move_learn_method
## $moves[[61]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[2]]$version_group
## $moves[[61]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[61]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[61]]$version_group_details[[3]]
## $moves[[61]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[3]]$move_learn_method
## $moves[[61]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[3]]$version_group
## $moves[[61]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[61]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[61]]$version_group_details[[4]]
## $moves[[61]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[4]]$move_learn_method
## $moves[[61]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[4]]$version_group
## $moves[[61]]$version_group_details[[4]]$version_group$name
## [1] "black-white"
## 
## $moves[[61]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[61]]$version_group_details[[5]]
## $moves[[61]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[5]]$move_learn_method
## $moves[[61]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[5]]$version_group
## $moves[[61]]$version_group_details[[5]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[61]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[61]]$version_group_details[[6]]
## $moves[[61]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[6]]$move_learn_method
## $moves[[61]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[6]]$version_group
## $moves[[61]]$version_group_details[[6]]$version_group$name
## [1] "x-y"
## 
## $moves[[61]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[61]]$version_group_details[[7]]
## $moves[[61]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[7]]$move_learn_method
## $moves[[61]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[7]]$version_group
## $moves[[61]]$version_group_details[[7]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[61]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[61]]$version_group_details[[8]]
## $moves[[61]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[8]]$move_learn_method
## $moves[[61]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[8]]$version_group
## $moves[[61]]$version_group_details[[8]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[61]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[61]]$version_group_details[[9]]
## $moves[[61]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[9]]$move_learn_method
## $moves[[61]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[9]]$version_group
## $moves[[61]]$version_group_details[[9]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[61]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[61]]$version_group_details[[10]]
## $moves[[61]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[61]]$version_group_details[[10]]$move_learn_method
## $moves[[61]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[61]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[61]]$version_group_details[[10]]$version_group
## $moves[[61]]$version_group_details[[10]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[61]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[62]]
## $moves[[62]]$move
## $moves[[62]]$move$name
## [1] "knock-off"
## 
## $moves[[62]]$move$url
## [1] "https://pokeapi.co/api/v2/move/282/"
## 
## 
## $moves[[62]]$version_group_details
## $moves[[62]]$version_group_details[[1]]
## $moves[[62]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[62]]$version_group_details[[1]]$move_learn_method
## $moves[[62]]$version_group_details[[1]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[62]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[62]]$version_group_details[[1]]$version_group
## $moves[[62]]$version_group_details[[1]]$version_group$name
## [1] "platinum"
## 
## $moves[[62]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[62]]$version_group_details[[2]]
## $moves[[62]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[62]]$version_group_details[[2]]$move_learn_method
## $moves[[62]]$version_group_details[[2]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[62]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[62]]$version_group_details[[2]]$version_group
## $moves[[62]]$version_group_details[[2]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[62]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[62]]$version_group_details[[3]]
## $moves[[62]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[62]]$version_group_details[[3]]$move_learn_method
## $moves[[62]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[62]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[62]]$version_group_details[[3]]$version_group
## $moves[[62]]$version_group_details[[3]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[62]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[62]]$version_group_details[[4]]
## $moves[[62]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[62]]$version_group_details[[4]]$move_learn_method
## $moves[[62]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[62]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[62]]$version_group_details[[4]]$version_group
## $moves[[62]]$version_group_details[[4]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[62]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[62]]$version_group_details[[5]]
## $moves[[62]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[62]]$version_group_details[[5]]$move_learn_method
## $moves[[62]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[62]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[62]]$version_group_details[[5]]$version_group
## $moves[[62]]$version_group_details[[5]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[62]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[63]]
## $moves[[63]]$move
## $moves[[63]]$move$name
## [1] "secret-power"
## 
## $moves[[63]]$move$url
## [1] "https://pokeapi.co/api/v2/move/290/"
## 
## 
## $moves[[63]]$version_group_details
## $moves[[63]]$version_group_details[[1]]
## $moves[[63]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[1]]$move_learn_method
## $moves[[63]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[1]]$version_group
## $moves[[63]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[63]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[63]]$version_group_details[[2]]
## $moves[[63]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[2]]$move_learn_method
## $moves[[63]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[2]]$version_group
## $moves[[63]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[63]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[63]]$version_group_details[[3]]
## $moves[[63]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[3]]$move_learn_method
## $moves[[63]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[3]]$version_group
## $moves[[63]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[63]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[63]]$version_group_details[[4]]
## $moves[[63]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[4]]$move_learn_method
## $moves[[63]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[4]]$version_group
## $moves[[63]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[63]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[63]]$version_group_details[[5]]
## $moves[[63]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[5]]$move_learn_method
## $moves[[63]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[5]]$version_group
## $moves[[63]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[63]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[63]]$version_group_details[[6]]
## $moves[[63]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[6]]$move_learn_method
## $moves[[63]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[6]]$version_group
## $moves[[63]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[63]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[63]]$version_group_details[[7]]
## $moves[[63]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[7]]$move_learn_method
## $moves[[63]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[7]]$version_group
## $moves[[63]]$version_group_details[[7]]$version_group$name
## [1] "colosseum"
## 
## $moves[[63]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[63]]$version_group_details[[8]]
## $moves[[63]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[8]]$move_learn_method
## $moves[[63]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[8]]$version_group
## $moves[[63]]$version_group_details[[8]]$version_group$name
## [1] "xd"
## 
## $moves[[63]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[63]]$version_group_details[[9]]
## $moves[[63]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[63]]$version_group_details[[9]]$move_learn_method
## $moves[[63]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[63]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[63]]$version_group_details[[9]]$version_group
## $moves[[63]]$version_group_details[[9]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[63]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## 
## 
## $moves[[64]]
## $moves[[64]]$move
## $moves[[64]]$move$name
## [1] "weather-ball"
## 
## $moves[[64]]$move$url
## [1] "https://pokeapi.co/api/v2/move/311/"
## 
## 
## $moves[[64]]$version_group_details
## $moves[[64]]$version_group_details[[1]]
## $moves[[64]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[64]]$version_group_details[[1]]$move_learn_method
## $moves[[64]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[64]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[64]]$version_group_details[[1]]$version_group
## $moves[[64]]$version_group_details[[1]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[64]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[65]]
## $moves[[65]]$move
## $moves[[65]]$move$name
## [1] "grass-whistle"
## 
## $moves[[65]]$move$url
## [1] "https://pokeapi.co/api/v2/move/320/"
## 
## 
## $moves[[65]]$version_group_details
## $moves[[65]]$version_group_details[[1]]
## $moves[[65]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[1]]$move_learn_method
## $moves[[65]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[1]]$version_group
## $moves[[65]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[65]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[65]]$version_group_details[[2]]
## $moves[[65]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[2]]$move_learn_method
## $moves[[65]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[2]]$version_group
## $moves[[65]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[65]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[65]]$version_group_details[[3]]
## $moves[[65]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[3]]$move_learn_method
## $moves[[65]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[3]]$version_group
## $moves[[65]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[65]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[65]]$version_group_details[[4]]
## $moves[[65]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[4]]$move_learn_method
## $moves[[65]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[4]]$version_group
## $moves[[65]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[65]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[65]]$version_group_details[[5]]
## $moves[[65]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[5]]$move_learn_method
## $moves[[65]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[5]]$version_group
## $moves[[65]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[65]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[65]]$version_group_details[[6]]
## $moves[[65]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[6]]$move_learn_method
## $moves[[65]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[6]]$version_group
## $moves[[65]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[65]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[65]]$version_group_details[[7]]
## $moves[[65]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[7]]$move_learn_method
## $moves[[65]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[7]]$version_group
## $moves[[65]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[65]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[65]]$version_group_details[[8]]
## $moves[[65]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[8]]$move_learn_method
## $moves[[65]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[8]]$version_group
## $moves[[65]]$version_group_details[[8]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[65]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[65]]$version_group_details[[9]]
## $moves[[65]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[9]]$move_learn_method
## $moves[[65]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[9]]$version_group
## $moves[[65]]$version_group_details[[9]]$version_group$name
## [1] "x-y"
## 
## $moves[[65]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[65]]$version_group_details[[10]]
## $moves[[65]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[10]]$move_learn_method
## $moves[[65]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[10]]$version_group
## $moves[[65]]$version_group_details[[10]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[65]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[65]]$version_group_details[[11]]
## $moves[[65]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[11]]$move_learn_method
## $moves[[65]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[11]]$version_group
## $moves[[65]]$version_group_details[[11]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[65]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[65]]$version_group_details[[12]]
## $moves[[65]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[65]]$version_group_details[[12]]$move_learn_method
## $moves[[65]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[65]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[65]]$version_group_details[[12]]$version_group
## $moves[[65]]$version_group_details[[12]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[65]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[66]]
## $moves[[66]]$move
## $moves[[66]]$move$name
## [1] "bullet-seed"
## 
## $moves[[66]]$move$url
## [1] "https://pokeapi.co/api/v2/move/331/"
## 
## 
## $moves[[66]]$version_group_details
## $moves[[66]]$version_group_details[[1]]
## $moves[[66]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[1]]$move_learn_method
## $moves[[66]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[1]]$version_group
## $moves[[66]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[66]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[66]]$version_group_details[[2]]
## $moves[[66]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[2]]$move_learn_method
## $moves[[66]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[2]]$version_group
## $moves[[66]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[66]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[66]]$version_group_details[[3]]
## $moves[[66]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[3]]$move_learn_method
## $moves[[66]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[3]]$version_group
## $moves[[66]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[66]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[66]]$version_group_details[[4]]
## $moves[[66]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[4]]$move_learn_method
## $moves[[66]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[4]]$version_group
## $moves[[66]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[66]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[66]]$version_group_details[[5]]
## $moves[[66]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[5]]$move_learn_method
## $moves[[66]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[5]]$version_group
## $moves[[66]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[66]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[66]]$version_group_details[[6]]
## $moves[[66]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[6]]$move_learn_method
## $moves[[66]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[6]]$version_group
## $moves[[66]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[66]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[66]]$version_group_details[[7]]
## $moves[[66]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[7]]$move_learn_method
## $moves[[66]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[7]]$version_group
## $moves[[66]]$version_group_details[[7]]$version_group$name
## [1] "colosseum"
## 
## $moves[[66]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/12/"
## 
## 
## 
## $moves[[66]]$version_group_details[[8]]
## $moves[[66]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[8]]$move_learn_method
## $moves[[66]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[8]]$version_group
## $moves[[66]]$version_group_details[[8]]$version_group$name
## [1] "xd"
## 
## $moves[[66]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/13/"
## 
## 
## 
## $moves[[66]]$version_group_details[[9]]
## $moves[[66]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[66]]$version_group_details[[9]]$move_learn_method
## $moves[[66]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[66]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[66]]$version_group_details[[9]]$version_group
## $moves[[66]]$version_group_details[[9]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[66]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[67]]
## $moves[[67]]$move
## $moves[[67]]$move$name
## [1] "magical-leaf"
## 
## $moves[[67]]$move$url
## [1] "https://pokeapi.co/api/v2/move/345/"
## 
## 
## $moves[[67]]$version_group_details
## $moves[[67]]$version_group_details[[1]]
## $moves[[67]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[1]]$move_learn_method
## $moves[[67]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[1]]$version_group
## $moves[[67]]$version_group_details[[1]]$version_group$name
## [1] "ruby-sapphire"
## 
## $moves[[67]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/5/"
## 
## 
## 
## $moves[[67]]$version_group_details[[2]]
## $moves[[67]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[2]]$move_learn_method
## $moves[[67]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[2]]$version_group
## $moves[[67]]$version_group_details[[2]]$version_group$name
## [1] "emerald"
## 
## $moves[[67]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/6/"
## 
## 
## 
## $moves[[67]]$version_group_details[[3]]
## $moves[[67]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[3]]$move_learn_method
## $moves[[67]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[3]]$version_group
## $moves[[67]]$version_group_details[[3]]$version_group$name
## [1] "firered-leafgreen"
## 
## $moves[[67]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/7/"
## 
## 
## 
## $moves[[67]]$version_group_details[[4]]
## $moves[[67]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[4]]$move_learn_method
## $moves[[67]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[4]]$version_group
## $moves[[67]]$version_group_details[[4]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[67]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[67]]$version_group_details[[5]]
## $moves[[67]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[5]]$move_learn_method
## $moves[[67]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[5]]$version_group
## $moves[[67]]$version_group_details[[5]]$version_group$name
## [1] "platinum"
## 
## $moves[[67]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[67]]$version_group_details[[6]]
## $moves[[67]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[6]]$move_learn_method
## $moves[[67]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[6]]$version_group
## $moves[[67]]$version_group_details[[6]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[67]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[67]]$version_group_details[[7]]
## $moves[[67]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[7]]$move_learn_method
## $moves[[67]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[7]]$version_group
## $moves[[67]]$version_group_details[[7]]$version_group$name
## [1] "black-white"
## 
## $moves[[67]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[67]]$version_group_details[[8]]
## $moves[[67]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[8]]$move_learn_method
## $moves[[67]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[8]]$version_group
## $moves[[67]]$version_group_details[[8]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[67]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[67]]$version_group_details[[9]]
## $moves[[67]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[9]]$move_learn_method
## $moves[[67]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[9]]$version_group
## $moves[[67]]$version_group_details[[9]]$version_group$name
## [1] "x-y"
## 
## $moves[[67]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[67]]$version_group_details[[10]]
## $moves[[67]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[10]]$move_learn_method
## $moves[[67]]$version_group_details[[10]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[10]]$version_group
## $moves[[67]]$version_group_details[[10]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[67]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[67]]$version_group_details[[11]]
## $moves[[67]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[11]]$move_learn_method
## $moves[[67]]$version_group_details[[11]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[11]]$version_group
## $moves[[67]]$version_group_details[[11]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[67]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[67]]$version_group_details[[12]]
## $moves[[67]]$version_group_details[[12]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[12]]$move_learn_method
## $moves[[67]]$version_group_details[[12]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[67]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[67]]$version_group_details[[12]]$version_group
## $moves[[67]]$version_group_details[[12]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[67]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[67]]$version_group_details[[13]]
## $moves[[67]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[67]]$version_group_details[[13]]$move_learn_method
## $moves[[67]]$version_group_details[[13]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[67]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[67]]$version_group_details[[13]]$version_group
## $moves[[67]]$version_group_details[[13]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[67]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[68]]
## $moves[[68]]$move
## $moves[[68]]$move$name
## [1] "natural-gift"
## 
## $moves[[68]]$move$url
## [1] "https://pokeapi.co/api/v2/move/363/"
## 
## 
## $moves[[68]]$version_group_details
## $moves[[68]]$version_group_details[[1]]
## $moves[[68]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[68]]$version_group_details[[1]]$move_learn_method
## $moves[[68]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[68]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[68]]$version_group_details[[1]]$version_group
## $moves[[68]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[68]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[68]]$version_group_details[[2]]
## $moves[[68]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[68]]$version_group_details[[2]]$move_learn_method
## $moves[[68]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[68]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[68]]$version_group_details[[2]]$version_group
## $moves[[68]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[68]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[68]]$version_group_details[[3]]
## $moves[[68]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[68]]$version_group_details[[3]]$move_learn_method
## $moves[[68]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[68]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[68]]$version_group_details[[3]]$version_group
## $moves[[68]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[68]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## 
## 
## $moves[[69]]
## $moves[[69]]$move
## $moves[[69]]$move$name
## [1] "worry-seed"
## 
## $moves[[69]]$move$url
## [1] "https://pokeapi.co/api/v2/move/388/"
## 
## 
## $moves[[69]]$version_group_details
## $moves[[69]]$version_group_details[[1]]
## $moves[[69]]$version_group_details[[1]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[1]]$move_learn_method
## $moves[[69]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[1]]$version_group
## $moves[[69]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[69]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[69]]$version_group_details[[2]]
## $moves[[69]]$version_group_details[[2]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[2]]$move_learn_method
## $moves[[69]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[2]]$version_group
## $moves[[69]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[69]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[69]]$version_group_details[[3]]
## $moves[[69]]$version_group_details[[3]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[3]]$move_learn_method
## $moves[[69]]$version_group_details[[3]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[3]]$version_group
## $moves[[69]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[69]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[69]]$version_group_details[[4]]
## $moves[[69]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[69]]$version_group_details[[4]]$move_learn_method
## $moves[[69]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[69]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[69]]$version_group_details[[4]]$version_group
## $moves[[69]]$version_group_details[[4]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[69]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[69]]$version_group_details[[5]]
## $moves[[69]]$version_group_details[[5]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[5]]$move_learn_method
## $moves[[69]]$version_group_details[[5]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[5]]$version_group
## $moves[[69]]$version_group_details[[5]]$version_group$name
## [1] "black-white"
## 
## $moves[[69]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[69]]$version_group_details[[6]]
## $moves[[69]]$version_group_details[[6]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[6]]$move_learn_method
## $moves[[69]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[6]]$version_group
## $moves[[69]]$version_group_details[[6]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[69]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[69]]$version_group_details[[7]]
## $moves[[69]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[69]]$version_group_details[[7]]$move_learn_method
## $moves[[69]]$version_group_details[[7]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[69]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[69]]$version_group_details[[7]]$version_group
## $moves[[69]]$version_group_details[[7]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[69]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[69]]$version_group_details[[8]]
## $moves[[69]]$version_group_details[[8]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[8]]$move_learn_method
## $moves[[69]]$version_group_details[[8]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[8]]$version_group
## $moves[[69]]$version_group_details[[8]]$version_group$name
## [1] "x-y"
## 
## $moves[[69]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[69]]$version_group_details[[9]]
## $moves[[69]]$version_group_details[[9]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[9]]$move_learn_method
## $moves[[69]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[9]]$version_group
## $moves[[69]]$version_group_details[[9]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[69]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[69]]$version_group_details[[10]]
## $moves[[69]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[69]]$version_group_details[[10]]$move_learn_method
## $moves[[69]]$version_group_details[[10]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[69]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[69]]$version_group_details[[10]]$version_group
## $moves[[69]]$version_group_details[[10]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[69]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[69]]$version_group_details[[11]]
## $moves[[69]]$version_group_details[[11]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[11]]$move_learn_method
## $moves[[69]]$version_group_details[[11]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[11]]$version_group
## $moves[[69]]$version_group_details[[11]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[69]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[69]]$version_group_details[[12]]
## $moves[[69]]$version_group_details[[12]]$level_learned_at
## [1] 31
## 
## $moves[[69]]$version_group_details[[12]]$move_learn_method
## $moves[[69]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[12]]$version_group
## $moves[[69]]$version_group_details[[12]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[69]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[69]]$version_group_details[[13]]
## $moves[[69]]$version_group_details[[13]]$level_learned_at
## [1] 0
## 
## $moves[[69]]$version_group_details[[13]]$move_learn_method
## $moves[[69]]$version_group_details[[13]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[69]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[69]]$version_group_details[[13]]$version_group
## $moves[[69]]$version_group_details[[13]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[69]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[69]]$version_group_details[[14]]
## $moves[[69]]$version_group_details[[14]]$level_learned_at
## [1] 30
## 
## $moves[[69]]$version_group_details[[14]]$move_learn_method
## $moves[[69]]$version_group_details[[14]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[69]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[69]]$version_group_details[[14]]$version_group
## $moves[[69]]$version_group_details[[14]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[69]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[70]]
## $moves[[70]]$move
## $moves[[70]]$move$name
## [1] "seed-bomb"
## 
## $moves[[70]]$move$url
## [1] "https://pokeapi.co/api/v2/move/402/"
## 
## 
## $moves[[70]]$version_group_details
## $moves[[70]]$version_group_details[[1]]
## $moves[[70]]$version_group_details[[1]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[1]]$move_learn_method
## $moves[[70]]$version_group_details[[1]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[1]]$version_group
## $moves[[70]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[70]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[70]]$version_group_details[[2]]
## $moves[[70]]$version_group_details[[2]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[2]]$move_learn_method
## $moves[[70]]$version_group_details[[2]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[2]]$version_group
## $moves[[70]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[70]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[70]]$version_group_details[[3]]
## $moves[[70]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[70]]$version_group_details[[3]]$move_learn_method
## $moves[[70]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[70]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[70]]$version_group_details[[3]]$version_group
## $moves[[70]]$version_group_details[[3]]$version_group$name
## [1] "platinum"
## 
## $moves[[70]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[70]]$version_group_details[[4]]
## $moves[[70]]$version_group_details[[4]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[4]]$move_learn_method
## $moves[[70]]$version_group_details[[4]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[4]]$version_group
## $moves[[70]]$version_group_details[[4]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[70]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[70]]$version_group_details[[5]]
## $moves[[70]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[70]]$version_group_details[[5]]$move_learn_method
## $moves[[70]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[70]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[70]]$version_group_details[[5]]$version_group
## $moves[[70]]$version_group_details[[5]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[70]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[70]]$version_group_details[[6]]
## $moves[[70]]$version_group_details[[6]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[6]]$move_learn_method
## $moves[[70]]$version_group_details[[6]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[6]]$version_group
## $moves[[70]]$version_group_details[[6]]$version_group$name
## [1] "black-white"
## 
## $moves[[70]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[70]]$version_group_details[[7]]
## $moves[[70]]$version_group_details[[7]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[7]]$move_learn_method
## $moves[[70]]$version_group_details[[7]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[7]]$version_group
## $moves[[70]]$version_group_details[[7]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[70]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[70]]$version_group_details[[8]]
## $moves[[70]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[70]]$version_group_details[[8]]$move_learn_method
## $moves[[70]]$version_group_details[[8]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[70]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[70]]$version_group_details[[8]]$version_group
## $moves[[70]]$version_group_details[[8]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[70]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[70]]$version_group_details[[9]]
## $moves[[70]]$version_group_details[[9]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[9]]$move_learn_method
## $moves[[70]]$version_group_details[[9]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[9]]$version_group
## $moves[[70]]$version_group_details[[9]]$version_group$name
## [1] "x-y"
## 
## $moves[[70]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[70]]$version_group_details[[10]]
## $moves[[70]]$version_group_details[[10]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[10]]$move_learn_method
## $moves[[70]]$version_group_details[[10]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[10]]$version_group
## $moves[[70]]$version_group_details[[10]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[70]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[70]]$version_group_details[[11]]
## $moves[[70]]$version_group_details[[11]]$level_learned_at
## [1] 0
## 
## $moves[[70]]$version_group_details[[11]]$move_learn_method
## $moves[[70]]$version_group_details[[11]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[70]]$version_group_details[[11]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[70]]$version_group_details[[11]]$version_group
## $moves[[70]]$version_group_details[[11]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[70]]$version_group_details[[11]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[70]]$version_group_details[[12]]
## $moves[[70]]$version_group_details[[12]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[12]]$move_learn_method
## $moves[[70]]$version_group_details[[12]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[12]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[12]]$version_group
## $moves[[70]]$version_group_details[[12]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[70]]$version_group_details[[12]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[70]]$version_group_details[[13]]
## $moves[[70]]$version_group_details[[13]]$level_learned_at
## [1] 37
## 
## $moves[[70]]$version_group_details[[13]]$move_learn_method
## $moves[[70]]$version_group_details[[13]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[13]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[13]]$version_group
## $moves[[70]]$version_group_details[[13]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[70]]$version_group_details[[13]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[70]]$version_group_details[[14]]
## $moves[[70]]$version_group_details[[14]]$level_learned_at
## [1] 0
## 
## $moves[[70]]$version_group_details[[14]]$move_learn_method
## $moves[[70]]$version_group_details[[14]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[70]]$version_group_details[[14]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[70]]$version_group_details[[14]]$version_group
## $moves[[70]]$version_group_details[[14]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[70]]$version_group_details[[14]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[70]]$version_group_details[[15]]
## $moves[[70]]$version_group_details[[15]]$level_learned_at
## [1] 18
## 
## $moves[[70]]$version_group_details[[15]]$move_learn_method
## $moves[[70]]$version_group_details[[15]]$move_learn_method$name
## [1] "level-up"
## 
## $moves[[70]]$version_group_details[[15]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/1/"
## 
## 
## $moves[[70]]$version_group_details[[15]]$version_group
## $moves[[70]]$version_group_details[[15]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[70]]$version_group_details[[15]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## $moves[[70]]$version_group_details[[16]]
## $moves[[70]]$version_group_details[[16]]$level_learned_at
## [1] 0
## 
## $moves[[70]]$version_group_details[[16]]$move_learn_method
## $moves[[70]]$version_group_details[[16]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[70]]$version_group_details[[16]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[70]]$version_group_details[[16]]$version_group
## $moves[[70]]$version_group_details[[16]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[70]]$version_group_details[[16]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[71]]
## $moves[[71]]$move
## $moves[[71]]$move$name
## [1] "energy-ball"
## 
## $moves[[71]]$move$url
## [1] "https://pokeapi.co/api/v2/move/412/"
## 
## 
## $moves[[71]]$version_group_details
## $moves[[71]]$version_group_details[[1]]
## $moves[[71]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[1]]$move_learn_method
## $moves[[71]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[1]]$version_group
## $moves[[71]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[71]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[71]]$version_group_details[[2]]
## $moves[[71]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[2]]$move_learn_method
## $moves[[71]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[2]]$version_group
## $moves[[71]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[71]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[71]]$version_group_details[[3]]
## $moves[[71]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[3]]$move_learn_method
## $moves[[71]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[3]]$version_group
## $moves[[71]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[71]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[71]]$version_group_details[[4]]
## $moves[[71]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[4]]$move_learn_method
## $moves[[71]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[4]]$version_group
## $moves[[71]]$version_group_details[[4]]$version_group$name
## [1] "black-white"
## 
## $moves[[71]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[71]]$version_group_details[[5]]
## $moves[[71]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[5]]$move_learn_method
## $moves[[71]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[5]]$version_group
## $moves[[71]]$version_group_details[[5]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[71]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[71]]$version_group_details[[6]]
## $moves[[71]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[6]]$move_learn_method
## $moves[[71]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[6]]$version_group
## $moves[[71]]$version_group_details[[6]]$version_group$name
## [1] "x-y"
## 
## $moves[[71]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[71]]$version_group_details[[7]]
## $moves[[71]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[7]]$move_learn_method
## $moves[[71]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[7]]$version_group
## $moves[[71]]$version_group_details[[7]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[71]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[71]]$version_group_details[[8]]
## $moves[[71]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[8]]$move_learn_method
## $moves[[71]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[8]]$version_group
## $moves[[71]]$version_group_details[[8]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[71]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[71]]$version_group_details[[9]]
## $moves[[71]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[9]]$move_learn_method
## $moves[[71]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[9]]$version_group
## $moves[[71]]$version_group_details[[9]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[71]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[71]]$version_group_details[[10]]
## $moves[[71]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[71]]$version_group_details[[10]]$move_learn_method
## $moves[[71]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[71]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[71]]$version_group_details[[10]]$version_group
## $moves[[71]]$version_group_details[[10]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[71]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[72]]
## $moves[[72]]$move
## $moves[[72]]$move$name
## [1] "leaf-storm"
## 
## $moves[[72]]$move$url
## [1] "https://pokeapi.co/api/v2/move/437/"
## 
## 
## $moves[[72]]$version_group_details
## $moves[[72]]$version_group_details[[1]]
## $moves[[72]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[1]]$move_learn_method
## $moves[[72]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[1]]$version_group
## $moves[[72]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[72]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[72]]$version_group_details[[2]]
## $moves[[72]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[2]]$move_learn_method
## $moves[[72]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[2]]$version_group
## $moves[[72]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[72]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[72]]$version_group_details[[3]]
## $moves[[72]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[3]]$move_learn_method
## $moves[[72]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[3]]$version_group
## $moves[[72]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[72]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[72]]$version_group_details[[4]]
## $moves[[72]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[4]]$move_learn_method
## $moves[[72]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[4]]$version_group
## $moves[[72]]$version_group_details[[4]]$version_group$name
## [1] "black-white"
## 
## $moves[[72]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[72]]$version_group_details[[5]]
## $moves[[72]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[5]]$move_learn_method
## $moves[[72]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[5]]$version_group
## $moves[[72]]$version_group_details[[5]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[72]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[72]]$version_group_details[[6]]
## $moves[[72]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[6]]$move_learn_method
## $moves[[72]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[6]]$version_group
## $moves[[72]]$version_group_details[[6]]$version_group$name
## [1] "x-y"
## 
## $moves[[72]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[72]]$version_group_details[[7]]
## $moves[[72]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[7]]$move_learn_method
## $moves[[72]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[7]]$version_group
## $moves[[72]]$version_group_details[[7]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[72]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[72]]$version_group_details[[8]]
## $moves[[72]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[8]]$move_learn_method
## $moves[[72]]$version_group_details[[8]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[8]]$version_group
## $moves[[72]]$version_group_details[[8]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[72]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[72]]$version_group_details[[9]]
## $moves[[72]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[9]]$move_learn_method
## $moves[[72]]$version_group_details[[9]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[72]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[72]]$version_group_details[[9]]$version_group
## $moves[[72]]$version_group_details[[9]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[72]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[72]]$version_group_details[[10]]
## $moves[[72]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[72]]$version_group_details[[10]]$move_learn_method
## $moves[[72]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[72]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[72]]$version_group_details[[10]]$version_group
## $moves[[72]]$version_group_details[[10]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[72]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[73]]
## $moves[[73]]$move
## $moves[[73]]$move$name
## [1] "power-whip"
## 
## $moves[[73]]$move$url
## [1] "https://pokeapi.co/api/v2/move/438/"
## 
## 
## $moves[[73]]$version_group_details
## $moves[[73]]$version_group_details[[1]]
## $moves[[73]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[1]]$move_learn_method
## $moves[[73]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[1]]$version_group
## $moves[[73]]$version_group_details[[1]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[73]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[73]]$version_group_details[[2]]
## $moves[[73]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[2]]$move_learn_method
## $moves[[73]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[2]]$version_group
## $moves[[73]]$version_group_details[[2]]$version_group$name
## [1] "black-white"
## 
## $moves[[73]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[73]]$version_group_details[[3]]
## $moves[[73]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[3]]$move_learn_method
## $moves[[73]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[3]]$version_group
## $moves[[73]]$version_group_details[[3]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[73]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[73]]$version_group_details[[4]]
## $moves[[73]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[4]]$move_learn_method
## $moves[[73]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[4]]$version_group
## $moves[[73]]$version_group_details[[4]]$version_group$name
## [1] "x-y"
## 
## $moves[[73]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[73]]$version_group_details[[5]]
## $moves[[73]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[5]]$move_learn_method
## $moves[[73]]$version_group_details[[5]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[5]]$version_group
## $moves[[73]]$version_group_details[[5]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[73]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[73]]$version_group_details[[6]]
## $moves[[73]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[6]]$move_learn_method
## $moves[[73]]$version_group_details[[6]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[6]]$version_group
## $moves[[73]]$version_group_details[[6]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[73]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[73]]$version_group_details[[7]]
## $moves[[73]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[7]]$move_learn_method
## $moves[[73]]$version_group_details[[7]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[73]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[73]]$version_group_details[[7]]$version_group
## $moves[[73]]$version_group_details[[7]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[73]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[73]]$version_group_details[[8]]
## $moves[[73]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[73]]$version_group_details[[8]]$move_learn_method
## $moves[[73]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[73]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[73]]$version_group_details[[8]]$version_group
## $moves[[73]]$version_group_details[[8]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[73]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[74]]
## $moves[[74]]$move
## $moves[[74]]$move$name
## [1] "captivate"
## 
## $moves[[74]]$move$url
## [1] "https://pokeapi.co/api/v2/move/445/"
## 
## 
## $moves[[74]]$version_group_details
## $moves[[74]]$version_group_details[[1]]
## $moves[[74]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[74]]$version_group_details[[1]]$move_learn_method
## $moves[[74]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[74]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[74]]$version_group_details[[1]]$version_group
## $moves[[74]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[74]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[74]]$version_group_details[[2]]
## $moves[[74]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[74]]$version_group_details[[2]]$move_learn_method
## $moves[[74]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[74]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[74]]$version_group_details[[2]]$version_group
## $moves[[74]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[74]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[74]]$version_group_details[[3]]
## $moves[[74]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[74]]$version_group_details[[3]]$move_learn_method
## $moves[[74]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[74]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[74]]$version_group_details[[3]]$version_group
## $moves[[74]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[74]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## 
## 
## $moves[[75]]
## $moves[[75]]$move
## $moves[[75]]$move$name
## [1] "grass-knot"
## 
## $moves[[75]]$move$url
## [1] "https://pokeapi.co/api/v2/move/447/"
## 
## 
## $moves[[75]]$version_group_details
## $moves[[75]]$version_group_details[[1]]
## $moves[[75]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[1]]$move_learn_method
## $moves[[75]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[1]]$version_group
## $moves[[75]]$version_group_details[[1]]$version_group$name
## [1] "diamond-pearl"
## 
## $moves[[75]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/8/"
## 
## 
## 
## $moves[[75]]$version_group_details[[2]]
## $moves[[75]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[2]]$move_learn_method
## $moves[[75]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[2]]$version_group
## $moves[[75]]$version_group_details[[2]]$version_group$name
## [1] "platinum"
## 
## $moves[[75]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/9/"
## 
## 
## 
## $moves[[75]]$version_group_details[[3]]
## $moves[[75]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[3]]$move_learn_method
## $moves[[75]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[3]]$version_group
## $moves[[75]]$version_group_details[[3]]$version_group$name
## [1] "heartgold-soulsilver"
## 
## $moves[[75]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/10/"
## 
## 
## 
## $moves[[75]]$version_group_details[[4]]
## $moves[[75]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[4]]$move_learn_method
## $moves[[75]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[4]]$version_group
## $moves[[75]]$version_group_details[[4]]$version_group$name
## [1] "black-white"
## 
## $moves[[75]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[75]]$version_group_details[[5]]
## $moves[[75]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[5]]$move_learn_method
## $moves[[75]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[5]]$version_group
## $moves[[75]]$version_group_details[[5]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[75]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[75]]$version_group_details[[6]]
## $moves[[75]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[6]]$move_learn_method
## $moves[[75]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[6]]$version_group
## $moves[[75]]$version_group_details[[6]]$version_group$name
## [1] "x-y"
## 
## $moves[[75]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[75]]$version_group_details[[7]]
## $moves[[75]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[7]]$move_learn_method
## $moves[[75]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[7]]$version_group
## $moves[[75]]$version_group_details[[7]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[75]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[75]]$version_group_details[[8]]
## $moves[[75]]$version_group_details[[8]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[8]]$move_learn_method
## $moves[[75]]$version_group_details[[8]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[8]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[8]]$version_group
## $moves[[75]]$version_group_details[[8]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[75]]$version_group_details[[8]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[75]]$version_group_details[[9]]
## $moves[[75]]$version_group_details[[9]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[9]]$move_learn_method
## $moves[[75]]$version_group_details[[9]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[9]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[9]]$version_group
## $moves[[75]]$version_group_details[[9]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[75]]$version_group_details[[9]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[75]]$version_group_details[[10]]
## $moves[[75]]$version_group_details[[10]]$level_learned_at
## [1] 0
## 
## $moves[[75]]$version_group_details[[10]]$move_learn_method
## $moves[[75]]$version_group_details[[10]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[75]]$version_group_details[[10]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[75]]$version_group_details[[10]]$version_group
## $moves[[75]]$version_group_details[[10]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[75]]$version_group_details[[10]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[76]]
## $moves[[76]]$move
## $moves[[76]]$move$name
## [1] "venoshock"
## 
## $moves[[76]]$move$url
## [1] "https://pokeapi.co/api/v2/move/474/"
## 
## 
## $moves[[76]]$version_group_details
## $moves[[76]]$version_group_details[[1]]
## $moves[[76]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[1]]$move_learn_method
## $moves[[76]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[1]]$version_group
## $moves[[76]]$version_group_details[[1]]$version_group$name
## [1] "black-white"
## 
## $moves[[76]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[76]]$version_group_details[[2]]
## $moves[[76]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[2]]$move_learn_method
## $moves[[76]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[2]]$version_group
## $moves[[76]]$version_group_details[[2]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[76]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[76]]$version_group_details[[3]]
## $moves[[76]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[3]]$move_learn_method
## $moves[[76]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[3]]$version_group
## $moves[[76]]$version_group_details[[3]]$version_group$name
## [1] "x-y"
## 
## $moves[[76]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[76]]$version_group_details[[4]]
## $moves[[76]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[4]]$move_learn_method
## $moves[[76]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[4]]$version_group
## $moves[[76]]$version_group_details[[4]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[76]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[76]]$version_group_details[[5]]
## $moves[[76]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[5]]$move_learn_method
## $moves[[76]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[5]]$version_group
## $moves[[76]]$version_group_details[[5]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[76]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[76]]$version_group_details[[6]]
## $moves[[76]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[6]]$move_learn_method
## $moves[[76]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[6]]$version_group
## $moves[[76]]$version_group_details[[6]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[76]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[76]]$version_group_details[[7]]
## $moves[[76]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[76]]$version_group_details[[7]]$move_learn_method
## $moves[[76]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[76]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[76]]$version_group_details[[7]]$version_group
## $moves[[76]]$version_group_details[[7]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[76]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[77]]
## $moves[[77]]$move
## $moves[[77]]$move$name
## [1] "round"
## 
## $moves[[77]]$move$url
## [1] "https://pokeapi.co/api/v2/move/496/"
## 
## 
## $moves[[77]]$version_group_details
## $moves[[77]]$version_group_details[[1]]
## $moves[[77]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[1]]$move_learn_method
## $moves[[77]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[1]]$version_group
## $moves[[77]]$version_group_details[[1]]$version_group$name
## [1] "black-white"
## 
## $moves[[77]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[77]]$version_group_details[[2]]
## $moves[[77]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[2]]$move_learn_method
## $moves[[77]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[2]]$version_group
## $moves[[77]]$version_group_details[[2]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[77]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[77]]$version_group_details[[3]]
## $moves[[77]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[3]]$move_learn_method
## $moves[[77]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[3]]$version_group
## $moves[[77]]$version_group_details[[3]]$version_group$name
## [1] "x-y"
## 
## $moves[[77]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[77]]$version_group_details[[4]]
## $moves[[77]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[4]]$move_learn_method
## $moves[[77]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[4]]$version_group
## $moves[[77]]$version_group_details[[4]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[77]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[77]]$version_group_details[[5]]
## $moves[[77]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[5]]$move_learn_method
## $moves[[77]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[5]]$version_group
## $moves[[77]]$version_group_details[[5]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[77]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[77]]$version_group_details[[6]]
## $moves[[77]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[6]]$move_learn_method
## $moves[[77]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[6]]$version_group
## $moves[[77]]$version_group_details[[6]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[77]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[77]]$version_group_details[[7]]
## $moves[[77]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[77]]$version_group_details[[7]]$move_learn_method
## $moves[[77]]$version_group_details[[7]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[77]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[77]]$version_group_details[[7]]$version_group
## $moves[[77]]$version_group_details[[7]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[77]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[78]]
## $moves[[78]]$move
## $moves[[78]]$move$name
## [1] "echoed-voice"
## 
## $moves[[78]]$move$url
## [1] "https://pokeapi.co/api/v2/move/497/"
## 
## 
## $moves[[78]]$version_group_details
## $moves[[78]]$version_group_details[[1]]
## $moves[[78]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[78]]$version_group_details[[1]]$move_learn_method
## $moves[[78]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[78]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[78]]$version_group_details[[1]]$version_group
## $moves[[78]]$version_group_details[[1]]$version_group$name
## [1] "black-white"
## 
## $moves[[78]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[78]]$version_group_details[[2]]
## $moves[[78]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[78]]$version_group_details[[2]]$move_learn_method
## $moves[[78]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[78]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[78]]$version_group_details[[2]]$version_group
## $moves[[78]]$version_group_details[[2]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[78]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[78]]$version_group_details[[3]]
## $moves[[78]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[78]]$version_group_details[[3]]$move_learn_method
## $moves[[78]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[78]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[78]]$version_group_details[[3]]$version_group
## $moves[[78]]$version_group_details[[3]]$version_group$name
## [1] "x-y"
## 
## $moves[[78]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[78]]$version_group_details[[4]]
## $moves[[78]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[78]]$version_group_details[[4]]$move_learn_method
## $moves[[78]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[78]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[78]]$version_group_details[[4]]$version_group
## $moves[[78]]$version_group_details[[4]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[78]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[78]]$version_group_details[[5]]
## $moves[[78]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[78]]$version_group_details[[5]]$move_learn_method
## $moves[[78]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[78]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[78]]$version_group_details[[5]]$version_group
## $moves[[78]]$version_group_details[[5]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[78]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[78]]$version_group_details[[6]]
## $moves[[78]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[78]]$version_group_details[[6]]$move_learn_method
## $moves[[78]]$version_group_details[[6]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[78]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[78]]$version_group_details[[6]]$version_group
## $moves[[78]]$version_group_details[[6]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[78]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[79]]
## $moves[[79]]$move
## $moves[[79]]$move$name
## [1] "grass-pledge"
## 
## $moves[[79]]$move$url
## [1] "https://pokeapi.co/api/v2/move/520/"
## 
## 
## $moves[[79]]$version_group_details
## $moves[[79]]$version_group_details[[1]]
## $moves[[79]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[1]]$move_learn_method
## $moves[[79]]$version_group_details[[1]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[1]]$version_group
## $moves[[79]]$version_group_details[[1]]$version_group$name
## [1] "black-white"
## 
## $moves[[79]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/11/"
## 
## 
## 
## $moves[[79]]$version_group_details[[2]]
## $moves[[79]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[2]]$move_learn_method
## $moves[[79]]$version_group_details[[2]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[2]]$version_group
## $moves[[79]]$version_group_details[[2]]$version_group$name
## [1] "black-2-white-2"
## 
## $moves[[79]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/14/"
## 
## 
## 
## $moves[[79]]$version_group_details[[3]]
## $moves[[79]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[3]]$move_learn_method
## $moves[[79]]$version_group_details[[3]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[3]]$version_group
## $moves[[79]]$version_group_details[[3]]$version_group$name
## [1] "x-y"
## 
## $moves[[79]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[79]]$version_group_details[[4]]
## $moves[[79]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[4]]$move_learn_method
## $moves[[79]]$version_group_details[[4]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[4]]$version_group
## $moves[[79]]$version_group_details[[4]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[79]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[79]]$version_group_details[[5]]
## $moves[[79]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[5]]$move_learn_method
## $moves[[79]]$version_group_details[[5]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[5]]$version_group
## $moves[[79]]$version_group_details[[5]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[79]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[79]]$version_group_details[[6]]
## $moves[[79]]$version_group_details[[6]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[6]]$move_learn_method
## $moves[[79]]$version_group_details[[6]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[6]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[6]]$version_group
## $moves[[79]]$version_group_details[[6]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[79]]$version_group_details[[6]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[79]]$version_group_details[[7]]
## $moves[[79]]$version_group_details[[7]]$level_learned_at
## [1] 0
## 
## $moves[[79]]$version_group_details[[7]]$move_learn_method
## $moves[[79]]$version_group_details[[7]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[79]]$version_group_details[[7]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[79]]$version_group_details[[7]]$version_group
## $moves[[79]]$version_group_details[[7]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[79]]$version_group_details[[7]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[80]]
## $moves[[80]]$move
## $moves[[80]]$move$name
## [1] "work-up"
## 
## $moves[[80]]$move$url
## [1] "https://pokeapi.co/api/v2/move/526/"
## 
## 
## $moves[[80]]$version_group_details
## $moves[[80]]$version_group_details[[1]]
## $moves[[80]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[80]]$version_group_details[[1]]$move_learn_method
## $moves[[80]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[80]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[80]]$version_group_details[[1]]$version_group
## $moves[[80]]$version_group_details[[1]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[80]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[80]]$version_group_details[[2]]
## $moves[[80]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[80]]$version_group_details[[2]]$move_learn_method
## $moves[[80]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[80]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[80]]$version_group_details[[2]]$version_group
## $moves[[80]]$version_group_details[[2]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[80]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[80]]$version_group_details[[3]]
## $moves[[80]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[80]]$version_group_details[[3]]$move_learn_method
## $moves[[80]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[80]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[80]]$version_group_details[[3]]$version_group
## $moves[[80]]$version_group_details[[3]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[80]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[81]]
## $moves[[81]]$move
## $moves[[81]]$move$name
## [1] "grassy-terrain"
## 
## $moves[[81]]$move$url
## [1] "https://pokeapi.co/api/v2/move/580/"
## 
## 
## $moves[[81]]$version_group_details
## $moves[[81]]$version_group_details[[1]]
## $moves[[81]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[81]]$version_group_details[[1]]$move_learn_method
## $moves[[81]]$version_group_details[[1]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[81]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[81]]$version_group_details[[1]]$version_group
## $moves[[81]]$version_group_details[[1]]$version_group$name
## [1] "x-y"
## 
## $moves[[81]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[81]]$version_group_details[[2]]
## $moves[[81]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[81]]$version_group_details[[2]]$move_learn_method
## $moves[[81]]$version_group_details[[2]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[81]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[81]]$version_group_details[[2]]$version_group
## $moves[[81]]$version_group_details[[2]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[81]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[81]]$version_group_details[[3]]
## $moves[[81]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[81]]$version_group_details[[3]]$move_learn_method
## $moves[[81]]$version_group_details[[3]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[81]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[81]]$version_group_details[[3]]$version_group
## $moves[[81]]$version_group_details[[3]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[81]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[81]]$version_group_details[[4]]
## $moves[[81]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[81]]$version_group_details[[4]]$move_learn_method
## $moves[[81]]$version_group_details[[4]]$move_learn_method$name
## [1] "egg"
## 
## $moves[[81]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/2/"
## 
## 
## $moves[[81]]$version_group_details[[4]]$version_group
## $moves[[81]]$version_group_details[[4]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[81]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## $moves[[81]]$version_group_details[[5]]
## $moves[[81]]$version_group_details[[5]]$level_learned_at
## [1] 0
## 
## $moves[[81]]$version_group_details[[5]]$move_learn_method
## $moves[[81]]$version_group_details[[5]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[81]]$version_group_details[[5]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[81]]$version_group_details[[5]]$version_group
## $moves[[81]]$version_group_details[[5]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[81]]$version_group_details[[5]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## $moves[[82]]
## $moves[[82]]$move
## $moves[[82]]$move$name
## [1] "confide"
## 
## $moves[[82]]$move$url
## [1] "https://pokeapi.co/api/v2/move/590/"
## 
## 
## $moves[[82]]$version_group_details
## $moves[[82]]$version_group_details[[1]]
## $moves[[82]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[82]]$version_group_details[[1]]$move_learn_method
## $moves[[82]]$version_group_details[[1]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[82]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[82]]$version_group_details[[1]]$version_group
## $moves[[82]]$version_group_details[[1]]$version_group$name
## [1] "x-y"
## 
## $moves[[82]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/15/"
## 
## 
## 
## $moves[[82]]$version_group_details[[2]]
## $moves[[82]]$version_group_details[[2]]$level_learned_at
## [1] 0
## 
## $moves[[82]]$version_group_details[[2]]$move_learn_method
## $moves[[82]]$version_group_details[[2]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[82]]$version_group_details[[2]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[82]]$version_group_details[[2]]$version_group
## $moves[[82]]$version_group_details[[2]]$version_group$name
## [1] "omega-ruby-alpha-sapphire"
## 
## $moves[[82]]$version_group_details[[2]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/16/"
## 
## 
## 
## $moves[[82]]$version_group_details[[3]]
## $moves[[82]]$version_group_details[[3]]$level_learned_at
## [1] 0
## 
## $moves[[82]]$version_group_details[[3]]$move_learn_method
## $moves[[82]]$version_group_details[[3]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[82]]$version_group_details[[3]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[82]]$version_group_details[[3]]$version_group
## $moves[[82]]$version_group_details[[3]]$version_group$name
## [1] "sun-moon"
## 
## $moves[[82]]$version_group_details[[3]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/17/"
## 
## 
## 
## $moves[[82]]$version_group_details[[4]]
## $moves[[82]]$version_group_details[[4]]$level_learned_at
## [1] 0
## 
## $moves[[82]]$version_group_details[[4]]$move_learn_method
## $moves[[82]]$version_group_details[[4]]$move_learn_method$name
## [1] "machine"
## 
## $moves[[82]]$version_group_details[[4]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/4/"
## 
## 
## $moves[[82]]$version_group_details[[4]]$version_group
## $moves[[82]]$version_group_details[[4]]$version_group$name
## [1] "ultra-sun-ultra-moon"
## 
## $moves[[82]]$version_group_details[[4]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/18/"
## 
## 
## 
## 
## 
## $moves[[83]]
## $moves[[83]]$move
## $moves[[83]]$move$name
## [1] "grassy-glide"
## 
## $moves[[83]]$move$url
## [1] "https://pokeapi.co/api/v2/move/803/"
## 
## 
## $moves[[83]]$version_group_details
## $moves[[83]]$version_group_details[[1]]
## $moves[[83]]$version_group_details[[1]]$level_learned_at
## [1] 0
## 
## $moves[[83]]$version_group_details[[1]]$move_learn_method
## $moves[[83]]$version_group_details[[1]]$move_learn_method$name
## [1] "tutor"
## 
## $moves[[83]]$version_group_details[[1]]$move_learn_method$url
## [1] "https://pokeapi.co/api/v2/move-learn-method/3/"
## 
## 
## $moves[[83]]$version_group_details[[1]]$version_group
## $moves[[83]]$version_group_details[[1]]$version_group$name
## [1] "sword-shield"
## 
## $moves[[83]]$version_group_details[[1]]$version_group$url
## [1] "https://pokeapi.co/api/v2/version-group/20/"
## 
## 
## 
## 
## 
## 
## $name
## [1] "bulbasaur"
## 
## $order
## [1] 1
## 
## $past_types
## list()
## 
## $species
## $species$name
## [1] "bulbasaur"
## 
## $species$url
## [1] "https://pokeapi.co/api/v2/pokemon-species/1/"
## 
## 
## $sprites
## $sprites$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/1.png"
## 
## $sprites$back_female
## NULL
## 
## $sprites$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/shiny/1.png"
## 
## $sprites$back_shiny_female
## NULL
## 
## $sprites$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png"
## 
## $sprites$front_female
## NULL
## 
## $sprites$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/1.png"
## 
## $sprites$front_shiny_female
## NULL
## 
## $sprites$other
## $sprites$other$dream_world
## $sprites$other$dream_world$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg"
## 
## $sprites$other$dream_world$front_female
## NULL
## 
## 
## $sprites$other$home
## $sprites$other$home$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/1.png"
## 
## $sprites$other$home$front_female
## NULL
## 
## $sprites$other$home$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/shiny/1.png"
## 
## $sprites$other$home$front_shiny_female
## NULL
## 
## 
## $sprites$other$`official-artwork`
## $sprites$other$`official-artwork`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png"
## 
## 
## 
## $sprites$versions
## $sprites$versions$`generation-i`
## $sprites$versions$`generation-i`$`red-blue`
## $sprites$versions$`generation-i`$`red-blue`$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/red-blue/back/1.png"
## 
## $sprites$versions$`generation-i`$`red-blue`$back_gray
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/red-blue/back/gray/1.png"
## 
## $sprites$versions$`generation-i`$`red-blue`$back_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/red-blue/transparent/back/1.png"
## 
## $sprites$versions$`generation-i`$`red-blue`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/red-blue/1.png"
## 
## $sprites$versions$`generation-i`$`red-blue`$front_gray
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/red-blue/gray/1.png"
## 
## $sprites$versions$`generation-i`$`red-blue`$front_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/red-blue/transparent/1.png"
## 
## 
## $sprites$versions$`generation-i`$yellow
## $sprites$versions$`generation-i`$yellow$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/yellow/back/1.png"
## 
## $sprites$versions$`generation-i`$yellow$back_gray
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/yellow/back/gray/1.png"
## 
## $sprites$versions$`generation-i`$yellow$back_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/yellow/transparent/back/1.png"
## 
## $sprites$versions$`generation-i`$yellow$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/yellow/1.png"
## 
## $sprites$versions$`generation-i`$yellow$front_gray
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/yellow/gray/1.png"
## 
## $sprites$versions$`generation-i`$yellow$front_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-i/yellow/transparent/1.png"
## 
## 
## 
## $sprites$versions$`generation-ii`
## $sprites$versions$`generation-ii`$crystal
## $sprites$versions$`generation-ii`$crystal$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/back/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/back/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$back_shiny_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/transparent/back/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$back_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/transparent/back/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$front_shiny_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/transparent/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$crystal$front_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/crystal/transparent/1.png"
## 
## 
## $sprites$versions$`generation-ii`$gold
## $sprites$versions$`generation-ii`$gold$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/gold/back/1.png"
## 
## $sprites$versions$`generation-ii`$gold$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/gold/back/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$gold$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/gold/1.png"
## 
## $sprites$versions$`generation-ii`$gold$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/gold/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$gold$front_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/gold/transparent/1.png"
## 
## 
## $sprites$versions$`generation-ii`$silver
## $sprites$versions$`generation-ii`$silver$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/silver/back/1.png"
## 
## $sprites$versions$`generation-ii`$silver$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/silver/back/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$silver$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/silver/1.png"
## 
## $sprites$versions$`generation-ii`$silver$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/silver/shiny/1.png"
## 
## $sprites$versions$`generation-ii`$silver$front_transparent
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-ii/silver/transparent/1.png"
## 
## 
## 
## $sprites$versions$`generation-iii`
## $sprites$versions$`generation-iii`$emerald
## $sprites$versions$`generation-iii`$emerald$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/emerald/1.png"
## 
## $sprites$versions$`generation-iii`$emerald$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/emerald/shiny/1.png"
## 
## 
## $sprites$versions$`generation-iii`$`firered-leafgreen`
## $sprites$versions$`generation-iii`$`firered-leafgreen`$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/firered-leafgreen/back/1.png"
## 
## $sprites$versions$`generation-iii`$`firered-leafgreen`$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/firered-leafgreen/back/shiny/1.png"
## 
## $sprites$versions$`generation-iii`$`firered-leafgreen`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/firered-leafgreen/1.png"
## 
## $sprites$versions$`generation-iii`$`firered-leafgreen`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/firered-leafgreen/shiny/1.png"
## 
## 
## $sprites$versions$`generation-iii`$`ruby-sapphire`
## $sprites$versions$`generation-iii`$`ruby-sapphire`$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/back/1.png"
## 
## $sprites$versions$`generation-iii`$`ruby-sapphire`$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/back/shiny/1.png"
## 
## $sprites$versions$`generation-iii`$`ruby-sapphire`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/1.png"
## 
## $sprites$versions$`generation-iii`$`ruby-sapphire`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iii/ruby-sapphire/shiny/1.png"
## 
## 
## 
## $sprites$versions$`generation-iv`
## $sprites$versions$`generation-iv`$`diamond-pearl`
## $sprites$versions$`generation-iv`$`diamond-pearl`$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/diamond-pearl/back/1.png"
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$back_female
## NULL
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/diamond-pearl/back/shiny/1.png"
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$back_shiny_female
## NULL
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/diamond-pearl/1.png"
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$front_female
## NULL
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/diamond-pearl/shiny/1.png"
## 
## $sprites$versions$`generation-iv`$`diamond-pearl`$front_shiny_female
## NULL
## 
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/heartgold-soulsilver/back/1.png"
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$back_female
## NULL
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/heartgold-soulsilver/back/shiny/1.png"
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$back_shiny_female
## NULL
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/heartgold-soulsilver/1.png"
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$front_female
## NULL
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/heartgold-soulsilver/shiny/1.png"
## 
## $sprites$versions$`generation-iv`$`heartgold-soulsilver`$front_shiny_female
## NULL
## 
## 
## $sprites$versions$`generation-iv`$platinum
## $sprites$versions$`generation-iv`$platinum$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/platinum/back/1.png"
## 
## $sprites$versions$`generation-iv`$platinum$back_female
## NULL
## 
## $sprites$versions$`generation-iv`$platinum$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/platinum/back/shiny/1.png"
## 
## $sprites$versions$`generation-iv`$platinum$back_shiny_female
## NULL
## 
## $sprites$versions$`generation-iv`$platinum$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/platinum/1.png"
## 
## $sprites$versions$`generation-iv`$platinum$front_female
## NULL
## 
## $sprites$versions$`generation-iv`$platinum$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-iv/platinum/shiny/1.png"
## 
## $sprites$versions$`generation-iv`$platinum$front_shiny_female
## NULL
## 
## 
## 
## $sprites$versions$`generation-v`
## $sprites$versions$`generation-v`$`black-white`
## $sprites$versions$`generation-v`$`black-white`$animated
## $sprites$versions$`generation-v`$`black-white`$animated$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/back/1.gif"
## 
## $sprites$versions$`generation-v`$`black-white`$animated$back_female
## NULL
## 
## $sprites$versions$`generation-v`$`black-white`$animated$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/back/shiny/1.gif"
## 
## $sprites$versions$`generation-v`$`black-white`$animated$back_shiny_female
## NULL
## 
## $sprites$versions$`generation-v`$`black-white`$animated$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/1.gif"
## 
## $sprites$versions$`generation-v`$`black-white`$animated$front_female
## NULL
## 
## $sprites$versions$`generation-v`$`black-white`$animated$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/shiny/1.gif"
## 
## $sprites$versions$`generation-v`$`black-white`$animated$front_shiny_female
## NULL
## 
## 
## $sprites$versions$`generation-v`$`black-white`$back_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/back/1.png"
## 
## $sprites$versions$`generation-v`$`black-white`$back_female
## NULL
## 
## $sprites$versions$`generation-v`$`black-white`$back_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/back/shiny/1.png"
## 
## $sprites$versions$`generation-v`$`black-white`$back_shiny_female
## NULL
## 
## $sprites$versions$`generation-v`$`black-white`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/1.png"
## 
## $sprites$versions$`generation-v`$`black-white`$front_female
## NULL
## 
## $sprites$versions$`generation-v`$`black-white`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/shiny/1.png"
## 
## $sprites$versions$`generation-v`$`black-white`$front_shiny_female
## NULL
## 
## 
## 
## $sprites$versions$`generation-vi`
## $sprites$versions$`generation-vi`$`omegaruby-alphasapphire`
## $sprites$versions$`generation-vi`$`omegaruby-alphasapphire`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vi/omegaruby-alphasapphire/1.png"
## 
## $sprites$versions$`generation-vi`$`omegaruby-alphasapphire`$front_female
## NULL
## 
## $sprites$versions$`generation-vi`$`omegaruby-alphasapphire`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vi/omegaruby-alphasapphire/shiny/1.png"
## 
## $sprites$versions$`generation-vi`$`omegaruby-alphasapphire`$front_shiny_female
## NULL
## 
## 
## $sprites$versions$`generation-vi`$`x-y`
## $sprites$versions$`generation-vi`$`x-y`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vi/x-y/1.png"
## 
## $sprites$versions$`generation-vi`$`x-y`$front_female
## NULL
## 
## $sprites$versions$`generation-vi`$`x-y`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vi/x-y/shiny/1.png"
## 
## $sprites$versions$`generation-vi`$`x-y`$front_shiny_female
## NULL
## 
## 
## 
## $sprites$versions$`generation-vii`
## $sprites$versions$`generation-vii`$icons
## $sprites$versions$`generation-vii`$icons$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vii/icons/1.png"
## 
## $sprites$versions$`generation-vii`$icons$front_female
## NULL
## 
## 
## $sprites$versions$`generation-vii`$`ultra-sun-ultra-moon`
## $sprites$versions$`generation-vii`$`ultra-sun-ultra-moon`$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vii/ultra-sun-ultra-moon/1.png"
## 
## $sprites$versions$`generation-vii`$`ultra-sun-ultra-moon`$front_female
## NULL
## 
## $sprites$versions$`generation-vii`$`ultra-sun-ultra-moon`$front_shiny
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-vii/ultra-sun-ultra-moon/shiny/1.png"
## 
## $sprites$versions$`generation-vii`$`ultra-sun-ultra-moon`$front_shiny_female
## NULL
## 
## 
## 
## $sprites$versions$`generation-viii`
## $sprites$versions$`generation-viii`$icons
## $sprites$versions$`generation-viii`$icons$front_default
## [1] "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-viii/icons/1.png"
## 
## $sprites$versions$`generation-viii`$icons$front_female
## NULL
## 
## 
## 
## 
## 
## $stats
## $stats[[1]]
## $stats[[1]]$base_stat
## [1] 45
## 
## $stats[[1]]$effort
## [1] 0
## 
## $stats[[1]]$stat
## $stats[[1]]$stat$name
## [1] "hp"
## 
## $stats[[1]]$stat$url
## [1] "https://pokeapi.co/api/v2/stat/1/"
## 
## 
## 
## $stats[[2]]
## $stats[[2]]$base_stat
## [1] 49
## 
## $stats[[2]]$effort
## [1] 0
## 
## $stats[[2]]$stat
## $stats[[2]]$stat$name
## [1] "attack"
## 
## $stats[[2]]$stat$url
## [1] "https://pokeapi.co/api/v2/stat/2/"
## 
## 
## 
## $stats[[3]]
## $stats[[3]]$base_stat
## [1] 49
## 
## $stats[[3]]$effort
## [1] 0
## 
## $stats[[3]]$stat
## $stats[[3]]$stat$name
## [1] "defense"
## 
## $stats[[3]]$stat$url
## [1] "https://pokeapi.co/api/v2/stat/3/"
## 
## 
## 
## $stats[[4]]
## $stats[[4]]$base_stat
## [1] 65
## 
## $stats[[4]]$effort
## [1] 1
## 
## $stats[[4]]$stat
## $stats[[4]]$stat$name
## [1] "special-attack"
## 
## $stats[[4]]$stat$url
## [1] "https://pokeapi.co/api/v2/stat/4/"
## 
## 
## 
## $stats[[5]]
## $stats[[5]]$base_stat
## [1] 65
## 
## $stats[[5]]$effort
## [1] 0
## 
## $stats[[5]]$stat
## $stats[[5]]$stat$name
## [1] "special-defense"
## 
## $stats[[5]]$stat$url
## [1] "https://pokeapi.co/api/v2/stat/5/"
## 
## 
## 
## $stats[[6]]
## $stats[[6]]$base_stat
## [1] 45
## 
## $stats[[6]]$effort
## [1] 0
## 
## $stats[[6]]$stat
## $stats[[6]]$stat$name
## [1] "speed"
## 
## $stats[[6]]$stat$url
## [1] "https://pokeapi.co/api/v2/stat/6/"
## 
## 
## 
## 
## $types
## $types[[1]]
## $types[[1]]$slot
## [1] 1
## 
## $types[[1]]$type
## $types[[1]]$type$name
## [1] "grass"
## 
## $types[[1]]$type$url
## [1] "https://pokeapi.co/api/v2/type/12/"
## 
## 
## 
## $types[[2]]
## $types[[2]]$slot
## [1] 2
## 
## $types[[2]]$type
## $types[[2]]$type$name
## [1] "poison"
## 
## $types[[2]]$type$url
## [1] "https://pokeapi.co/api/v2/type/4/"
## 
## 
## 
## 
## $weight
## [1] 69
```

```r
names(poke)
```

```
##  [1] "abilities"                "base_experience"         
##  [3] "forms"                    "game_indices"            
##  [5] "height"                   "held_items"              
##  [7] "id"                       "is_default"              
##  [9] "location_area_encounters" "moves"                   
## [11] "name"                     "order"                   
## [13] "past_types"               "species"                 
## [15] "sprites"                  "stats"                   
## [17] "types"                    "weight"
```

```r
poke[["weight"]]
```

```
## [1] 69
```


