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

    ## Start:  AIC=30282.24
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     sewer + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - sewer            2 5.9727e+09 4.4195e+12 30280
    ## - fireplaces       1 1.9887e+07 4.4135e+12 30280
    ## - age              1 4.1804e+07 4.4135e+12 30280
    ## - pctCollege       1 1.0457e+08 4.4136e+12 30280
    ## - fuel             2 1.0136e+10 4.4236e+12 30281
    ## <none>                          4.4135e+12 30282
    ## - heating          2 2.3261e+10 4.4367e+12 30286
    ## - centralAir       1 1.9275e+10 4.4328e+12 30286
    ## - rooms            1 2.4272e+10 4.4378e+12 30288
    ## - bedrooms         1 3.5352e+10 4.4488e+12 30291
    ## - lotSize          1 4.9730e+10 4.4632e+12 30296
    ## - waterfront       1 6.8851e+10 4.4823e+12 30302
    ## - newConstruction  1 7.4325e+10 4.4878e+12 30303
    ## - bathrooms        1 1.2747e+11 4.5409e+12 30320
    ## - livingArea       1 6.5086e+11 5.0643e+12 30470
    ## - landValue        1 1.0768e+12 5.4903e+12 30582
    ## 
    ## Step:  AIC=30280.11
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + fireplaces + bathrooms + rooms + heating + fuel + 
    ##     waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - fireplaces       1 1.3757e+07 4.4195e+12 30278
    ## - age              1 8.1696e+07 4.4195e+12 30278
    ## - fuel             2 6.8366e+09 4.4263e+12 30278
    ## - pctCollege       1 5.2399e+08 4.4200e+12 30278
    ## <none>                          4.4195e+12 30280
    ## - centralAir       1 1.7887e+10 4.4373e+12 30284
    ## - heating          2 2.4726e+10 4.4442e+12 30284
    ## - rooms            1 2.4559e+10 4.4440e+12 30286
    ## - bedrooms         1 3.3711e+10 4.4532e+12 30289
    ## - lotSize          1 6.7252e+10 4.4867e+12 30299
    ## - waterfront       1 7.0701e+10 4.4902e+12 30300
    ## - newConstruction  1 7.5985e+10 4.4954e+12 30302
    ## - bathrooms        1 1.2423e+11 4.5437e+12 30316
    ## - livingArea       1 6.5157e+11 5.0710e+12 30468
    ## - landValue        1 1.0716e+12 5.4911e+12 30578
    ## 
    ## Step:  AIC=30278.11
    ## price ~ lotSize + age + landValue + livingArea + pctCollege + 
    ##     bedrooms + bathrooms + rooms + heating + fuel + waterfront + 
    ##     newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - age              1 7.8285e+07 4.4195e+12 30276
    ## - fuel             2 6.8330e+09 4.4263e+12 30276
    ## - pctCollege       1 5.5849e+08 4.4200e+12 30276
    ## <none>                          4.4195e+12 30278
    ## - centralAir       1 1.8010e+10 4.4375e+12 30282
    ## - heating          2 2.4867e+10 4.4443e+12 30282
    ## - rooms            1 2.4659e+10 4.4441e+12 30284
    ## - bedrooms         1 3.3700e+10 4.4532e+12 30287
    ## - lotSize          1 6.7364e+10 4.4868e+12 30297
    ## - waterfront       1 7.0824e+10 4.4903e+12 30298
    ## - newConstruction  1 7.6229e+10 4.4957e+12 30300
    ## - bathrooms        1 1.2489e+11 4.5444e+12 30315
    ## - livingArea       1 6.8158e+11 5.1010e+12 30474
    ## - landValue        1 1.0719e+12 5.4914e+12 30576
    ## 
    ## Step:  AIC=30276.14
    ## price ~ lotSize + landValue + livingArea + pctCollege + bedrooms + 
    ##     bathrooms + rooms + heating + fuel + waterfront + newConstruction + 
    ##     centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - pctCollege       1 5.6125e+08 4.4201e+12 30274
    ## - fuel             2 7.3058e+09 4.4269e+12 30274
    ## <none>                          4.4195e+12 30276
    ## - centralAir       1 1.8504e+10 4.4381e+12 30280
    ## - heating          2 2.6598e+10 4.4461e+12 30280
    ## - rooms            1 2.4734e+10 4.4443e+12 30282
    ## - bedrooms         1 3.4806e+10 4.4544e+12 30285
    ## - lotSize          1 6.8674e+10 4.4882e+12 30295
    ## - waterfront       1 7.0753e+10 4.4903e+12 30296
    ## - newConstruction  1 7.7179e+10 4.4967e+12 30298
    ## - bathrooms        1 1.3872e+11 4.5583e+12 30317
    ## - livingArea       1 6.8153e+11 5.1011e+12 30472
    ## - landValue        1 1.0874e+12 5.5069e+12 30578
    ## 
    ## Step:  AIC=30274.31
    ## price ~ lotSize + landValue + livingArea + bedrooms + bathrooms + 
    ##     rooms + heating + fuel + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## - fuel             2 6.9370e+09 4.4270e+12 30273
    ## <none>                          4.4201e+12 30274
    ## - centralAir       1 1.7944e+10 4.4381e+12 30278
    ## - heating          2 2.7058e+10 4.4472e+12 30279
    ## - rooms            1 2.4739e+10 4.4448e+12 30280
    ## - bedrooms         1 3.5537e+10 4.4556e+12 30283
    ## - lotSize          1 6.9102e+10 4.4892e+12 30294
    ## - waterfront       1 7.2480e+10 4.4926e+12 30295
    ## - newConstruction  1 7.7244e+10 4.4974e+12 30296
    ## - bathrooms        1 1.3895e+11 4.5591e+12 30315
    ## - livingArea       1 6.8105e+11 5.1012e+12 30470
    ## - landValue        1 1.1065e+12 5.5266e+12 30581
    ## 
    ## Step:  AIC=30272.48
    ## price ~ lotSize + landValue + livingArea + bedrooms + bathrooms + 
    ##     rooms + heating + waterfront + newConstruction + centralAir
    ## 
    ##                   Df  Sum of Sq        RSS   AIC
    ## <none>                          4.4270e+12 30273
    ## - centralAir       1 1.9515e+10 4.4466e+12 30277
    ## - heating          2 3.0525e+10 4.4576e+12 30278
    ## - rooms            1 2.5001e+10 4.4520e+12 30278
    ## - bedrooms         1 3.4742e+10 4.4618e+12 30281
    ## - lotSize          1 6.3071e+10 4.4901e+12 30290
    ## - waterfront       1 7.0369e+10 4.4974e+12 30292
    ## - newConstruction  1 7.6088e+10 4.5031e+12 30294
    ## - bathrooms        1 1.5209e+11 4.5791e+12 30317
    ## - livingArea       1 6.7974e+11 5.1068e+12 30468
    ## - landValue        1 1.1317e+12 5.5587e+12 30585

    ## 
    ## Call:
    ## lm(formula = price ~ lotSize + landValue + livingArea + bedrooms + 
    ##     bathrooms + rooms + heating + waterfront + newConstruction + 
    ##     centralAir, data = saratoga_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -224164  -34086   -4181   27825  453762 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             7.369e+04  2.299e+04   3.205  0.00138 ** 
    ## lotSize                 1.236e+04  2.797e+03   4.418 1.07e-05 ***
    ## landValue               9.421e-01  5.034e-02  18.714  < 2e-16 ***
    ## livingArea              7.207e+01  4.969e+00  14.504  < 2e-16 ***
    ## bedrooms               -9.184e+03  2.801e+03  -3.279  0.00107 ** 
    ## bathrooms               2.384e+04  3.474e+03   6.860 1.04e-11 ***
    ## rooms                   2.912e+03  1.047e+03   2.782  0.00548 ** 
    ## heatinghot water/steam -1.325e+04  4.442e+03  -2.982  0.00291 ** 
    ## heatingelectric        -6.245e+03  4.381e+03  -1.425  0.15431    
    ## waterfrontNo           -9.092e+04  1.948e+04  -4.667 3.36e-06 ***
    ## newConstructionNo       3.706e+04  7.637e+03   4.852 1.36e-06 ***
    ## centralAirNo           -9.046e+03  3.681e+03  -2.457  0.01411 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 56850 on 1370 degrees of freedom
    ## Multiple R-squared:  0.6644, Adjusted R-squared:  0.6617 
    ## F-statistic: 246.5 on 11 and 1370 DF,  p-value: < 2.2e-16

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
    ## -226209  -33183   -3998   26906  444748 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             9.023e+05  1.753e+05   5.147 3.03e-07 ***
    ## lotSize                 1.155e+04  2.793e+03   4.137 3.74e-05 ***
    ## age                    -2.471e+01  6.279e+01  -0.394 0.693978    
    ## landValue               8.926e-01  5.144e-02  17.353  < 2e-16 ***
    ## livingArea              1.937e+02  2.724e+01   7.111 1.85e-12 ***
    ## bedrooms                1.658e+04  7.559e+03   2.194 0.028408 *  
    ## bathrooms               2.492e+04  3.656e+03   6.814 1.41e-11 ***
    ## rooms                   2.116e+03  1.054e+03   2.008 0.044820 *  
    ## heatinghot water/steam -1.105e+04  4.536e+03  -2.435 0.015001 *  
    ## heatingelectric        -6.596e+03  4.411e+03  -1.495 0.135039    
    ## waterfrontNo           -9.104e+04  1.937e+04  -4.700 2.87e-06 ***
    ## newConstructionNo       3.958e+04  7.697e+03   5.143 3.10e-07 ***
    ## centralAirNo           -1.051e+04  3.702e+03  -2.840 0.004576 ** 
    ## log(livingArea)        -1.407e+05  2.928e+04  -4.805 1.72e-06 ***
    ## livingArea:bedrooms    -1.298e+01  3.832e+00  -3.388 0.000724 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 56430 on 1367 degrees of freedom
    ## Multiple R-squared:   0.67,  Adjusted R-squared:  0.6666 
    ## F-statistic: 198.2 on 14 and 1367 DF,  p-value: < 2.2e-16

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
    ##    67456.79    58642.30

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
    ##    67456.79    58642.30    57093.46

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
assume children would be more likely to be on the reservation. Finally,
customer type was interacted with several other indicator variables.

The RMSE for the engineered model is:

    engineered_rmse

    ## [1] 0.2320949

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
