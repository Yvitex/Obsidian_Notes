---
aliases: []
---
Installation is 
```shell
$ npm add sass
```

A special kind of css. So we have this component [[HTML]]
```js
return (
    <div className='categories-container'>
      {categories.map((data) => {
        return (
          <div className='category-container'>
            {/* <img /> */}
            <div className='category-body-container'>
              <h2>{data.title}</h2>
              <p>Shop Now</p>
            </div>
          </div>
        )
    })}
```

We will stule each div elements in a normal css like this
```css
.categories-container {
	background-color: red;
}

.categories-container .category-container {
	background-color: green;
}

.categories-container .category-container .category-body-container {
	background-color: blue;
}
```

SCSS will help us with this by allowing it to write in nested selectors
```css
.categories-container {
	background-color: red;

	.category-container {
		background-color: green;

		.category-body-container {
			background-color: blue;
		}
	}
}
```


# Metatags
###### Related: [[React]], [[Javascript]], [[CSS]], [[React Styling]]
###### Tags: #incomplete 
###### Source: 

---