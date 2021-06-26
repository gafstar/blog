---
title: "Handling Missing Values"
date: 2021-06-01
categories:
- Exploratory Data Analaysis, Machine Learning
tags:
- Python, R
keywords:
- Missing Values
#thumbnailImage: //example.com/image.jpg
---
Missing values ​​are difficult to deal with, and there is no better way to deal with them. It depends on different scenarios that are random and in some cases nonrandom to the data. First, let us have a clear understanding of what we mean by missingness in data.
<!--more-->

#### _Missing Data Mechanisms_

Missing values ​​are difficult to deal with, and there is no better way to deal with them. It depends on different scenarios that are random and in some cases nonrandom to the data. First, let us have a clear understanding of what we mean by missingness in data.

Missing values can be indicated in different ways. For instance, indicating a missing integer with `-9999`, `-999`, `-99` or `-9`, `999`, `???`, `?`, `np.inf` and `N/A`. `Unknown` is common or sometimes a conventional method is used for indicating floating-point missing value with  NaN (Not a Number) in python and NA (Not Available) in R programming. Sometimes you may see zero on some variables, therefore, it is a good idea to take a closer look at those variables as it might be invalid or a missing value.  

It is imperative to think about missing data during our analysis. Because, if we fail to take into account our analysis might be futile and if the data is fed to an algorithm, the bias will result in biased algorithms leading to biased decisions.

Before we start imputing missing values it is a good idea if we can visualize the data, so that we may be able to detect the missing values like -9999 which may appear as outliers compared to other values depending on the dataset variables domain.

The following general missingness mechanisms will give us some idea:

1.  __Missing completely at random (MCAR):__ This can be summarized as if your value  is completely missing  a variable at random, then by throwing out the cases of missing data, you will not miss much information or bias your inferences. A safe maximum threshold for missing data is 5% of the total. If a certain feature is missing more than 5% then you should probably discard that feature or collect more information.
You can confirm this case by partitioning the data into two parts: one set containing the missing values and the other set containing non-missing values. After partitioning use the t-test of mean difference to check whether there exist any difference in the sample between the two datasets.

2.  __Missing at random (MAR):__ Here missingness is not completely random.This means that the probability that a variable is  missing depends only on the available full information. In such cases, it is acceptable to 
exclude the missing value (i.e to treat them as NA or NaN). [expand on this explanation]
These are not randomly missing across observations but are distributed within one or more sub-samples. If the missing values are not randomly distributed across the observation, it is problematic. Therefore, they can be ignored by performing data imputation to replace them.

3.  __Missing that depends on unobserved predictors:__ This arises when the missing data depends on some unrecorded information. For example, suppose there is a pattern in the missingnes that correlates to another predictor, it would reveal that relationship and the variable and the other unknown predictor. Therefore, the missingness of data is not at random, therefore, it has to be explicitly addressed in modeling by choosing robust algorithms to missing values.
4.  __Missing that depends on the missing value itself:__ This is a difficult situation where the probability of missingness depends on the probability of the variable itself. For instance, if you are dealing with a time series data and you see a missing value on the data that might depend on the previous time, that might mispredict seasonality and pattern on the data.

Deciding on best analysis strategy to yield the least biased estimates
    1.  __Deletion Methods__
            + Listwise Deletion, Pairwise Deletion
    2.  __Single Imputation Methods__
            + Mean/Median/Mode substitution, dummy variable (constant) method, single regression
    3. __Model-Based Methods__
            + Maximum Likelihood, Multiple Imputation

_Handling Datasets Containing Missing Values:_


__1. Listwise Deletion (AKA Complete Case Analysis)__

Involves removal of all events (rows) with incomplete data (NA’s, NaN’s) for any feature. This reduces the effective sample size, which in turn, reduces the statistical power for hypothesis testing to unacceptably low values that lead to biased inference. Listwise deletion assumes the data are MCAR, which is not often the case in the real world. So we should be very careful in dealing with listwise deletion.
```python
# removing all the missing values
my_data.dropna(inplace = True)
```
```R
new_data <- na.omit(my_data)
```
_Advantages:_
+ Simplicity
+ Comparability across analysis

_Disadvantages:_
+ Reduces statistical power (because it lowers the number of records)
+ Doesn’t use all information
+ Estimates may be biased if data not MCAR

__2. Pairwise Deletion (AKA Available Case Analysis):__ 

Pairwise attempts to minimize the loss of information that occurs in listwise deletion. Think of it as a correlation matrix where the correlation measures the strength of the relationship between the available data of two pairs of variables.

_Advantages:_
+ Increases statistical power because it keeps as many records as possible

_Disadvantages:_
+ Similarly to listwise deletion estimates may be biased if data not MCAR
+ Can’t compare analysis because of sampling different variables each time

__3. Zero/Constant Imputation__

Involves substituting the missing values with zero or a constant value such as mean.
    
_Advantages:_
+ Uses all available information about the missing observation

_Disadvantages:_
+ Leads to biased estimates
+ Not theoretically driven

```Python 
# Replace missing values with a constant number
my_data['col_name'].fillna(10, inplace=True)
```
```R
# missing values col_1 will be filled with 10
my_data$col_1[is.na(my_data$col_1)] = 10
```
__4. Mean/Median/Mode Imputation:__

In mean, median or mode imputation, the mean, median or mode of all values for the same feature is calculated and then imputed to the missing values. Mode imputation is appropriate to nominal and categorical values. 

_Advantages:_
+ Uses the whole data

_Disadvantages:_
+ Reduces variability 
+ Ignores relationship between variables which weakens covariance and correlation estimates

```Python 
#  For python dataframe
#  Impute the mean/median/mode for each variable
my_data.fillna(mydata.mean())
my_data.fillna(mydata.median())
my_data.fillna(mydata.mode())
```
```Python
#For Python array data structure
# get the mean of columns you need
cols_mean = np.nanmean(my_array, axis = 0)
# Find the indices where you want to replace
indices = np.where(np.isnan(my_array))
```
           
```Python
# Replace the column means in the indices
My_array[indices] = np.take (cols_mean, indices[1])
```
```R
na_mean(my_data, option = 'mean')
na_mean(my_data, option = 'median')
na_mean(my_data, option = 'mode')
```
```R 
impute(data, method = "mean")   # method = either "mean/median/mode"
```

__5. Multiple Imputation__

One motivation of multiple imputation is to increase statistical power by increasing the    number of observations used. Multiple imputation incorporates information from all the variables in the dataset  to derive values that would be imputed in the place of the missing values. Instead of filling in a single value for each missing value, a set of plausible values that closely represent the uncertainty of each of the imputed missing values. The general, oversimplified, procedure can be summed in three steps: Impute, Analyze and Pool.

1. __Impute:__ Missing values are imputed using a specified regression model. It is repeated m times, resulting in m separate dataset 
2. __Analyze:__ Analysis is performed within each dataset 
3. __Pool:__ The results are pooled into one estimate
![Insert Image](imputation.jpg)

_Advantages:_
+ Variability due to sampling and due to imputation are more accurate
+ Increases precision
+ Resistant to outliers

_Disadvantages:_
+ Tedious coding
+ Liable to making errors when specifying models
          
__6.  Regression Imputation:__ 

A regression model is fitted for the variables with missing values. Based on the resulting model, a new regression model is then fitted and is used to impute the missing values for each variable.

_Advantages:_
+ Uses all information

_Disadvantages:_
+ Overestimates model fit and correlation estimates
+ Weakens variance
+ May impute values which are out of the possible range for a variable

This can further be classified into two: Deterministic and stochastic regression imputation.

__6.1 Deterministic Regression imputation:__

Here a linear regression function is computed in which the feature with missing value is dependent variable and the other features would be independent variables. The residual (i.e. error term) The estimate     of the dependent variable will be imputed in the missing value. 
```R
install.packages("mice") # installing the mice package
library("mice") # load mice package
```
```R
# Multiple imputation using deterministic regression
my_data_imputed<- mice(my_data, method = "norm.predict", m = 5) # 
my_data_imputed <- complete(my_data_imputed) # store data
```
For Linear regression we use ‘norm.predic’ for the method argument. The default number of imputation is 5, however, you are free to change the value.

__6.2 Stochastic Regression Imputation:__

This is a two step process which includes regressing from the other variables and adding an extra step of augmenting  each predicted score with residual term. The residual term is normally distributed with a mean of zero and variance equal to the residual variance of the predictor on the outcome.

_Cons:_
+ Stochastic regression may lead to implausible values. That is the variable to be imputed may be restricted to certain values (i.e only positive or negative value)
+ Stochastic regression imputation leads to poor results when data is heteroscedastic. This assumes that the random error has on average the same size for all parts of the distribution.
```R
install.packages("mice") # installing the mice package
library("mice") # load mice package

# Multiple imputation using deterministic regression
my_data_imputed<- mice(my_data, method = "norm.nob", m = 5) # 
my_data_imputed <- complete(my_data_imputed) # store data
```
```Python
import fancyimpute
mice = fancyimpute.MICE(verbose=0)
X_train_fancy_mice = mice.complete(X_train)
```
We have changed the method argument from ‘norm.predict’ to ‘norm.nob’ for stochastic regression imputation.
    
__7.  Hot-Deck:__ 

This method is one of the simplest single-imputation methods used to 
replace missing values randomly from background attributes which are selected by the user and are maximally similar to the missing one.

Here are some steps to follow when dealing with multiple variables containing missing values in a dataset:
1. First rank the variables by percent of missing information.
2. Begin imputing one variable at a time on those that has least MV
3. Retain and use the newly substituted values in the model-building process for each subsequent variable
4. Use every variable in building imputation models and discard the lower ranked variables with MVs.
5. In evaluating model based imputation, compare the pre-imputed means and standard deviation (based on the full information after deleting the MV’s) with the post-imputation values. If imputation is successful, there will be little or no significant difference in these mariginals.

__Sources:__

[Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html) _by Jake Vanderplas_

[Missing Values in Data](https://www.statisticssolutions.com/dissertation-resources/missing-values-in-data/) _Statistics Solutions_

[Missing Data Imputation](http://www.stat.columbia.edu/~gelman/arm/missing.pdf) _Data Analysis Using Regression and Multilevel/Hierarchical Models by Andrew Gelman et. al_

[Missing Data & How to Deal: An overview of missing data](https://liberalarts.utexas.edu/prc/_files/cs/Missing-Data.pdf) _by Melissa Humphries_

[Regression Imputation (Stochastic vs. Deterministic & R Example)](https://statisticsglobe.com/regression-imputation-stochastic-vs-deterministic/) _by Joachim Schork_

 [A data set with missing values in multiple variables](https://stats.stackexchange.com/questions/266296/a-data-set-with-missing-values-in-multiple-variables) _Stackexchange_