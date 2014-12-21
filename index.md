---
title       : Predict Maximum Dose of a Drug
subtitle    : Predict the maximum dose
author      : Kirsten Frank
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Reason to make this application

"The Dose Makes the Poison"-- Paracelsus 

This application uses data about the pharmacokinetics of Theophylline to predict the maximum concentration in the blood.

The maximum concentration in the blood is the maximum effective dose. Most drugs have an optimal dosage, above that there is a poisonous dose. 



---

## Data source

The data were taken from a dataset that is in the R base setup.

Boeckmann, Sheiner and Beal (1994) wrote up a study from Dr. Robert Upton. This study had twelve subjects. Each subject was weighed, given an amount of theophylline, and had blood drawn for serum concentrations at 11 time points in the next 25 hours. 

In processing this data, I found the observation where concentration was a maximum for each subject. I created a new dataset with just the subject ID, weight (in kg), Dose (in mg of drug/kg of subject weight), maximum concentration and time. I created a new variable recipWt, equal to one over the weight. I fit the maximum concentration to a linear function of dose and recipWt. 


Boeckmann, A. J., Sheiner, L. B. and Beal, S. L. (1994), NONMEM Users Guide: Part V, NONMEM Project Group, University of California, San Francisco.

---

## Fit display


```r
summary(fitobj4)
```

```
## 
## Call:
## lm(formula = MaxConc ~ recipWt * Dose, data = MaxConcset)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -2.1842 -0.2586  0.1406  0.4406  1.9236 
## 
## Coefficients:
##               Estimate Std. Error t value Pr(>|t|)  
## (Intercept)     52.819     26.134   2.021   0.0779 .
## recipWt      -4008.585   2895.951  -1.384   0.2037  
## Dose            -7.155      3.171  -2.257   0.0540 .
## recipWt:Dose   690.659    351.829   1.963   0.0853 .
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.181 on 8 degrees of freedom
## Multiple R-squared:  0.5321,	Adjusted R-squared:  0.3566 
## F-statistic: 3.032 on 3 and 8 DF,  p-value: 0.09314
```



---

## Using the App

This application is used by inputting the person's weight in kg and amount of the drug in mg. The application calculates the dose by dividing the amount of drug by the weight. It also calculates the recipWt by taking 1 over the weight in kgs. 

The application then predicts the maximum dose and the prediction interval. The prediction interval is appropriate because the extremes of the lowest and highest possible dose are important for the safety of the patient.




