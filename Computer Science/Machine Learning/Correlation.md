---
aliases: [Pearson]
---

# Pearson's Correlations
Collerations describe how strong a relationship between variables are. There are actually 3 types of correlation.

## 3 Types of Correlations
1. [[Positive Correlation]] - if x increase, y also increase
2. [[Negative Correlation]] - while x increase, y decrease
3. [[No Correlation]] -  without pattern or in a chaotic distribution


Take note that this correlationships in data visualization is somehow similar to [[Linear Regression]]


## Mathematical Formula
$$\rho_{xy} = corr(x, y)$$
$$-1.0 \leq \rho_{xy} \leq 1.0$$

Correlations are purposeful because it allows us to visualize the direaction and strength between the relationship data

## Python Code
[[Pandas]] module already has a method that output the correlation between variables and that is though the use of `x.corr(y)` method.

![[Pasted image 20220605154157.png]]

data from: [[Data Exploration]]

```
data["PRICE"].corr(data["RM"])
```
The output equates into: 0.695359947071539 which means it is [[Positive Correlation|possitively correlated]] 

```
data["PRICE"].corr(data["PTRATIO"])
```
The output will be : -0.5077866855375615 which means it is [[Negative Correlation|negatively correlated]]

the easiest way to calculate all data at once is using `dataframe_var.corr()`
```
data.corr()
```
![[Pasted image 20220606123158.png]]

We can see this diagonal region filled with highly correlated values
![[Pasted image 20220606123158 - Copy.png]]

Looking closely, it is obvious that they will have this correlation because they are correlating to themselves such as crime rate is highly correlated to crime rate resulting to a possitive correlation value.

![[Pasted image 20220606123158 - Copy (2).png]]

We could also see the redundancy in the half side, only the first half is important.

To remove the redundant parts, read [[Masking a DataFrame in Half]]
To visualize this data, read [[Correlation Matrix]]
Next is to read how to create a [[Scatter Plot]] to check distribution in [[Correlation Scatter Plot Visualization]]

## Why do we measure correlation?
- It is to avoid [[Multicollinearity]] which makes the relationship redundant, unreliable and nonsensical. This makes it hard for our variables to find the individual or unique contribution of the variables to the target. In our case, the price
- To identify strong correlations
- To identify and exlude irrelevant data

## Weakness of Correlations
- We can identify correlations all we want, but [[Correlations doesn't implicate causation.]] Not because one thing moves relative to another doesn't mean that this thing is that cause that causes the other move. 
- It only works on [[Correlations Problem on Linear Data|linear data]] 


Related: [[Data Exploration]]
