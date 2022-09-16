---
aliases: [grid-column, grid-row]
---
# grid-column Property

```css
.container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    grid-template-rows: 1fr 1fr;
}

.green {
    grid-column: 1/4;
}
```

![[Pasted image 20220911042228.png]]

Now the items span within 3 grid columns. 1/4 is just the starting line to ending line. 
We could also use `grid-row` for this one. 
```css
.green {
    grid-row: 1/4;
}
```

The problem with this is that if you declare the last item as 1/4, then it will wrap all the way up at th beginning to staisfy it. What we could do is to replace it with `span` unit
```css
.green {
    grid-row: span 3;
}
```

In this, the positioning will not be [[Justify-Align Grid Item]] but `justify-self` and `align-self`
```css
.green {
    grid-row: span 3;
    justify-self: center;
    align-self: center;
}
```
