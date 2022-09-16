---
aliases: [minmax, auto-fill]
---
# Minmax and auto-fill Grid
Grids are not so very responsive 
```css
.container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: 1fr 1fr 2fr;
    grid-template-rows: 1fr 1fr;
}
```

![[Pasted image 20220911040258.png]]

What we could do is to use the Repeat property then use the auto-fill so that the items wrap
```css
.container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: repeat(auto-fill, 300px);;
    grid-template-rows: 1fr 1fr;
}
```

![[chrome-capture-2022-8-11.gif]]

instead of using pixel values, we could use `minmax()` to aid us
```css
.container {
    display: grid;
    grid-gap: 20px;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));;
    grid-template-rows: 1fr 1fr;
}
```

![[chrome-capture-2022-8-11 (1).gif]]

This means that use 300px for the minimum value and if the viewport decrease, use 1fr
