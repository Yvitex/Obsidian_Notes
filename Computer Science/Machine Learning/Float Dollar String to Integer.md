# Object to Integer
One of the most common problem in [[Data analysis]] is that sometimes, our number is written in dollar notation like $400,000.00. It have $ , and . which makes it a string or object rather than integer

![[Pasted image 20220726172539.png]]

To make this right, we could do this. According to this [stackoverflow solution](https://stackoverflow.com/questions/44469313/price-column-object-to-int-in-pandas)
We could do this [[Algorithm]]. HEre we will use [[Regex]] patterns to do this for us. 
```python
dataframe["Price"] = dataframe["Price"].str.extract("(.+)\.[0-9]+").astype(str)
```

We extract out the period and the next number after it. 
Maybe we could remove the astype as there is no conversion happening. Next is to remove the strange symbols
```python
dataframe["Price"] = dataframe["Price"].str.replace("[$\,\.]", "").astype(int)
```

We replace those strange symbols with null string then conver it to int. alternatively, we could do this [[Python Slicing]] technique

```
dataframe["Price"] = dataframe["Price"].str[:-2].astype(int)
```

![[Pasted image 20220726173045.png]]



