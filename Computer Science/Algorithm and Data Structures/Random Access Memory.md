---
aliases: [ram]
---
# Ram
![[Pasted image 20220906174024.png]]
A temporary and volatile memory use to store data fast in a computer system.

RAM could have many types such as [[SDRAM]], [[RDRAM]], [[DDR SDRAM]] and [[DDR SDRAM]]. DDR RAm is relatively new compared to SD RAM.  RAM have their own speed and capacity. 

We could notice that each one of them have the idea of [[DRAM]]


RAM is generally composed of cells where each cell could hold 8 bits or 1 byte of data and each cell is marked with a [[Memory address]]. Each [[Memory address|memory location]] if connected individually with the [[Memory Controller]] that could access each cell from any point, hence the term ==random access== 

![[Pasted image 20220802035452.png]]
```ad-Attention
title: But...
collapse: open
Even though it could access any [[memory address]] from any point, it is still slower when accessing data cell far from the recently accessed. For example, accessing the [[memory address]] 10023223 would take longer time if it came from [[memory address]] 0 but would be faster if the recent is 10023222
```

When stoing integers in a program like
```js
let a = 1
```

Because an integer has 32 bit of data, it will be divided into 4 cells.  Meaning if they can't hold data anymore to store this numbers, like
```js
math.power(10, 100000000)
```

It will just simply say infinity because it cannot hold the data. 

Here is a video discussing How Ram works
<iframe width="560" height="315" src="https://www.youtube.com/embed/fpnE6UAfbtU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
