# Workflow
[[Matplotlib module]]  basic workflow/
![[Pasted image 20220728110002.png]]


The first steps is to [[Creating Data and Plot]] including plotting the data
Second step is to [[Customise the Plot]]
Third Step is to [[Save and Share the plot]]

Create Data
```python
x = [1, 2, 3]
y= [13, 17, 31]
```

Create Plot
```
fig, ax = plt.subplots(figsize=[10, 10])
```
![[Pasted image 20220728121332.png]]

Plot data
```python
ax.plot(x, y)
```
![[Pasted image 20220728121408.png]]

Customize plot
```python
ax.set(title="test plot", xlabel="X-label", ylabel="Y-label")
```
![[Pasted image 20220728121837.png]]

Save:
```python
fig.savefig("image.png")
```
![[Pasted image 20220728121959.png]]


