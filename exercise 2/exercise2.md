# Exercise 2

## KNN Practice

First we split the data based on whether the car has a trim level of 350
or 65 AMG. In the plot below we compare price vs mileage for each trim.
![](exercise2_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

First split the data into training and test sets for both trim data

Then Plot RMSE vs K graphs to find the K which gives the minimum RMSE
for both
    models

![](exercise2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

    The KNN model with the minimum RMSE is fitted with K = 17 for a trim level of 350.

![](exercise2_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

    The KNN model with the minimum RMSE is fitted with K = 22 for a trim level of 65 AMG.

Lastly, plot both models over the test data.
![](exercise2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->![](exercise2_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->
Q2 advice: combine values from land model and house improvement
