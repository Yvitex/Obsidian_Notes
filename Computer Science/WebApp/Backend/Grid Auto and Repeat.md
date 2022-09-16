# Grid Auto and Repeat
```css
.container {
	display: grid;
	grid-gap: 20px;
	grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
	grid-template-rows: 1fr 2fr;
}
```

Instead of writting multiple fr units, what we could do is to use the `repeat` and it will do the same thing
```css
.container {
	display: grid;
	grid-gap: 20px;
	grid-template-columns: repeat(5, 1fr);
	grid-template-rows: 1fr 2fr;
}
```

We could also use `auto` unit in order to size the divs according to the item inside them
```css
.container {
	display: grid;
	grid-gap: 20px;
	grid-template-columns: 1fr auto;
	grid-template-rows: 1fr 2fr;
}
```

![[Pasted image 20220911034248.png]]

