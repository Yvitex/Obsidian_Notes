---
aliases: [baseline grid, manuscript grid, column grid, modular grid]
---

# Grid Basics
Ancient societies use grid to neatly arrange the content of their texts. So basically, it is useful for placing things in an organized manner. 

To create a powerful graph with consistent spacing, we need to know about [[Base Unit]]. Why? All [[User Interface Basics|user interface]] elements are measured in those [[Base Unit]] to commit consistency. 

This is an example of incosistent measuring style in [[User Interface Basics|ui]] element
![[Pasted image 20220722153245.png]]

Proper [[Base Unit]] measurement will help us determine the padding of elements
![[Pasted image 20220722153431.png]]

The example above have a 16px padding in all sides that create this professional looking card element. 

Grids are made up of 3 parts
- Columns - The actual vertical line, can range from 12 columns in desktop, 8 to tablet and 4 or 6 on mobile, rember the [[Bootstrap]] css module? Well, this sort of arrangement will help us create responsive design
- Margins - space between the ends of of the grid to the end of the viewport
- Gutter - spacing of each columns.
![[Pasted image 20220722153620.png]]


## Types of Grids
There are 4 types of grids. 
#### Manuscript Grid
![[Pasted image 20220722153947.png]]

## Column Grid
The most common grid
![[Pasted image 20220722153620.png]]

This kind of grid makes it easy for us to divide elements for responsive application
![[Pasted image 20220722154054.png]]

#### Modular Grid
These have both horizontal and vertical lines
![[Pasted image 20220722154121.png]]

#### Baseline Grid
Creates a horizontal rhythm useful in positioning typography and [[User Interface Basics|ui]] elements. It is base on the [[Base Unit]], usually a 4px baseline grid. 
![[Pasted image 20220722154305.png]]

![[Pasted image 20220722154545.png]]

The baseline is base on the line height of the typography, If you have 16px fontsize, you may want to use a 24px baseline grid. Or if 24px font size, then 32 px line height.


To create a responsive design, we need to think about certain [[Grid Breakpoints]]


