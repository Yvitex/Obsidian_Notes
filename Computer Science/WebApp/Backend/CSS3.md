# CSS3
There are alot of features in [[CSS]] new version
Though some of it is not supported yet by some browser as said in this [reference website](https://www.w3schools.com/cssref/css3_browsersupport.asp)
In that case, we need to use Prefixes to use them

![[Pasted image 20220904175004.png]]

We could check the compatibility with [caniuse](https://caniuse.com/)

An example of CSS3 new properties are transition property
```css
div {
	transition: all 1s;
}

div:hover {
	transform: scale(102%);
}
```

This will cause the scale to scale by 1s and not instantly
