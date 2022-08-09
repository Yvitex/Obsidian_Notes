---
aliases: [ax.bar()]
---
# Bar Graph
To do this in [[Matplotlib module]], we just need to call the `bar()` on its axes, refer to the [[Anatomy of Matplotlib Plots]]. We could work with Python Dictionary in this case 

```python
import matplotlib.pyplot as plt

shit_taste = {"Kumo desu ga Nani ga?": 8, "Mobusekai": 8.5, "Disciple of the Lich": 9}

fig, ax = plt.subplots()
ax.bar(shit_taste.keys(), shit_taste.values())
```

![[Pasted image 20220728145831.png]]

We could also do horizontal bar graph
```python
shit_taste = {"Kumo desu ga Nani ga?": 8, "Mobusekai": 8.5, "Disciple of the Lich": 9}

fig, ax = plt.subplots()
ax.barh(shit_taste.keys(), shit_taste.values())
```

THis will sprout a type error: dict is not hasable. Transform the key value pair to list
```python
shit_taste = {"Kumo desu ga Nani ga?": 8, "Mobusekai": 8.5, "Disciple of the Lich": 9}

fig, ax = plt.subplots()
ax.barh(list(shit_taste.keys()), list(shit_taste.values()))
```
![[Pasted image 20220728152912.png]]

