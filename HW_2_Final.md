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

    ## Start:  AIC=30407.85
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     sewer + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - sewer            2 2.8738e+09 4.8363e+12 30405
    ## - fuel             2 5.4394e+09 4.8389e+12 30405
    ## - fireplaces       1 1.8186e+08 4.8336e+12 30406
    ## - pctCollege       1 2.5343e+09 4.8360e+12 30407
    ## <none>                          4.8334e+12 30408
    ## - age              1 1.0045e+10 4.8435e+12 30409
    ## - heating          2 1.9798e+10 4.8532e+12 30410
    ## - rooms            1 2.0640e+10 4.8541e+12 30412
    ## - bedrooms         1 2.0932e+10 4.8544e+12 30412
    ## - lotSize          1 2.8319e+10 4.8618e+12 30414
    ## - centralAir       1 3.1305e+10 4.8647e+12 30415
    ## - newConstruction  1 1.2617e+11 4.9596e+12 30442
    ## - bathrooms        1 1.3967e+11 4.9731e+12 30445
    ## - waterfront       1 1.4699e+11 4.9804e+12 30447
    ## - livingArea       1 6.1740e+11 5.4508e+12 30572
    ## - landValue        1 1.1697e+12 6.0031e+12 30705
    ## 
    ## Step:  AIC=30404.67
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - fuel             2 4.6631e+09 4.8410e+12 30402
    ## - fireplaces       1 2.2961e+08 4.8365e+12 30403
    ## - pctCollege       1 3.5112e+09 4.8398e+12 30404
    ## <none>                          4.8363e+12 30405
    ## - age              1 1.0405e+10 4.8467e+12 30406
    ## - heating          2 2.0963e+10 4.8573e+12 30407
    ## - bedrooms         1 2.0036e+10 4.8563e+12 30408
    ## - rooms            1 2.0534e+10 4.8568e+12 30409
    ## - centralAir       1 3.0360e+10 4.8667e+12 30411
    ## - lotSize          1 3.6999e+10 4.8733e+12 30413
    ## - newConstruction  1 1.2763e+11 4.9639e+12 30439
    ## - bathrooms        1 1.3788e+11 4.9742e+12 30442
    ## - waterfront       1 1.4782e+11 4.9841e+12 30444
    ## - livingArea       1 6.2045e+11 5.4568e+12 30570
    ## - landValue        1 1.1692e+12 6.0055e+12 30702
    ## 
    ## Step:  AIC=30402.01
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + waterfront + 
    ##     newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - fireplaces       1 2.1484e+08 4.8412e+12 30400
    ## - pctCollege       1 2.7122e+09 4.8437e+12 30401
    ## <none>                          4.8410e+12 30402
    ## - age              1 1.1894e+10 4.8529e+12 30403
    ## - bedrooms         1 1.9079e+10 4.8600e+12 30405
    ## - rooms            1 2.1143e+10 4.8621e+12 30406
    ## - heating          2 3.2787e+10 4.8738e+12 30407
    ## - centralAir       1 3.0252e+10 4.8712e+12 30409
    ## - lotSize          1 3.4985e+10 4.8760e+12 30410
    ## - newConstruction  1 1.2579e+11 4.9668e+12 30436
    ## - bathrooms        1 1.3813e+11 4.9791e+12 30439
    ## - waterfront       1 1.4761e+11 4.9886e+12 30442
    ## - livingArea       1 6.1968e+11 5.4606e+12 30567
    ## - landValue        1 1.1906e+12 6.0316e+12 30704
    ## 
    ## Step:  AIC=30400.07
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + bathrooms + rooms + heating + waterfront + newConstruction + 
    ##     centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - pctCollege       1 2.5542e+09 4.8437e+12 30399
    ## <none>                          4.8412e+12 30400
    ## - age              1 1.2097e+10 4.8533e+12 30402
    ## - bedrooms         1 1.9182e+10 4.8604e+12 30404
    ## - rooms            1 2.1005e+10 4.8622e+12 30404
    ## - heating          2 3.2722e+10 4.8739e+12 30405
    ## - centralAir       1 3.1192e+10 4.8724e+12 30407
    ## - lotSize          1 3.5127e+10 4.8763e+12 30408
    ## - newConstruction  1 1.2737e+11 4.9686e+12 30434
    ## - bathrooms        1 1.4135e+11 4.9825e+12 30438
    ## - waterfront       1 1.4756e+11 4.9887e+12 30440
    ## - livingArea       1 6.5691e+11 5.4981e+12 30574
    ## - landValue        1 1.1908e+12 6.0319e+12 30702
    ## 
    ## Step:  AIC=30398.8
    ## price ~ lotSize + age + landValue + livingArea + bedrooms + bathrooms + 
    ##     rooms + heating + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## <none>                          4.8437e+12 30399
    ## - age              1 1.1786e+10 4.8555e+12 30400
    ## - bedrooms         1 2.0212e+10 4.8640e+12 30403
    ## - rooms            1 2.0965e+10 4.8647e+12 30403
    ## - heating          2 3.2624e+10 4.8764e+12 30404
    ## - centralAir       1 2.9080e+10 4.8728e+12 30405
    ## - lotSize          1 3.6650e+10 4.8804e+12 30407
    ## - newConstruction  1 1.2521e+11 4.9689e+12 30432
    ## - bathrooms        1 1.4135e+11 4.9851e+12 30437
    ## - waterfront       1 1.5477e+11 4.9985e+12 30440
    ## - livingArea       1 6.5531e+11 5.4990e+12 30572
    ## - landValue        1 1.2128e+12 6.0565e+12 30706

    ## 
    ## Call:
    ## lm(formula = price ~ lotSize + age + landValue + livingArea + 
    ##     bedrooms + bathrooms + rooms + heating + waterfront + newConstruction + 
    ##     centralAir, data = saratoga_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -223241  -36193   -4818   27567  454828 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             8.964e+04  2.091e+04   4.287 1.94e-05 ***
    ## lotSize                 6.951e+03  2.160e+03   3.218  0.00132 ** 
    ## age                    -1.149e+02  6.293e+01  -1.825  0.06820 .  
    ## landValue               9.531e-01  5.148e-02  18.514  < 2e-16 ***
    ## livingArea              6.996e+01  5.140e+00  13.609  < 2e-16 ***
    ## bedrooms               -6.912e+03  2.892e+03  -2.390  0.01698 *  
    ## bathrooms               2.389e+04  3.779e+03   6.321 3.52e-10 ***
    ## rooms                   2.693e+03  1.106e+03   2.434  0.01505 *  
    ## heatinghot water/steam -1.154e+04  4.760e+03  -2.424  0.01548 *  
    ## heatingelectric        -1.062e+04  4.662e+03  -2.279  0.02284 *  
    ## waterfrontNo           -1.116e+05  1.687e+04  -6.614 5.36e-11 ***
    ## newConstructionNo       4.727e+04  7.946e+03   5.949 3.43e-09 ***
    ## centralAirNo           -1.106e+04  3.858e+03  -2.867  0.00421 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 59480 on 1369 degrees of freedom
    ## Multiple R-squared:  0.6565, Adjusted R-squared:  0.6535 
    ## F-statistic:   218 on 12 and 1369 DF,  p-value: < 2.2e-16

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
    ## -270488  -35690   -3774   26718  446428 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             8.501e+05  1.796e+05   4.734 2.43e-06 ***
    ## lotSize                 6.237e+03  2.154e+03   2.896 0.003845 ** 
    ## age                    -1.166e+02  6.269e+01  -1.861 0.062994 .  
    ## landValue               9.084e-01  5.220e-02  17.404  < 2e-16 ***
    ## livingArea              1.847e+02  2.798e+01   6.600 5.88e-11 ***
    ## bedrooms                1.834e+04  7.730e+03   2.372 0.017807 *  
    ## bathrooms               2.501e+04  3.767e+03   6.641 4.48e-11 ***
    ## rooms                   2.034e+03  1.111e+03   1.831 0.067277 .  
    ## heatinghot water/steam -9.964e+03  4.748e+03  -2.099 0.036029 *  
    ## heatingelectric        -1.062e+04  4.658e+03  -2.281 0.022730 *  
    ## waterfrontNo           -1.119e+05  1.678e+04  -6.671 3.69e-11 ***
    ## newConstructionNo       4.868e+04  7.910e+03   6.154 9.88e-10 ***
    ## centralAirNo           -1.237e+04  3.849e+03  -3.214 0.001338 ** 
    ## log(livingArea)        -1.298e+05  3.007e+04  -4.318 1.69e-05 ***
    ## livingArea:bedrooms    -1.280e+01  3.863e+00  -3.313 0.000947 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 59120 on 1367 degrees of freedom
    ## Multiple R-squared:  0.6611, Adjusted R-squared:  0.6577 
    ## F-statistic: 190.5 on 14 and 1367 DF,  p-value: < 2.2e-16

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
    ##    66896.84    58287.51

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
    ##    66896.84    58287.51    57093.46

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

    ## [1] 0.2682055

The model with all the data provided (exlcuding arrival date) has the
following estimated RMSE:

    all_rmse

    ## [1] 0.2285238

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
assume children would be more likely to be on the reservation. Finally,
customer type was interacted with several other indicator variables.

The RMSE for the engineered model is:

    engineered_rmse

    ## [1] 0.2283713

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
