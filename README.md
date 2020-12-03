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
