# ECO 395M HW 1: Daniel Oliner, Musab Alquwaee, Jacob McGill

# Q1: Executive Summary

Focusing on the data set on house prices in Saratoga, NY, this report
presents a comparative analysis of two model classes: Linear Models and
K-Nearest-Neighbors. We will begin by building a comprehensive linear
model, then a KNN model, then will evaluate the two models’ efficacy and
predictive accuracy by comparing their out-of-sample mean-squared error.
The goal is to identify a model that combines high predictive accuracy
with practicality for use by the local taxing authority.

## Question 1: Part 1: Building an Enhanced Linear Model

    ## Start:  AIC=30362.29
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     sewer + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - sewer            2 8.8181e+08 4.6776e+12 30359
    ## - fireplaces       1 5.8001e+08 4.6772e+12 30361
    ## - pctCollege       1 6.7086e+08 4.6773e+12 30361
    ## - fuel             2 7.4980e+09 4.6842e+12 30361
    ## <none>                          4.6767e+12 30362
    ## - heating          2 1.4197e+10 4.6909e+12 30363
    ## - age              1 1.4439e+10 4.6911e+12 30365
    ## - rooms            1 1.9336e+10 4.6960e+12 30366
    ## - centralAir       1 2.4660e+10 4.7013e+12 30368
    ## - bedrooms         1 3.5005e+10 4.7117e+12 30371
    ## - lotSize          1 3.7246e+10 4.7139e+12 30371
    ## - waterfront       1 9.1376e+10 4.7680e+12 30387
    ## - newConstruction  1 1.0747e+11 4.7841e+12 30392
    ## - bathrooms        1 1.2300e+11 4.7997e+12 30396
    ## - livingArea       1 6.5833e+11 5.3350e+12 30542
    ## - landValue        1 1.0619e+12 5.7386e+12 30643
    ## 
    ## Step:  AIC=30358.55
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - fuel             2 6.6479e+09 4.6842e+12 30357
    ## - fireplaces       1 5.1861e+08 4.6781e+12 30357
    ## - pctCollege       1 9.6098e+08 4.6785e+12 30357
    ## <none>                          4.6776e+12 30359
    ## - heating          2 1.4549e+10 4.6921e+12 30359
    ## - age              1 1.4719e+10 4.6923e+12 30361
    ## - rooms            1 1.9318e+10 4.6969e+12 30362
    ## - centralAir       1 2.4177e+10 4.7017e+12 30364
    ## - bedrooms         1 3.4388e+10 4.7119e+12 30367
    ## - lotSize          1 4.4799e+10 4.7224e+12 30370
    ## - waterfront       1 9.1897e+10 4.7694e+12 30383
    ## - newConstruction  1 1.0803e+11 4.7856e+12 30388
    ## - bathrooms        1 1.2214e+11 4.7997e+12 30392
    ## - livingArea       1 6.5831e+11 5.3359e+12 30539
    ## - landValue        1 1.0687e+12 5.7462e+12 30641
    ## 
    ## Step:  AIC=30356.51
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + waterfront + 
    ##     newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - fireplaces       1 4.3313e+08 4.6846e+12 30355
    ## - pctCollege       1 5.2278e+08 4.6847e+12 30355
    ## <none>                          4.6842e+12 30357
    ## - age              1 1.8496e+10 4.7027e+12 30360
    ## - rooms            1 1.9355e+10 4.7036e+12 30360
    ## - centralAir       1 2.5133e+10 4.7093e+12 30362
    ## - heating          2 3.6377e+10 4.7206e+12 30363
    ## - bedrooms         1 3.2667e+10 4.7169e+12 30364
    ## - lotSize          1 4.0184e+10 4.7244e+12 30366
    ## - waterfront       1 8.8297e+10 4.7725e+12 30380
    ## - newConstruction  1 1.0606e+11 4.7903e+12 30386
    ## - bathrooms        1 1.2588e+11 4.8101e+12 30391
    ## - livingArea       1 6.5553e+11 5.3397e+12 30536
    ## - landValue        1 1.0959e+12 5.7801e+12 30645
    ## 
    ## Step:  AIC=30354.64
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + bathrooms + rooms + heating + waterfront + newConstruction + 
    ##     centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - pctCollege       1 6.6551e+08 4.6853e+12 30353
    ## <none>                          4.6846e+12 30355
    ## - age              1 1.8214e+10 4.7028e+12 30358
    ## - rooms            1 1.9545e+10 4.7042e+12 30358
    ## - centralAir       1 2.4727e+10 4.7094e+12 30360
    ## - heating          2 3.6221e+10 4.7209e+12 30361
    ## - bedrooms         1 3.2494e+10 4.7171e+12 30362
    ## - lotSize          1 3.9988e+10 4.7246e+12 30364
    ## - waterfront       1 8.8399e+10 4.7730e+12 30379
    ## - newConstruction  1 1.0569e+11 4.7903e+12 30384
    ## - bathrooms        1 1.2598e+11 4.8106e+12 30389
    ## - livingArea       1 6.7475e+11 5.3594e+12 30539
    ## - landValue        1 1.0960e+12 5.7806e+12 30643
    ## 
    ## Step:  AIC=30352.83
    ## price ~ lotSize + age + landValue + livingArea + bedrooms + bathrooms + 
    ##     rooms + heating + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## <none>                          4.6853e+12 30353
    ## - age              1 1.8029e+10 4.7033e+12 30356
    ## - rooms            1 1.9669e+10 4.7050e+12 30357
    ## - centralAir       1 2.4062e+10 4.7094e+12 30358
    ## - heating          2 3.6291e+10 4.7216e+12 30360
    ## - bedrooms         1 3.3384e+10 4.7187e+12 30361
    ## - lotSize          1 4.0858e+10 4.7262e+12 30363
    ## - waterfront       1 9.1778e+10 4.7771e+12 30378
    ## - newConstruction  1 1.0636e+11 4.7917e+12 30382
    ## - bathrooms        1 1.2585e+11 4.8111e+12 30388
    ## - livingArea       1 6.7409e+11 5.3594e+12 30537
    ## - landValue        1 1.1260e+12 5.8113e+12 30649

    ## 
    ## Call:
    ## lm(formula = price ~ lotSize + age + landValue + livingArea + 
    ##     bedrooms + bathrooms + rooms + heating + waterfront + newConstruction + 
    ##     centralAir, data = saratoga_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -206349  -35676   -4508   28130  453133 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             8.385e+04  2.172e+04   3.860 0.000119 ***
    ## lotSize                 8.558e+03  2.477e+03   3.455 0.000567 ***
    ## age                    -1.497e+02  6.523e+01  -2.295 0.021875 *  
    ## landValue               9.494e-01  5.234e-02  18.139  < 2e-16 ***
    ## livingArea              7.085e+01  5.048e+00  14.034  < 2e-16 ***
    ## bedrooms               -9.137e+03  2.925e+03  -3.123 0.001826 ** 
    ## bathrooms               2.261e+04  3.729e+03   6.064 1.72e-09 ***
    ## rooms                   2.579e+03  1.076e+03   2.397 0.016648 *  
    ## heatinghot water/steam -9.891e+03  4.713e+03  -2.098 0.036048 *  
    ## heatingelectric        -1.311e+04  4.594e+03  -2.853 0.004391 ** 
    ## waterfrontNo           -9.355e+04  1.807e+04  -5.178 2.57e-07 ***
    ## newConstructionNo       4.420e+04  7.928e+03   5.575 2.98e-08 ***
    ## centralAirNo           -1.018e+04  3.840e+03  -2.652 0.008105 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 58500 on 1369 degrees of freedom
    ## Multiple R-squared:  0.6446, Adjusted R-squared:  0.6414 
    ## F-statistic: 206.9 on 12 and 1369 DF,  p-value: < 2.2e-16

Started by running an “everything and the kitchen sink” model and then
used a backwards selection approach to iteratively delete statistically
insignificant variables in order to improve model performance.

    ## 
    ## Call:
    ## lm(formula = price ~ lotSize + age + landValue + livingArea + 
    ##     bedrooms + bathrooms + rooms + heating + waterfront + newConstruction + 
    ##     centralAir + livingArea:bedrooms + log(livingArea), data = saratoga_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -207797  -34145   -4680   27595  443608 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             1.014e+06  1.874e+05   5.410 7.44e-08 ***
    ## lotSize                 7.594e+03  2.463e+03   3.083  0.00209 ** 
    ## age                    -1.488e+02  6.507e+01  -2.286  0.02240 *  
    ## landValue               8.943e-01  5.302e-02  16.867  < 2e-16 ***
    ## livingArea              2.148e+02  2.980e+01   7.209 9.32e-13 ***
    ## bedrooms                2.282e+04  8.028e+03   2.843  0.00454 ** 
    ## bathrooms               2.452e+04  3.716e+03   6.599 5.92e-11 ***
    ## rooms                   1.864e+03  1.077e+03   1.731  0.08363 .  
    ## heatinghot water/steam -8.327e+03  4.685e+03  -1.778  0.07569 .  
    ## heatingelectric        -1.318e+04  4.584e+03  -2.876  0.00409 ** 
    ## waterfrontNo           -9.305e+04  1.791e+04  -5.195 2.36e-07 ***
    ## newConstructionNo       4.708e+04  7.888e+03   5.969 3.04e-09 ***
    ## centralAirNo           -1.177e+04  3.823e+03  -3.079  0.00212 ** 
    ## log(livingArea)        -1.600e+05  3.167e+04  -5.051 4.98e-07 ***
    ## livingArea:bedrooms    -1.643e+01  4.077e+00  -4.029 5.91e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 58000 on 1367 degrees of freedom
    ## Multiple R-squared:  0.6511, Adjusted R-squared:  0.6475 
    ## F-statistic: 182.2 on 14 and 1367 DF,  p-value: < 2.2e-16

We proceeded by creating a model with the relevant variables remaining
after the backwards selection process, then adding a relevant
interaction term (living area:bedrooms) and one logarithmic
transformation. We included an interaction of living area size and
number of bedrooms because we suspected that the combination of living
area size and the number of bedrooms together influence the price of a
house in ways that considering each of these factors alone cannot
capture. We also included a logarithmic transformation of the living
area variable in order to capture how proportional changes in living
area affect price, allowing for non-linearity in the relationship
between these variables.

    ## Using parallel package.
    ##   * Set seed with set.rseed().
    ##   * Disable this message with options(`mosaic:parallelMessage` = FALSE)

    ## Average Out-of-Sample RMSE Across 100 Train/Test Splits

    ##         lm2 lm_enhanced 
    ##    66133.65    58121.78

As evidenced above, the average out-of-sample RMSE for our enhanced
model is clearly lower than that of the previously considered medium
model. We used the average RMSEs over 100 train/test splits in order to
account for random variation in measuring out-of-sample performance.

## Question 1: Part 2: Building the KNN Model

    ## k-Nearest Neighbors 
    ## 
    ## 1383 samples
    ##   10 predictor
    ## 
    ## Pre-processing: centered (10), scaled (10) 
    ## Resampling: Cross-Validated (10 fold, repeated 3 times) 
    ## Summary of sample sizes: 1244, 1246, 1246, 1244, 1246, 1244, ... 
    ## Resampling results across tuning parameters:
    ## 
    ##   k    RMSE      Rsquared   MAE     
    ##    14  65596.47  0.5758291  45632.29
    ##   118  72173.83  0.5248243  49006.41
    ##   179  74122.32  0.5099177  49781.43
    ##   195  74623.45  0.5055043  50083.18
    ##   229  75568.76  0.5001878  50616.50
    ##   244  75967.34  0.4976787  50834.51
    ##   299  77330.09  0.4914922  51612.39
    ##   306  77519.96  0.4905998  51724.76
    ##   426  80415.64  0.4810244  53488.36
    ## 
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final value used for the model was k = 14.

    ##         RMSE     Rsquared          MAE 
    ## 5.709346e+04 6.166043e-01 4.212205e+04

### Model Comparison: Linear Model vs KNN

    ## Average Out-of-Sample RMSE By Model

    ##         lm2 lm_enhanced  KNN (k=14) 
    ##    66133.65    58121.78    57093.46

## Q1: Conclusion

Based on our analysis, the KNN model seems to do better at achieving a
lower out-of-sample mean squared error, indicating a higher level of
predictive accuracy relative to the linear model. This suggests that for
the purpose of estimating house prices in Saratoga, NY, the KNN model
might be the preferred choice. However, it’s important to note that the
difference in performance between the two models is relatively modest.
The choice between these models should also consider factors such as
interpretability and ease of implementation. While the KNN model offers
marginally better accuracy, the enhanced linear model provides clearer
insights into how specific features influence house prices, which could
be valuable for policy formulation and decision-making by the local
taxing authority. Considering the taxing authority’s need to predict
property values to determine tax policy, the slightly lower RMSE
achieved by the KNN model suggests that the KNN model is performing
marginally better at predicting property values in this context.

# Question 2: German Credit Data

![](HW_2_Final_files/figure-markdown_strict/unnamed-chunk-9-1.png)

    ##         (Intercept)            duration              amount         installment 
    ##               -0.71                0.03                0.00                0.22 
    ##                 age         historypoor     historyterrible          purposeedu 
    ##               -0.02               -1.11               -1.88                0.72 
    ## purposegoods/repair       purposenewcar      purposeusedcar       foreigngerman 
    ##                0.10                0.85               -0.80               -1.26

The data and analysis from a German bank highlight a puzzling
relationship between credit history and loan defaults. The bar plot
indicates that worse credit history is associated with higher default
rates. However, the logistic regression model suggests the opposite,
with ‘poor’ and ‘terrible’ credit histories associated with lower
default probabilities, which contradicts common financial intuition.

This contradiction is likely due to the bank’s sampling method, which
oversamples defaults. This method creates a bias, making the model less
applicable to the general population of borrowers. For the model to be
useful in screening new borrowers, the bank needs to use a sample that
accurately reflects the true default rate in its overall portfolio.
Correcting this sampling bias is essential for the bank to develop a
reliable model for classifying borrowers by default risk.

# Question 3: Hotel Bookings

## Model Engineering

To estimate the performance of these 3 models, we will use K-fold cross
validation with K = 10 to calculate the RMSE for each linear probability
model.

The 1st model has the following estimated RMSE:

    spec_rmse

    ## [1] 0.2682111

The model with all the data provided (exlcuding arrival date) has the
following estimated RMSE:

    all_rmse

    ## [1] 0.2332761

For the best performing model, we expanded off the all model and added
several interaction terms and polynomials. We fitted adults to a 2nd
degree polynomial, since increasing adults up to likely increases the
chance of children coming but after the would decrease. We also fitted
lead time to a 2nd degree polynomial, since reservations booked very
early and very late would likely be business trips, as well as total
number of special requests since families may make some requests for
their children but a large amount indicates some special or business
event. Finally, stay in weekend nights and stay in week nights were
fitted to 2nd degree polynomials as well, as large amounts of both would
indicate long term stays, which would likely not have children. I also
added an interaction term for is\_repeated\_guest and
previous\_bookings\_not\_canceled, as that may indicate a repeat
customer who makes sudden changes to their bookings, which would likely
not have a child. Finally, I extracted several pieces of data from the
timestamp of arrival. “Summer” marks whether the reservation was in the
Summer, a time when children are more likely to be traveling. I also
added week\_end arrival, which tracked if the reservation started on
Friday or Saturday. As people arriving on those days are likely
traveling for vacation rather than business, it would be reasonable to
assume children would be more likely to be on the reservation.

The RMSE for the engineered model is:

    engineered_rmse

    ## [1] 0.2323567

As can be seen, this model outperforms the other 2 in terms of RMSE.

## Data Validation

I am then moving on to validating the data with the hotels\_val set. To
do so, I graph the the model’s Total Positivity Rate (TPR) and False
Positivity Rate (FPR) as a function of t, the threshold for considering
a predicted probability a yes.

![](HW_2_Final_files/figure-markdown_strict/unnamed-chunk-19-1.png)

## Fold test

After graphing the ROC curve, we move to testing model against 20 equal
sized folds int he validation data set.

The below figure summarizes this performance, with the red bars being
the actual amount of bookings with children and the red the predicted
amount of bookings. As can be seen, the model does moderately well at
predicting the total number of bookings with children. While the model
did not perfectly predict a fold, it was never substantially of (such as
having a prediction off by 10 or more). Considering that each fold has
about 250 bookings, that is not a substantial deviance.

![](HW_2_Final_files/figure-markdown_strict/unnamed-chunk-21-1.png)

# Question 4: Poisonous Mushrooms

    ## [1] "Optimal lambda: 0.000676086748498989"

    ## Setting levels: control = 0, case = 1

    ## Setting direction: controls < cases

![](HW_2_Final_files/figure-markdown_strict/unnamed-chunk-24-1.png)

    ## Area under the curve: 1

    ##          Actual
    ## Predicted   0   1
    ##         0 841   0
    ##         1   0 783

    ## [1] "True Positive Rate: 1"

    ## [1] "False Positive Rate: 0"

The document contains results from a Lasso regression model with 10-fold
cross-validation, indicating an optimal lambda value of approximately
0.000676. The area under the ROC curve (AUC) is 1, suggesting perfect
model performance. The confusion matrix shows no misclassifications,
with 841 true negatives and 783 true positives, leading to a True
Positive Rate (TPR) of 1 and a False Positive Rate (FPR) of 0. These
results suggest that the model perfectly distinguishes between the
classes without any errors, so a threshold of 1 would be recommended for
declaring a mushroom poisonous.
