---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 06-Supervised-Learning-III.md in _episodes_rmd/
title: 'Supervised Learning III: regularized regression'
author: "Jorge Perez de Acha Chavez"
questions: 
- "Are there any improvements to the regression algorithm?"
objectives: 
- "Learn improvements to the regression algorithm."
keypoints: 
- "Lasso regression can be used to identify key variables."
output: html_document
---





## Supervised Learning III: regularized regression

When performing linear regression, instead of minimizing the MSE, you can add other constraints that will stop the model parameters from shooting up too high. Lasso regression and ridge regression are a few examples. Your instructor will write several equations on the board to explain these constraints and all the necessary information is also in [this glmnet vignette](https://web.stanford.edu/~hastie/glmnet/glmnet_alpha.html). You'll use the glmnet package to fit a lasso regression to the data:



~~~
x = as.matrix(subset(gm, select=-life))
y = gm$life
fit = glmnet(x, y)
plot(fit, label=TRUE)
~~~
{: .language-r}

> ## Discussion
>
> Interpret the above figure. For a hint, check out [this part of Hastie & Qian's vignette](https://web.stanford.edu/~hastie/glmnet/glmnet_alpha.html#qs):
>
{: .discussion}

### Lasso regression and cross validation

The glmnet API makes k-fold cross validation pretty easy. Give it a go and find the best choice for the hyperparameter lambda:


~~~
cvfit = cv.glmnet(x, y, alph=1)
print(cvfit$lambda.min)
plot(cvfit)
~~~
{: .language-r}

### Feature selection using lasso regression

One great aspect of lasso regression is that it can be used for automatic feature selection. Once you have used k-fold CV to find the best lambda, you can look at the coefficients of each variable (for that value of lambda) and the variables with the largest coefficients are the ones to select.



~~~
x = as.matrix(subset(gm, select=-life))
y = gm$life
fit = glmnet(x, y, alpha=1)
plot(fit, label=TRUE)
~~~
{: .language-r}

> ## Discussion
>
> 1. What is the most important variable in the above?
> 2. Why would automatic variable selection be useful?
> 3. What are potential pitfalls of automatic variable selection?
>
{: .discussion}
