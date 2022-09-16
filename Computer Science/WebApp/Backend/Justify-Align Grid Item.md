# Justify-Align Grid Item
To position the items horizontally depending on the size of their container we could use
```css
.container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 2fr;
    justify-content: end;
}
```

We could also use:
- strech - default
- center
- end
- start

The same goes for vertical, we could align it using 
```css
.container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 2fr;
    align-items: flex-start;
}
```

Other value include:
- flex-start
- strech
- flex-end
- center