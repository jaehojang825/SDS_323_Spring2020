Exercise 1
==========

``` r
library(readr)
library(tidyverse)
library(mosaic)
urlfile = "https://raw.githubusercontent.com/jgscott/SDS323/master/data/ABIA.csv"
mydata <- read_csv(url(urlfile))
```

``` r
grouped_Data <- mydata %>% group_by(UniqueCarrier) %>% summarise(mean_DepDelay=mean(DepDelay,na.rm=TRUE),mean_ArrDelay=mean(ArrDelay,na.rm=TRUE), count=n())
grouped_Data <- grouped_Data %>% arrange(desc(count))
grouped_Data <- grouped_Data %>% slice(1:5)
grouped_Data <- grouped_Data %>% gather("Direction","Delay",-count,-UniqueCarrier)
ggplot(grouped_Data,aes(x=UniqueCarrier,y=Delay,fill=Direction)) +
  geom_col(position = "dodge")
```

![](exercise1_files/figure-markdown_github/unnamed-chunk-2-1.png)
