# Column Value Conversion
Using [[Pandas]], this is relatively easy using [[Lambda]] expressions. 
![[Pasted image 20220727050311.png]]

We want to convert the KM to Miles so we need to divide each value by 16, we could just [[Creating New Columns|create columns]] instead and calculate it there but one way is to use `apply()` method

```python
dataframe["Odometer (KM)"] = dataframe["Odometer (KM)"].apply(lambda x: x/16)
```

Basically what we are doing here is we are [[Overriding Data]] and apply a [[Lambda]] that takes a parameter x which is the past value and dividing this value by 16 then returning it. 