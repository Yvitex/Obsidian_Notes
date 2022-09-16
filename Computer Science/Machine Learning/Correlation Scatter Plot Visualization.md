# Creating a Scatter Plot for Correlation
## Given
![[Pasted image 20220606123158.png]]

Find the [[Correlation]] plot for NOX or nitrogen oxide emission and DIS or distance away from emplyment center. Refer to [[Data Exploration]]

## Two ways to Do this
### Matplotlib
[[Matplotlib module]]

Simly create a [[Scatter Plot]] using `plt.scatter()`  with Nox and Dis as the parameter

```
import matplotlib.pyplot as plt

plt.figure(figsize=[15, 10]) #Change Size
nox_dis_corr = data["NOX"].corr(data["DIS"]) #value of correlation
plt.scatter(data["DIS"], data["NOX"], s=100, color="green", alpha=0.6) # mail [[scatter plot]]
plt.title(f"DIS vs NOX (Correlation: {round(nox_dis_corr, 2)})") # title
plt.xlabel("Distance from the Employment Center", fontsize=14) 
plt.ylabel("Amount of Pollution", fontsize=14)
plt.show()
```

![[Pasted image 20220609142436.png]]

As we could, there is a negative correaltion between this 2 variables. It basically means, the farther you from employment centers, the less the pollution tends to occur and this makes sense. We could notice the fact that the plot moves in a downward slope that supports the [[Negative Correlation]] 

### Seaborn
We can do the same thing with less code using [[Seaborn Module]] through `sns.jointplot()`, this works the same with [[Scatter Plot]] but with more design and customization

```
import seaborn as sns

sns.set()
```

We use `sns.set()` to reset the design from the past codes. 
```
import seaborn as sns

sns.set()
sns.jointplot(x= data["DIS"], y= data["NOX"])
```
![[Pasted image 20220609143113.png]]

Joinplot already created a histogram as the [[Scatter Plot]] along with the labels without directly stating it. 
We could set the style using `sns.set_style()` which can be 'white', 'dark', 'whitegrid', etc

```
import seaborn as sns

sns.set()
sns.set_style('dark')
sns.jointplot(x= data["DIS"], y= data["NOX"])
```
![[Pasted image 20220609143404.png]]

The bacground gets slightly darker.
Now, we could also change the size or style  with `sns.set_conctext()` 

```
import seaborn as sns

sns.set()
sns.set_style('dark')
sns.set_context('talk')
sns.jointplot(x= data["DIS"], y= data["NOX"])
```

![[Pasted image 20220609143714.png]]

Now, we could add more style to promotive visibility and ease for the viewer, we could use `height=` to change the over all graph size and `s=` to change the plot size
```
import seaborn as sns

sns.set()
sns.set_style('dark')
sns.set_context('talk')
sns.jointplot(x= data["DIS"], y= data["NOX"], s=200, height= 10, color='indigo')
```
![[Pasted image 20220609144709.png]]

We could also see the density of the [[Scatter Plot]] usiing a keyword argument `joint_kws={"alpha": 0.5}`

```
import seaborn as sns

sns.set()
sns.set_style('dark')
sns.set_context('talk')
sns.jointplot(x= data["DIS"], y= data["NOX"], s=200, height= 10, color='indigo', joint_kws={"alpha": 0.5})
```
![[Pasted image 20220609145012.png]]

We could also set the `kind=` attribute to change the type of the graph rather than [[Scatter Plot]]
```
import seaborn as sns

sns.set()
sns.set_style('dark')
sns.set_context('talk')
sns.jointplot(x= data["DIS"], y= data["NOX"], height= 10, color='indigo', kind='hex')
```

One thing to note here is that it doesn't work with `s=` because it was not a [[Scatter Plot]] anymore and also `joint_kws={"alpha": 0.5}` does not look good with it so i removed it

![[Pasted image 20220609145420.png]]

Here, we could see the density of the graph through its color. It's LIT!!

Other kinds include, "scatter" | "kde" | "hist" | "hex" | "reg" | "resid"|'reg',


In the examples above, it shows a clear correlation with each other using figures, but what does it looks like if our correlation is senseless.

Read: [[Senseless Correlation]]


We can also create multiple [[Scatter Plot]] at once using [[Seaborn Module]], read it at [[Multiple Scatter Plot and Linear Regression with Panda's DataFrame]]

