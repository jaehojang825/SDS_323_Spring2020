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
grouped_Data <- mydata %>% group_by(UniqueCarrier) %>% summarise(mean_DepDelay=mean(DepDelay,na.rm=TRUE),mean_ArrDelay=mean(ArrDelay,na.rm=TRUE), count=n())
grouped_Data <- grouped_Data %>% arrange(desc(count))
grouped_Data <- grouped_Data %>% slice(1:5)
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
From the graph, it is reasonable to conclude that their is not any
significant difference in flight delays among the top 5 major airlines
flying out of Austin. The exception is Southwest Airlines which has the
lowest arrival delay. The reason for this could be that many of
Southwest flight into Austin are in-state flights and thus have less
time for delays to occur.
