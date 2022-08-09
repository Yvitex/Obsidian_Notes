# Proper way how
This is how to convert your [[Dataframe (Pandas)|dataframe]] to a [[Matplotlib module]]'s plot. In this way we could create the most flexible plot with all capabilities and ability to [[Customise the Plot]]

In this example we use a [[Scatter Plot (Pd)]]
![[Pasted image 20220729052411.png]]

follow the [[Matplotlib's Workflow]]
Prepare in this case we [[Import Data from CSV to Dataframe]] stored in dataframe variable
Next is  to create the figure.
```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=[10, 6])
```

To plot the data, we use the axes directly. we set this into a variable for a later use for [[Adding some Legends]]
```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])

```
![[Pasted image 20220729083116.png]]

We coudl customize it by [[Setting the Label and Title of the Plot]]
```python
label_setting = {
     "color": "White",
     "fontsize": 15
}

title_setting = {
    "color": "White",
    "fontsize": 20
}

fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])
ax.set_title("Cholesterol per Age", title_setting)
ax.set_xlabel("Age", label_setting)
ax.set_ylabel("Cholesterol", label_setting)
```

![[Pasted image 20220729083352.png]]

Then changing the [[Customize Ticks|.tick_params()]]
```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])
ax.set_title("Cholesterol per Age", title_setting)
ax.set_xlabel("Age", label_setting)
ax.set_ylabel("Cholesterol", label_setting)
ax.tick_params(color="white", labelcolor="white")
```

![[Pasted image 20220729083522.png]]

We could also customize it further by [[Adding some Legends]]
```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])
ax.set_title("Cholesterol per Age", title_setting)
ax.set_xlabel("Age", label_setting)
ax.set_ylabel("Cholesterol", label_setting)
ax.tick_params(color="white", labelcolor="white")
ax.legend(*scatter.legend_elements(), title="target")
ax.axhline(y=over_50["chol"].mean(),
           linestyle="--")
```
![[Pasted image 20220729083635.png]]

