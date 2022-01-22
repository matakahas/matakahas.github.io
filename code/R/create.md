---
title: "data cleaning"
output:
  html_document:
    keep_md: yes
---

## How to generate a column based on an existing column




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

suppose that I want to create a column `Condition` consisting of values 1 through 4, which correspond to the conditions as specified under the `Island` and `Distance` columns. Here is one way to achieve this.

```r
data <- data %>% mutate(Condition = case_when((Island == "non" & Distance == "sh") ~ 1,
                                              (Island == "non" & Distance == "lg") ~ 2,
                                              (Island == "isl" & Distance == "sh") ~ 3,
                                              (Island == "isl" & Distance == "lg") ~ 4,
                                              TRUE ~ 0))
```
