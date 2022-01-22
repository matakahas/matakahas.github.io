---
title: "data cleaning & visualization practice"
output:
  html_document:
    keep_md: yes
---
## Overview
this file walks you through the process of importing a dataset that resembles the real dataset that we obtain from an acceptability judgment experiment, cleaning it, and analyzing it. 

## Install and import required packages

`tidyverse` is a collection of R packages ("libraries") designed for data science.
uncomment and run the following code if the package is not installed in your environment:

```r
#install.packages('tidyverse') 
```

call the installed library so that we can use it in this file


## Import and clean the data

```r
data = read.csv('./fakedata.csv')
```

check the data type of each column

```r
glimpse(data)
```

```
## Rows: 512
## Columns: 6
## $ X         <int> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17…
## $ Sentence  <chr> "統計的機械学習での分析が応用可能で、より精度の高いデータと…
## $ Lex_set   <int> 1, 1, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, …
## $ Condition <int> 1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, …
## $ Subj_id   <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ Score     <int> 6, 5, 3, 1, 7, 6, 1, 1, 7, 5, 1, 3, 6, 5, 3, 4, 6, 5, 4, 2, …
```
There are columns like the following: \
* `Lex_set`: Serial number of lexicalization sets (sets of sentences that belong to different conditions but share certain words and phrases)
* `Condition`: Serial number of condition. As you can see, each lexicalization set consists of four sentences belonging to the different conditions
* `Score`: Acceptability score given by participants

**NB**: If you are seeing unicodes (e.g., `\u9ad8`) but not kanji under the `Sentence` column, try updating R (not R Studio) to the latest version (R 4.1.2 as of December 2021)

let's convert some of the data types from numerical to categorical. This is because the variables like `Condition` are numbered but we do not intend to apply mathematical operations to them.

```r
cols = c('Lex_set', 'Condition', 'Subj_id')
data[cols] = lapply(data[cols], factor) 
```

we can obtain a subset of data (i.e., certain rows and/or certain columns) using a square bracket

```r
#subset rows to show acceptability scores from subject 1
data[data$Subj_id == 1, 6] #6 is the column index of the Score column 
```

```
##  [1] 6 5 3 1 7 6 1 1 7 5 1 3 6 5 3 4 6 5 4 2 7 5 3 2 7 5 2 1 6 5 3 3
```
or we can do so with `which()` function

```r
#getting row numbers where the subject ID is ten
idx = which(data$Subj_id == 10)
data[idx, ]
```

```
##       X
## 289 288
## 290 289
## 291 290
## 292 291
## 293 292
## 294 293
## 295 294
## 296 295
## 297 296
## 298 297
## 299 298
## 300 299
## 301 300
## 302 301
## 303 302
## 304 303
## 305 304
## 306 305
## 307 306
## 308 307
## 309 308
## 310 309
## 311 310
## 312 311
## 313 312
## 314 313
## 315 314
## 316 315
## 317 316
## 318 317
## 319 318
## 320 319
##                                                                                                                     Sentence
## 289                                             統計的機械学習での分析が応用可能で、より精度の高いデータと統計的モデリングが
## 290                                             統計的機械学習での誤差は、計算モデルによって測定される。誤差関数formula_13は
## 291                                         統計的機械学習での標本化の手法は、次のようになる。これは、与えられた条件下で学習
## 292                                 統計的機械学習での学習には、特定の神経細胞領域がどのように機能するかに関する実験的モデル
## 293                           世界中の商品情報を、業界の実情や背景を踏まえて発信し、消費者に新たな可能性を提供するための広報
## 294                   世界中の商品情報を発信するために日本を代表するローカル紙「週刊東洋経済」を発行していた。創刊当初から、
## 295                               世界中の商品情報をまとめ、それらを雑誌に載せるといった、いわば「パワフル雑誌」となっている
## 296               世界中の商品情報を発信するとともに、各都道府県の情報を提供している。また、各種地域情報を発信するため、全国
## 297 情報流通を促進することを目的としている。全国経済産業団体連合会の傘下に入っている。経済産業省と経済産業省資源エネルギー庁
## 298                 情報流通を促進するための新たな政策、例えばインターネット普及の促進のための新たな政策、たとえば、通信技術
## 299                       情報流通を促進するために、情報流通業者(情報流通エージェントなど)を育成することを目指している。また
## 300                                        情報流通を促進するためには、販売流通機構の確立が必要である。その第1段階が流通機構
## 301                                                   私たちの強みは、より人間的(すなわち人間の脳)である」という言葉を引用。
## 302                                                                 私たちの強みは他者の強みであった。この強みは相手を「強み
## 303                                                           私たちの強みは、他者の弱みである」と教えていた。この主張は後の
## 304                                                        私たちの強みは、その強さであった」 と表現している。「その能力は、
## 305                                                         チームワークを意識して、練習には4年振り(2021年8月時点)の現役復帰
## 306                                        チームワークを意識して、練習に打ち込めた。小学校の1年でサッカーを始め、中学からは
## 307                                          チームワークを意識して作られた。2019年7月23日、本作の主要撮影がシカゴで始まった
## 308                                              チームワークを意識して、「」という曲が生まれた。『Inner Red』は、「」という
## 309                                   インターネットの配信に使用しているドメインである。2018年4月現在、ユーザーは50.1%がこの
## 310   インターネットのゲーム『ファイナルファンタジーXII』のシナリオライターを務めた。同作者の漫画『ファイナルファンタジーXII
## 311                           インターネットのニュースサイトを介した報道を行える「ニュースサイト ニュースサイト フォーチュン
## 312                                                  インターネットのメディアサイト(YouTube)で1位を獲得した。2019年2月、S.I.
## 313                                   会社でトラブルの原因を追及していた。しかし、この事故は、ボーイングが事故機について検査
## 314                                                   会社でトラブルの原因を解明した後、アメリカへ渡った。2013年の秋、サメの
## 315                                 会社でトラブルの原因を尋ねられていた。その調査を進めるうちに、大勢の人間が消えた。しかも
## 316                                                    会社でトラブルの原因を究明する作業員と、その社員が協力して、2人の男性
## 317                                              最新のニュース映像やイベント、CMなども放送。2018年8月からは、平日朝7:30 - 8
## 318                                    最新のニュース映像や映像を提供。2019年10月からは、ニュースルームで「Live News Network
## 319                 最新のニュース映像や番組が放送されるが、番組本編ではノンスクランブルかつ完全ノンスクランブルで放送される
## 320                         最新のニュース映像やライブステージなどのほか、音楽シーンや番組独自のコーナーも多数放送する。2020
##     Lex_set Condition Subj_id Score
## 289       1         1      10     6
## 290       1         2      10     6
## 291       1         3      10     4
## 292       1         4      10     2
## 293       2         1      10     7
## 294       2         2      10     5
## 295       2         3      10     4
## 296       2         4      10     1
## 297       3         1      10     5
## 298       3         2      10     6
## 299       3         3      10     3
## 300       3         4      10     1
## 301       4         1      10     7
## 302       4         2      10     5
## 303       4         3      10     2
## 304       4         4      10     4
## 305       5         1      10     6
## 306       5         2      10     7
## 307       5         3      10     2
## 308       5         4      10     1
## 309       6         1      10     7
## 310       6         2      10     6
## 311       6         3      10     1
## 312       6         4      10     4
## 313       7         1      10     5
## 314       7         2      10     5
## 315       7         3      10     1
## 316       7         4      10     1
## 317       8         1      10     6
## 318       8         2      10     5
## 319       8         3      10     1
## 320       8         4      10     2
```

### Exercise 1: Find & replace rows with NA values
suppose that I forgot to turn on the feature in my experiment where participants must select an answer in order to proceed. As a result, there may be some rows with an acceptability score missing. Find rows with a missing `Score` value and replace them with **3**.

**Advanced**: Find rows with a missing `Score` value and replace them with the mean acceptability score. 


```r
#write your answers here
```

### Answers

```r
#find rows with NA values
data[is.na(data$Score),]
```

```
##       X
## 159 158
## 232 231
## 454 453
##                                                                                                       Sentence
## 159   最新のニュース映像や番組が放送されるが、番組本編ではノンスクランブルかつ完全ノンスクランブルで放送される
## 232 世界中の商品情報を発信するとともに、各都道府県の情報を提供している。また、各種地域情報を発信するため、全国
## 454     世界中の商品情報を発信するために日本を代表するローカル紙「週刊東洋経済」を発行していた。創刊当初から、
##     Lex_set Condition Subj_id Score
## 159       8         3       5    NA
## 232       2         4       8    NA
## 454       2         2      15    NA
```


```r
#replace NA values with 3
idx = which(is.na(data$Score)) #get row number of missing values
data[idx, ]$Score = 3
data[idx, ]
```

```
##       X
## 159 158
## 232 231
## 454 453
##                                                                                                       Sentence
## 159   最新のニュース映像や番組が放送されるが、番組本編ではノンスクランブルかつ完全ノンスクランブルで放送される
## 232 世界中の商品情報を発信するとともに、各都道府県の情報を提供している。また、各種地域情報を発信するため、全国
## 454     世界中の商品情報を発信するために日本を代表するローカル紙「週刊東洋経済」を発行していた。創刊当初から、
##     Lex_set Condition Subj_id Score
## 159       8         3       5     3
## 232       2         4       8     3
## 454       2         2      15     3
```


```r
#replace NA values with mean score.
#Don't forget to include na.rm=TRUE, or the returned value will be NA
data[idx, ]$Score = mean(data$Score, na.rm=TRUE)
data[idx, ]
```

```
##       X
## 159 158
## 232 231
## 454 453
##                                                                                                       Sentence
## 159   最新のニュース映像や番組が放送されるが、番組本編ではノンスクランブルかつ完全ノンスクランブルで放送される
## 232 世界中の商品情報を発信するとともに、各都道府県の情報を提供している。また、各種地域情報を発信するため、全国
## 454     世界中の商品情報を発信するために日本を代表するローカル紙「週刊東洋経済」を発行していた。創刊当初から、
##     Lex_set Condition Subj_id    Score
## 159       8         3       5 4.439453
## 232       2         4       8 4.439453
## 454       2         2      15 4.439453
```

### Exercise 2: Find & modify impossible scores
suppose also that there are some rows with the acceptability score out of the possible range (1 to 7). Find such rows.

**Advanced**: Replace the rows with **7** if a value is over 7, and **1** if it is under 1. Hint: Use `ifelse()` function whose arguments are condition, value if the condition is met, value if the condition is not met


```r
#example
sample_data = data.frame(a = seq(1,8), b = LETTERS[1:8])
#make a new column c where a value is "even" if column a on the same row is an even number, "odd" if an odd number
sample_data$c = ifelse(sample_data$a %% 2 == 0, "even", "odd")
sample_data
```

```
##   a b    c
## 1 1 A  odd
## 2 2 B even
## 3 3 C  odd
## 4 4 D even
## 5 5 E  odd
## 6 6 F even
## 7 7 G  odd
## 8 8 H even
```


```r
#write your answers here
```

### Answers

```r
#find rows with the score of over 7 or under 1 and modify them
idx = which(data$Score > 7 | data$Score < 1)
data[idx, ]$Score = ifelse(data[idx, ]$Score > 7, 7, 1)
data[idx, ]
```

```
##       X
## 188 187
## 377 376
##                                                                                   Sentence
## 188                  会社でトラブルの原因を究明する作業員と、その社員が協力して、2人の男性
## 377 会社でトラブルの原因を追及していた。しかし、この事故は、ボーイングが事故機について検査
##     Lex_set Condition Subj_id Score
## 188       7         4       6     1
## 377       7         1      12     7
```

## Get the summary of results
grouping the data by condition and averaging the acceptability score with the `summarize` function is a quick and easy way to get a snapshot of results.

```r
data %>% group_by(Condition) %>% summarize(ave = mean(Score))
```

```
## # A tibble: 4 × 2
##   Condition   ave
##   <fct>     <dbl>
## 1 1          6.07
## 2 2          5.89
## 3 3          2.57
## 4 4          2.49
```

### Exercise 3: Get an average score per participant 

```r
#write your answers here
```

### Answer

```r
data %>% group_by(Subj_id) %>% summarize(ave = mean(Score))
```

```
## # A tibble: 16 × 2
##    Subj_id   ave
##    <fct>   <dbl>
##  1 1        4.06
##  2 2        4.06
##  3 3        4   
##  4 4        4.59
##  5 5        4.26
##  6 6        4.06
##  7 7        4.25
##  8 8        4.42
##  9 9        4.16
## 10 10       4   
## 11 11       4.31
## 12 12       4.5 
## 13 13       4.75
## 14 14       4.28
## 15 15       4.26
## 16 16       4.06
```

## Convert raw acceptability scores to z-scores
in reality, participants make use of the acceptability scale in various ways; some people use 1 and 7 exclusively, while other people stick to 3 through 5. In order to normalize their scores, it is common to convert raw acceptability to z-scores (standard scores). The formula for z-score conversion is as follows:  

z-score = raw score - sample mean / standard deviation of sample  


```r
data = data %>% group_by(Subj_id) %>% mutate(Z_score = (Score - mean(Score)) / sd(Score))
```

## Plot the results
we will use the package `ggplot` for visualization. The syntax for ggplot is slightly different from the R syntax, such as the use of `+` when you want to add plot features. First, we will create a summary data to be plotted.

```r
data_summary = data %>% group_by(Condition) %>% summarize(Ave = mean(Z_score))

#the code below converts condition numbers to actual condition names
columns = data.frame(Extraction=c('no_extraction', 'no_extraction', 'extraction', 'extraction'),
                     RC=c('non_RC','RC','non_RC','RC'))
data_summary = cbind(columns, data_summary)
data_summary
```

```
##      Extraction     RC Condition        Ave
## 1 no_extraction non_RC         1  0.9122053
## 2 no_extraction     RC         2  0.8148336
## 3    extraction non_RC         3 -0.8437908
## 4    extraction     RC         4 -0.8832481
```


```r
data_summary$Extraction = factor(data_summary$Extraction, levels = c('no_extraction', 'extraction'))

data_summary %>% ggplot(aes(x=Extraction, y=Ave))+
  geom_point()+
  geom_path(aes(group = RC, linetype = rev(RC)))+
  guides(linetype = guide_legend(reverse = TRUE))+
  expand_limits(y = c(-1, 1))
```

![](practice_files/figure-html/unnamed-chunk-20-1.png)<!-- -->

### Exercise 4: Make the graph look better
please do the following:  
- Change the title of the y-axis to be something more descriptive (e.g., "mean acceptability in z-score")  
- Remove the x-axis title ("Extraction")  
- Make the axis titles and labels bigger  
- Remove the legend title ("rev(RC)")
- Remove the grey background and grids (use function `theme_classic()` or `theme_bw()`)
- **Advanced** move the legend so that it is displayed inside the graph (rather than next to the graph)

```r
#write your answers here
```

### Answer

```r
data_summary %>% ggplot(aes(x=Extraction, y=Ave))+
  geom_point()+
  geom_path(aes(group = RC, linetype = rev(RC)))+
  guides(linetype = guide_legend(reverse = TRUE))+
  expand_limits(y = c(-1, 1))+
  theme_classic()+
  ylab('mean z-score')+
  theme(legend.title = element_blank(),
        legend.position = c(0.9, 0.9),
        legend.text = element_text(size = 15),
        axis.text.x = element_text(size = 15),
        axis.title.x = element_blank(),
        axis.title.y = element_text(size = 15))
```

![](practice_files/figure-html/unnamed-chunk-22-1.png)<!-- -->


