# Improving the Model
![[Pasted image 20220610094813.png]]

Here is the [[Advanced Data Analysis Histogram|Histogram]] for our price data in [[First Step of Data Exploration]]. We could see that there are outliers and have a high skewness compared to normal distribution a.k.a. bellcurve

![[Pasted image 20220610095025.png]]

We could actually see the skeness of this data by using [[Pandas]] `.skew()` method

```
data['PRICE'].skew()
```

Output: 1.1080984082549072

Normal distribition skewness is equals to 0. 

To improve our model, we could rely on something called [[Data Transformation]]

