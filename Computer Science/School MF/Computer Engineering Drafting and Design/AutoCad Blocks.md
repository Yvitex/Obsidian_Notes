---
aliases: []
---
# AutoCad Blocks
This insert synbols into your drawing using downloaded or your own created design. It is simply the collection of items combined to create a single entity. ![[Pasted image 20221003100553.png]]
Each of the block created are individual drawing stored in a folder with other files. To insert a block, press the insert in the block panel
![[Pasted image 20221003101326.png]]

When you insert a block, it is attached to the cursor, usually at the origin point (0, 0), this is called <u>Insertion Point</u>, After this insertion, a grip will be visible and this grip allows us to rotate, scale or move the block. 

Adding a drawinf file as a block would create a static reference, but for a reference that dynamically changes we could insert it using the command XREF, or External Reference Palette.

Alternatively, we could create our own block directly rather than creating a separate file then inserting it as a block. Use this method when you only want this block to appear inside that specific project, this can't be used on other drawing files. ![[Pasted image 20221003102047.png]]
Also, creating multiple drawing files to be inserted as a block is called <u>block library drawing</u>


Once it was created, then we could insert it. If we need to make this block as an independent component, then we could use the EXPLODE command. 

We could create block that displays some attribute using this command called ATTDEF

# Metatags
###### Related: [[AutoCAD]]
###### Tags: 
###### Source: 

---