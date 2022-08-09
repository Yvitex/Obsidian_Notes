# Label from String to Binary
Machine does not understand string, but it understand [[Binary]] values.
For instance that we have 10222 samples with 120 different categories. We need to covnert those 10222 samples into an array of 0's and 1's in a array with a length of 120

![[Pasted image 20220806120548.png]]

First  is to extract individual row labels into an array
```python
breeds = label["breed"]
breeds = np.array(breeds)
len(breeds)
```

The length should be 10222, the same number as the rows
Extract then the unique values from the breeds collection.
```python 
unique_breeds = np.unique(breeds)
len(unique_breeds)
```

The length here should be 120. The same number as the total class. 
Create now an array of true and false by comparing these 2 variables, the original set of breeds and the unique breeds
```python
transformed_breeds = []
for i in range(len(breeds)):
	transformed_breeds.push(breeds[i] == unique_breeds)
len(transformed_breeds)
```

The length should be 10222, which concedes the number of our rows. An alternative to this is throug [[Python List Comprehension]]
```python
transformed_breeds = [breed == unique_breeds for breed in breeds]
```

Now to make it a number. just simply transform it using `astype(int)`. get the index using [[Numpy Unique Numbers|np.argmax()]]

```python
indexer = 2
print(breeds[indexer])
print(f"At index {transformed_breeds[indexer].argmax()}")
print(transformed_breeds[indexer].astype(int))
```
![[Pasted image 20220806121304.png]]



