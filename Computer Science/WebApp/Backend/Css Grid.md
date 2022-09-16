# Grid
Will help your website to become responsive also like [[CSS Flex Box]]
```.html
<div class="container">
	<div class="zone green">🦊</div>
	<div class="zone red">🐰</div>
	<div class="zone blue">🐸</div>
	<div class="zone yellow">🦁</div>
	<div class="zone purple">🐯</div>
	<div class="zone brown">🐭</div>
	<div class="zone green">🦄</div>
	<div class="zone red">🐲</div>
	<div class="zone blue">🐷</div>
	<div class="zone yellow">🐺</div>
	<div class="zone purple">🐼</div>
	<div class="zone brown">🐻</div>
</div>
```

We could create a container which holds different cards.
```css
.container {
	display: grid;
}
```

This won't do anything yet, we could add this line of code
```css
.container {
	display: grid;
	grid-template-columns: 300px 300px;
}
```

This will divide the items into 2 300px width columns
![[Pasted image 20220910053321.png]]

This is very not responsive, what we could use is `fr` unit like
```css
.container {
	display: grid;
	grid-gap: 20px;
	grid-template-columns: 1fr 1fr 2fr;
}
```

![[Pasted image 20220910053451.png]]

Use always use fr in grids to make it Responsive.
We could also use the `grid-template-rows` property in which it will define the size of the item vertically
```css
.container {
	display: grid;
	grid-gap: 20px;
	grid-template-columns: 1fr 1fr 2fr;
	grid-template-rows: 1fr 2fr;
}
```

![[Pasted image 20220911033632.png]]

This will cause a repeating in which the first the third and the fourth row didn't change, only the second

To make our lives more easier, we could use the [[Grid Auto and Repeat]]
There is also a property that will position each item inside the grid called [[Justify-Align Grid Item]], 

This thing is not responsive enough so there is a technique to make it look responsive and that is through the use of [[Minmax and auto-fill Grid]]

The items inside the grid could be individually modified in their scaling using [[Individual Grid Property]]
