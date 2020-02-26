Exercise 2
==========

``` r
library(tidyverse)
library(mosaic)
```

KNN Practice
------------

``` r
sclass = read.csv("sclass.csv")

# Split data based on trim
trim_350 = sclass[sclass$trim == "350",]
trim_65 = sclass[sclass$trim == "65 AMG",]
```

### Split the data into training and test sets for both trim data

``` r
# Define the training and testing set for 350 trim
N_350 = nrow(trim_350)
N_train_350 = floor(0.8*N_350)
N_test_350 = N_350 - N_train_350
train_ind_350 = sample.int(N_350, N_train_350, replace=FALSE)
D_train_350 = trim_350[train_ind_350,]
D_test_350 = trim_350[-train_ind_350,]

# Define the training and testing set for 65 AMG trim
N_65 = nrow(trim_65)
N_train_65= floor(0.8*N_65)
N_test_65 = N_65 - N_train_65
train_ind_65 = sample.int(N_65, N_train_65, replace=FALSE)
D_train_65 = trim_65[train_ind_65,]
D_test_65 = trim_65[-train_ind_65,]
```
