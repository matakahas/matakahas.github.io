---
title: "data cleaning"
output:
  html_document:
    keep_md: yes
---

## How to rename values in a column




```r
data <- read.csv('./sampledata.csv')
head(data, 3)
```

```
##   Movement Island_Type Island Distance Item
## 1       WH         whe    non       sh    1
## 2       WH         whe    non       sh    2
## 3       WH         whe    non       sh    3
##                                   Sentence Subj_id Score
## 1 Who thinks that Paul stole the necklace?       1     6
## 2     Who thinks that Matt chased the bus?       1     2
## 3 Who thinks that Tom sold the television?       1     3
```
suppose that I want to change the values in the dataset such that the value "sh" under the `Distance` column is "short", and the value "lg" is "long". Here are some ways to achieve this.

```r
#example 1
data$Distance[data$Distance == "sh"] <- "short"
data$Distance[data$Distance == "lg"] <- "long"
```


```r
#example 2
data = data %>% mutate(Distance = ifelse(Distance == "sh", "short", "long"))
```
