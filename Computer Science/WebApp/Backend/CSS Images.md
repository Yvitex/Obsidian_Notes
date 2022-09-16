# Images
[[CSS]] properties on images

One of the most important properties of images in css is the ability to be wrapped around text and we could do that using a property called `float`
```css
img{
	float: right;
}
```

![[Pasted image 20220904150330.png]]

Website made with love is a footer and we want it below the images, one of the most common properties use along side `float` is the `clear` property where we disable the wrapping of the text and make it looks like it is on a `block` display division element
```css
footer{
	clear: both;
	text-align: center;
}
```
![[Pasted image 20220904150524.png]]
