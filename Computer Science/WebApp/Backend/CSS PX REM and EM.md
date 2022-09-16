---
aliases: [px, rem, em]
---
# Sizes
A [[CSS]] concept about css sizes we could use in sizes etc.

if we have this [[HTML]]
```html
<p>Lorem <span>Ipsum</span></p>
```

If we set the p and span to the same pixels
```css
p {
	font-size: 16px;
}

span {
	font-size: 16px;
}
```

Then they will have the same size, if we use em instead
```css
p {
	font-size: 16px;
}

span {
	font-size: 2em;
}
```

Span will become double the size as em will base on the parent component size multiplied by our em value which is 16 *  2

Then if we use rem instead, instead of basing it to the parent element, we will bas eit to the root element
```css
p {
	font-size: 8px;
}

span {
	font-size: 2rem;
}
```

Span will remain the same size as 1 rem is equal to 32px

