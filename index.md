---
title: "Visualization of Infections in different districts of Nepal"
author: "Sudha Bhandari"
highlighter: highlight.js
output: md_document
job: Data Enthusiast
knit: slidify::knit2slides
mode: selfcontained
hitheme: tomorrow
subtitle: Using ggplot visualization to view the number of poeple infected with Communicable
  and Infectious Disease in Nepal
framework: io2012
widgets: []
---

## Infections data
Nepal is country with 75 districts and varying health care facilities among this districts. Every year, there are huge number of people infected with communicable and infectious diseases in various districts of Nepal. I have created a shiny application [Infections data Visualization](https://sudha.shinyapps.io/Sudha/)  to present the data as visualization and presenting my idea in this presentation. I downloaded the data from [Open Data Nepal ](http://data.opennepal.net/)


```r
infections <- read.csv("infections.csv")
nrow(infections)
```

```
## [1] 2980
```

```r
names(infections)
```

```
## [1] "Year"                               
## [2] "District"                           
## [3] "Communicable.and.infectious.disease"
## [4] "Number.of.people"
```


--- .class #id 

## Data Preprocessing



```r
infections$Year <- sapply(strsplit(as.character(infections$Year), "/"),"[[",1)
infections$Year <- as.factor(infections$Year)
infections$District <- as.factor(infections$District)
infections$Number.of.people <- as.numeric(infections$Number.of.people)
infections$Communicable.and.infectious.disease <- as.factor(infections$Communicable.and.infectious.disease)
names(infections) <- c("Year","District","Disease","Number.of.people")
head(infections)
```

```
##   Year District                                Disease Number.of.people
## 1 2009  Bhojpur ARI /Lower respiratory tract infection            13490
## 2 2009  Bhojpur      Upper respiratory Tract infection             5992
## 3 2009  Bhojpur                              Pneumonia             6910
## 4 2009  Bhojpur                       Server Pneumonia              242
## 5 2009  Bhojpur                             Bronchitis             3191
## 6 2009  Bhojpur                                 Asthma             3118
```

--- .class #id2

## Data Visualization of infections in 2009

```r
dataset <- subset(infections, Year = 2009)
aggregated_data <- aggregate(Number.of.people ~ District, data = dataset, FUN = sum)
top_25_data <- aggregated_data[order(-aggregated_data$Number.of.people),][1:25,]
top_25_data$District <- factor(top_25_data$District, levels = top_25_data$District)
head(top_25_data)
```

```
##     District Number.of.people
## 43    Morang           451859
## 28     Jhapa           448791
## 67    Siraha           433504
## 19  Dhanusha           408700
## 69   Sunsari           401130
## 35 Kathmandu           398205
```

--- .class #id3

## Data Visualization output
![Plot](Rplot.png)
This flow is made dynamic to be drived with the district and year selected by user. 
