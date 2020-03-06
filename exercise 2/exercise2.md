# Exercise 2

## KNN Practice

**Goal:** Build two KNN models for 350 and 65 AMG trim Mercedes to
predict car price given a car’s mileage.

-----

First we split the data based on whether the car has a trim level of 350
or 65 AMG. In the plot below we compare price vs mileage for each trim.

![](exercise2_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

As we can see from the above scatterplot, there is a group of 65 AMG
cars with 0 mileage which have a significantly higher price than the 350
trim cars. This will affect how the two models are built later.

Next we need to split the data into training and test tests and use the
training sets to fit two KNN models. This leads to the question of how
to pick the model parameters K for each model. One way to do this is to
pick the K which gives the minimum root mean square error (rmse) using
the test sets. Below is a plot of RMSE vs K for each
    model:

![](exercise2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

    The KNN model with the minimum RMSE is fitted with K = 16 for a trim level of 350.

![](exercise2_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

    The KNN model with the minimum RMSE is fitted with K = 33 for a trim level of 65 AMG.

Now that we have fitted each model with a K parameter which minimizes
RMSE, we can plot both models over its corresponding test data to
visualize how the predictions (in red) compared with the actual values
(grey
points).

![](exercise2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->![](exercise2_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

The 65 AMG model is always fitted with a higher K value than the 350
trim model. At the beginning of the analysis, it was pointed out that
there is a group of outlier 65 AMG trim cars which have significantly
higher price and 0 mileage. If we chose a lower K value for the 65 AMG
trim model, our predictions would have higher variance because the model
would memorize the noise of the outliers. Since the 350 trim model has
less extreme outliers choosing a smaller K doesn’t lead to as much error
as choosing a small K would in the 65 AMG model. Therefore a larger K
minimizes RMSE for the 65 AMG model and the oppositie is true for the
350 trim model.

## Saratoga House Prices

**Goal: Build Linear and KNN models which predict Saratoga House Price**

-----

| Medium\_Model | New\_Model |
| :-----------: | :--------: |
|   68314.57    |  65736.09  |

Q2 advice: combine values from land model and house improvement
