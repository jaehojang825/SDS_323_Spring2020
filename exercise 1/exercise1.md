Exercise 1
==========

``` r
library(readr)
library(tidyverse)
library(mosaic)
urlfile = "https://raw.githubusercontent.com/jgscott/SDS323/master/data/ABIA.csv"
mydata <- read_csv(url(urlfile))
```

Data visualization: flights at ABIA
-----------------------------------

``` r
# Group data by airline and calculate mean arrival/departure delay
grouped_Data <- mydata %>% group_by(UniqueCarrier) %>% summarise(mean_DepDelay=mean(DepDelay,na.rm=TRUE),mean_ArrDelay=mean(ArrDelay,na.rm=TRUE), count=n())

#Get subset of top 5 airlines in terms of number of flights.
grouped_Data <- grouped_Data %>% arrange(desc(count))
grouped_Data <- grouped_Data %>% slice(1:5)

# Flatten data to seperate arrival and departure delay
grouped_Data <- grouped_Data %>% gather("Direction","Delay",-count,-UniqueCarrier)

grouped_Data$UniqueCarrier <- recode(grouped_Data$UniqueCarrier, AA="American", WN="Southwest",B6="JetBlue", YV="Mesa", CO="Continental")
ggplot(grouped_Data,aes(x=UniqueCarrier,y=Delay,fill=Direction)) +
  geom_col(position = "dodge") +
  ggtitle("Austin Flight Arrival/Departure Delay by Airline")+
  labs(x="Airline",y="Mean Delay")
```

![](exercise1_files/figure-markdown_github/unnamed-chunk-2-1.png)

<ins>
Conclusion
</ins>
<br> From the graph, it is reasonable to conclude that their is not any
significant difference in flight delays among the top 5 major airlines
flying out of Austin. The exception is Southwest Airlines which has the
lowest arrival delay. The reason for this could be that many of
Southwest flight into Austin are in-state flights and thus have less
time for delays to occur.

Regression Practice
-------------------

``` r
creatinine = read.csv("creatinine.csv",header=TRUE)
lm1 = lm(creatclear~age,data = creatinine)

#plug in age 55 to linear model to get expected creatine clearance rate
 
coef(lm1)
```

    ## (Intercept)         age 
    ## 147.8129158  -0.6198159

``` r
cleareance_rate55 = as.numeric(coef(lm1)[1]) + (55 * as.numeric(coef(lm1)[2]))
ggplot(creatinine) +
  geom_point(mapping=aes(x=age,y=creatclear))
```

![](exercise1_files/figure-markdown_github/unnamed-chunk-3-1.png)

1.  Based on the linear model we can expect a creatine clearance rate
    of  
    147.813 + (55\*-0.6198) = **113.723 ml/minute**.

2.  As age increases creatinine clearance rate decreases by **0.6198
    ml/minute per year**

3.  E(Creatinine clearance rate \| Age = 40) = 147.813 + (40*-0.6198) =
    123.02 E(Creatinine clearance rate \| Age = 60) = 147.813 +
    (60*-0.6198) = 110.624 135 - 123.0203 = 11.98 112 - 110.624 = 1.376
    Because the residual is higher, the 40-year-old is healthier for his
    age than the 60-year-old.
