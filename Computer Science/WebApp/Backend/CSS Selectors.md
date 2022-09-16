# Selectors
Different kinds of selectors in [[CSS]]
- .class
- \#id 
- element
- selector, selector : selects both selector
```html
<h1></h1>
<div></div>
<h2></h2>
```
- selector selector : selects the selector inside the first selector
```html
<h1>
	<div>
		<h2></h2>
	</div>
</h1>
```
- selector > selector : it selects the selector if it is a parent of the first selector
```html
<h1>
	<h2></h2>
</h1>
```
- selector + selector : it selects the element after the first selector
```html
<h1></h1>
<h2></h2>
```

- :hover
- :last-child - select the last child of an element
```html
<div>
	<p>First</p>
	<p>Second</p>
	<p>Last</p> <!-- this selects the last child-->
</div>
```

- :first-child
```html
<div>
	<p>First</p> <!-- this selects the first child-->
	<p>Second</p>
	<p>Last</p> 
</div>
```