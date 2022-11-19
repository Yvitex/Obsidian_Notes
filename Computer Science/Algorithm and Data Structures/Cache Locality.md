---
aliases: []
---
# Cache Locality

RAM is generally composed of cells where each cell could hold 8 bits or 1 byte of data and each cell is marked with a [[Memory address]]. Each [[Memory address|memory location]] if connected individually with the [[Memory Controller]] that could access each cell from any point, hence the term ==random access== 

![[Pasted image 20220802035452.png]]
```ad-Attention
title: But...
collapse: open
Even though it could access any [[memory address]] from any point, it is still slower when accessing data cell far from the recently accessed. For example, accessing the [[memory address]] 10023223 would take longer time if it came from [[memory address]] 0 but would be faster if the recent is 10023222
```

Cache locality is the fact that there is a high probability that successive items will be stored in the [[CPU Cache]] therefore being faster. 











# Metatags
###### Related: [[Random Access Memory]]
###### Tags: 
###### Source: 

---