# Figma Basics
One of the greaterst program when it comes to [[Sketching]]

The first thing we need to consider when creating a design is to create a guide using the layout grid panel
![[Pasted image 20220717033934.png]]

Bootstrap have 12 columns too, and we apply 100 pixel margin for a nice spacing. 
![[Pasted image 20220717034030.png]]

This will act in palcing our icons and images.

![[Pasted image 20220717040121.png]]

We could then create a text by pressing T, the font format below is merriweather which is good in making authoritative text, allign it with the layout goide and pixel size is 36px. Smaller than the image. 
![[Pasted image 20220717040710.png]]

Secondary paragraphs with friendly tone could be a friendly font such as *open sans* which are more readable. We allign it to the main text, but we could also scale it smaller than them with one columns apart. The first part must be alligned. 
![[Pasted image 20220717041314.png]]

We also use *auto height* to make the space adapt to the height of the text. 
We simply created a button by creating a new frame which we renamed as button, fill it with some color and input a text inside it
![[Pasted image 20220717043118.png]]

But once we resize it, it will look outrageous, the thing we could do it to apply a constrain in the text to both center. THis is the same like when we are creating a [[User Interface Basics]] in java
![[Pasted image 20220717043238.png]]

```ad-Notice
title: Center Center
collapse: open
Left right and top bottom contrains won't work when trying to make the text responsive in without changing the size of the text in the center

```
![[Pasted image 20220717043518.png]]

What about auto layout. It is useful in setting spaces around an element like constrains, now we set the button to have a horizontal padding of 40 and vertical of 16.
![[Pasted image 20220717044450.png]]

They are both placed in a *hug* which means it doesn't grow when resizing but grows when we add content
![[chrome-capture-2022-6-17.gif]]

We could group the 3 component, button, paragraph and heading by right clicking and selecting *frame selection*. The reverse of the hug content is called *fixed length*, it only means that it doesn't grow when we add more content. We set the new frame as horizontally fixed but vertically hugged so that we could add more items in it. Because we set the horizontal as fixed, we need to indicate the constrains manually, which is left an right if we want to resize it when we scale. 

After we scale, we may set the inner content to another type called *Fill container*, where the text fills in the whole of its container, so when we resize that container, it automatically wraps
![[chrome-capture-2022-6-17 (1).gif]]

We could set the imaegs to left and right constrains which is enough to make them responsive
![[Pasted image 20220717050258.png]]

Then we could make a navigation text, make it into their own frame and using the allignments, allign it to the shapes like logo
![[Pasted image 20220717050655.png]]


Make components; simply be pressing the create component in the top button. This will enable us to reuse the components.

#design 