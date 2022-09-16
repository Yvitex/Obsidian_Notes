# Using Pandas Imputation and Deletion
THis [[Dataframe (Pandas)|dataframe]] have some Nan. We could detect it using [[Describe DataFrame|info()]] method or we could use some other [[Null Value Detection]]
```python
import pandas as pd

data = pd.read_csv("file.csv")
data.isna().sum()
```
![[Pasted image 20220730101120.png]]

Make is only a string category. We could replace it as a "missing" string using [[Dealing With Missing Values|fillna()]]
```python
car_sales_missing["Make"].fillna("Missing", inplace=True)
```

The same is the color string classification
```python
car_sales_missing["Colour"].fillna("Missing", inplace=True)
```

The Odometer is a range of integers and we could acturlly just find the [[Mean]]
```python
car_sales_missing["Odometer (KM)"].fillna(car_sales_missing["Odometer (KM)"].mean(), inplace=True)
```

The door is a category, and by [[Counting Frequently Occuring Value]]
```python
car_sales_missing["Doors"].value_counts()
```
![[Pasted image 20220730110850.png]]

We could say that most of the time, it will have the value of 4 so we could assume that other will be the same
```python
car_sales_missing["Doors"].fillna(4, inplace=True)
```

Counting the missing again
```python
car_sales_missing.isna().sum()
```
![[Pasted image 20220730111012.png]]

Price is the only left and because it is very important, it is the [[Target]] label, we drop those missing values to oblivion
```python
car_sales_missing.dropna(inplace=True)
```

```ad-Upset
title: Note to Self
collapse: open
You can't call dropna() in a single column like car_sales_missing["Price"].dropna(). Instead what we could do is car_sales_missing.dropna(subset=["Price"], inplace=True)
```

Now we have 0 null values, we could now proceed to [[Convert classification string values into Numerical Data]]


