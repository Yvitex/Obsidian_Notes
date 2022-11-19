---
aliases: []
---
# Graphical Method
This is about making a plot of the function and then observe when the value cross the x axis. 

Here we have a [[Transcendental Functions]] in the formula of:
$$f(x) = e^{-x} - x$$
We will create a graph with our initial incremented values and on the otehr side, the values of the f(x) wherein we substituted the x with the inital incremented values. 

| x   | f(x)        |
| --- | ----------- |
| 0   | 1           |
| 0.2 | 0.61873075  |
|  0.4   | 0.27032004  |
|   0.6  | -0.05118836 |
|  0.8   |   -0.35067104  |

We could see that beyong 0.6, it is already negative, so f(x) must be close to 0 and not lower than 0. We will repeat this process but with lower increment between 0.4 to 0.6, maybe with a step of 0.01 until we get the values closest to 0. We will then try to plot the value of root in a lineary graph

![[Pasted image 20220922125054.png]]


## Algorithm

Basically, I created a program for it in [[Python]]
```python
def graphicalMethod(self, function, x, step, iteration):  
	if (function(x) > 0):  
		print("normal")  
		for index in range(iteration):  
			y = function(x)  
			print(f"y:{y}, x:{x}, step:{step}")  
			if (y < 0):  
				x = x - step  
				step = step * 0.5  
			x = x + step  
	
	else:  
		print("else")  
		for index in range(iteration):  
			y = function(x)  
			print(f"y:{y}, x:{x}, step:{step}")  
			if (y > 0):  
				x = x - step  
				step = step * 0.5  
			x = x + step
```

# Metatags
###### Related: [[Bracketing Method]], [[Transcendental Functions]]
###### Tags: 
###### Source: 

---