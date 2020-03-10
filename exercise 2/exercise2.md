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

    The KNN model with the minimum RMSE is fitted with K = 21 for a trim level of 350.

![](exercise2_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

    The KNN model with the minimum RMSE is fitted with K = 9 for a trim level of 65 AMG.

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

**Goal: Build Linear and KNN models which predict Saratoga House
Prices**

-----

### Linear Model

The first table below shows the rmse of the medium model vs my “hand
built” model. The second table shows the coefficents for the new “hand
built” model.

| Medium\_Model | New\_Model |
| :-----------: | :--------: |
|   66730.94    |  65172.04  |

|                         |    Coefficents |
| ----------------------- | -------------: |
| (Intercept)             |   1.412753e+05 |
| lotSize                 |   3.375861e+04 |
| livingArea              |   2.081790e+02 |
| age                     | \-1.575181e+02 |
| roomSize                | \-2.516289e+02 |
| waterfrontNo            | \-6.811831e+04 |
| centralAirNo            | \-2.604581e+04 |
| newConstructionNo       |   2.510816e+04 |
| rooms                   | \-9.521115e+03 |
| lotSize:livingArea      | \-2.385748e+01 |
| bathrooms:bedrooms      |   2.676271e+03 |
| lotSize:landValue       |   4.268698e-01 |
| livingArea:waterfrontNo | \-6.682000e+01 |
| lotSize:fireplaces      |   8.802635e+02 |

Compared to the medium model, the new model has a lower RMSE. The new
model uses the equation:

**Price = lotSize \* livingArea + age + bathrooms:bedrooms + roomSize +
waterfront + centralAir + newConstruction + landValue:lotSize +
livingArea:waterfront + rooms + fireplaces:lotSize,
data=saratoga\_train**

To improve on the medium model I removed the variables: pct\_college,
heating, and fuel. I added the variables waterfront and newConstruction.
NewConstruction was a big driver of price because home buyers value new
properties more than one that has already been lived in. Homes being at
a waterfront location was also big driver of price due to it being one
of the most valued locations to have a house. In addition, I added a new
variable called roomSize which was calculated by dividing the size of
the house by the number of rooms. I also added multiple interactions
which were strong drivers of price. For example, I added an interaction
between bathrooms and bedrooms, because bathrooms connected to bedrooms
is important to house buyers.

### KNN Model

To fit a KNN model for Saratoga House Prices using the same variabes as
the linear model, I first standardized the variables. Next I recoded the
categorical variables (waterfront, newConstruction, and centralAir) to
dummy variables corresponding to 1 for yes and 0 for no. Finally to pick
the parameter for the KNN model, the average rmse was calculated (over
100 train/test splits) for K values from 3 to 50. This resulted in the
following rmse vs k scatterplot:

![](exercise2_files/figure-gfm/unnamed-chunk-8-1.png)<!-- --> After
picking the K which resulted in the
rmse,

``` r
cat("The KNN model is fitted with K =",k, "and has an average RMSE of", min(rmse_vals))
```

    ## The KNN model is fitted with K = 18 and has an average RMSE of 65665.88
