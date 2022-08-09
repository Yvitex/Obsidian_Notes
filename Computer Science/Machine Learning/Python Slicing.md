# Python Slicing
A way to extract specific sequence of string and array
```python
string = "abcdefg"
```

if we do this
```python
string = string[:-2]
```

The output would be: "abcde", it removes the last 2 letters and print the rest, if we did this
```python
string = string[:2]
```

the output would be: "ab". It will only print the first 2 letters. 

For instance you have this [[Numpy Module|ndarrays]]
![[Pasted image 20220801095402.png]]


We could slice it using the following:
If we want to slice from index 0 to the 10th item do
```python
variable[:10]
```
![[Pasted image 20220801095452.png]]

If we want to slice from 5th index to the 10th item
```python
variable[5:10]
```
![[Pasted image 20220801095559.png]]

If we want to print from first index to the 10th item while jumpring per 2 indexes
```python
variable[0:10:2]
```
![[Pasted image 20220801095809.png]]

If you want to print the second column do this
```python
variable[:, 1]
```
![[Pasted image 20220801095910.png]]

If we want to print only the first 5 items in the second columns
```python
variable[:5, 1]
```
![[Pasted image 20220801100102.png]]
