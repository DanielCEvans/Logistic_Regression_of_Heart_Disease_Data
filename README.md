## Predicting Heart Disease Using Logistic Regression

- “Heart disease is a catch-all term covering a variety of conditions that affect the heart’s structure and function” [1].
- “Coronary heart disease is the leading cause of death in Australia” [1].
- “An estimated 1.2 million (5.6%) Australian adults aged 18 years and over had 1 or more conditions related to heart or vascular disease, including stroke, in 2017–18, based on self-reported data from the Australian Bureau of Statistics (ABS) 2017–18 National Health Survey” [2].

These staggering statistics are the reason behind modelling this particular data. This report aims to determine if there are any key indicators of heart disease among the attributes in the dataset. This will be done through data visualisations and data modelling.

As the target feature ‘diagnosis of heart disease’ is binary, a logistic regression model will be fitted to the data. A logistic regression model will enable us to determine the probability of a patient being diagnosed with heart disease given that patients attribute information. Further, the odds of being diagnosed with heart disease with varying levels of certain significant predictor attributes will be analysed.


## Table of Contents
1. Executive Summary
2. Statistical Modelling
2.1 Model Fitting
2.2 Residual Analysis
2.3 Response Analysis
2.4 Goodness of Fit
2.5 Confidence Intervals
2.6 Hypothesis Tests for Regression Parameters
2.7 Sensitivity Analysis
3. Critique and Limitations
4. Summary and Conclusions
5. References
{:toc}

## 2. Statistical Modelling

For the purpose of the logistic regression model, the categorical variables were converted to factors.

```
heart <- read.csv("Project Group 62_data.csv")

heart$sex <- as.factor(heart$sex)
heart$cp <- as.factor(heart$cp)
heart$fbs <- as.factor(heart$fbs)
heart$restecg <- as.factor(heart$restecg)
heart$exang <- as.factor(heart$exang)
heart$slope <- as.factor(heart$slope)
heart$ca <- as.factor(heart$ca)
heart$thal <- as.factor(heart$thal)
heart$target <- as.factor(heart$target)
```

## 2.1 

Firstly, a saturated logistic model was fitted using all of the independent variables to determine which ones were relevant for predicting heart disease.

#### Full Model

```
mod.fit <- glm(formula = target ~ ., family = binomial(link = logit),
               data = heart)
summary(mod.fit)
```

```
## Call:
## glm(formula = target ~ ., family = binomial(link = logit), data = heart)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -2.9459  -0.2738   0.1012   0.4515   3.1248  
## 
## Coefficients:
##              Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  0.179045   3.705420   0.048 0.961461    
## age          0.027819   0.025428   1.094 0.273938    
## sex1        -1.862297   0.570844  -3.262 0.001105 ** 
## cp1          0.864708   0.578000   1.496 0.134645    
## cp2          2.003186   0.529356   3.784 0.000154 ***
## cp3          2.417107   0.719242   3.361 0.000778 ***
## trestbps    -0.026162   0.011943  -2.191 0.028481 *  
## chol        -0.004291   0.004245  -1.011 0.312053    
## fbs1         0.445666   0.587977   0.758 0.448472    
## restecg1     0.460582   0.399615   1.153 0.249089    
## restecg2    -0.714204   2.768873  -0.258 0.796453    
## thalach      0.020055   0.011859   1.691 0.090820 .  
## exang1      -0.779111   0.451839  -1.724 0.084652 .  
## oldpeak     -0.397174   0.242346  -1.639 0.101239    
## slope1      -0.775084   0.880495  -0.880 0.378707    
## slope2       0.689965   0.947657   0.728 0.466568    
## ca1         -2.342301   0.527416  -4.441 8.95e-06 ***
## ca2         -3.483178   0.811640  -4.292 1.77e-05 ***
## ca3         -2.247144   0.937629  -2.397 0.016547 *  
## ca4          1.267961   1.720014   0.737 0.461013    
## thal1        2.637558   2.684285   0.983 0.325808    
## thal2        2.367747   2.596159   0.912 0.361759    
## thal3        0.915115   2.600380   0.352 0.724901    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 417.64  on 302  degrees of freedom
## Residual deviance: 179.63  on 280  degrees of freedom
## AIC: 225.63
## 
## Number of Fisher Scoring iterations: 6
```

```
Anova(mod.fit)
```

```
## Analysis of Deviance Table (Type II tests)
## 
## Response: target
##          LR Chisq Df Pr(>Chisq)    
## age         1.209  1  0.2715575    
## sex        11.810  1  0.0005892 ***
## cp         21.419  3  8.617e-05 ***
## trestbps    5.043  1  0.0247270 *  
## chol        0.991  1  0.3194764    
## fbs         0.583  1  0.4452161    
## restecg     1.458  2  0.4823037    
## thalach     3.002  1  0.0831391 .  
## exang       2.958  1  0.0854290 .  
## oldpeak     2.809  1  0.0937236 .  
## slope       9.402  2  0.0090856 ** 
## ca         40.038  4  4.250e-08 ***
## thal       13.703  3  0.0033389 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```
The analysis of variance of the saturated model indicates that sex, type of chest pain (cp), resting blood pressure (trestbps), slope of the peak during exercise (slope), number of major vessels coloured by fluoroscopy (ca), and whether or not someone had a heart defect (thal) are all good predictors of heart disease as their p values all fall below 0.05.


