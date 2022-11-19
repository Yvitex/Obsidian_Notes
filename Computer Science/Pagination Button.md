---
aliases: []
---
The first thing that we need to do is the [[HTML]] setup
```html
<div class="pagination">
      <ul>
        <!-- <li class="btn prev">
          <span><i class="fa-solid fa-angle-left"></i> Prev</span>
        </li>
        <li class="numb active"><span>1</span></li>
        <li class="numb"><span>2</span></li>
        <li class="dots"><span>...</span></li>
        <li class="numb"><span>4</span></li>
        <li class="numb"><span>5</span></li>
        <li class="dots"><span>...</span></li>
        <li class="numb"><span>7</span></li>
        <li class="btn next">
          <span><i class="fa-solid fa-angle-right"></i> Next</span>
        </li> -->
      </ul>
</div>
```

the [[CSS]] are as follows
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Poppins", sans-serif;
  }

  body {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 10px;
    background-color: #20b2aa;
  }
  
  .pagination ul {
    display: flex;
    background-color: #fff;
    padding: 8px;
    border-radius: 50px;
    color: #20b2aa;
  }

  .pagination ul li {
    list-style: none;
    line-height: 45px;
    text-align: center;
    font-size: 18px;
    font-weight: 500;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50px;
  }

  .pagination ul li.numb {
    height: 45px;
    width: 45px;
  }

  .pagination ul li.dots {
    font-size: 22px;
    cursor: default;
  }

  .pagination ul li.btn {
    padding: 0 20px;
  }

  .pagination ul li.prev {
    border-radius: 25px 5px 5px 25px;
  }

  .pagination ul li.next {
    border-radius: 5px 25px 25px 5px;
  }

  .pagination ul li.active,
  .pagination ul li.numb:hover,
  .pagination ul li.btn:hover {
    background: #20b2aa;
    color: white;
  }
```

This will be commented out. THe keytakeaway is that `active` class is the colorbackground that changes when we hover or when it is the page that is currently active. This will have a previous and next button, the numbers will be replaced so it doesn't matter. There are also dots in between numbers. 

![[Pasted image 20221029093551.png]]

Comment out the list tag inside the ul tag.

In [[Javascript]], create a function that will take the active page and the total page, call this element. Also, took the ul element inside pagination;
```js
let pagination = document.querySelector("ul");
const totalPage = 20;

function element (page, totalPage){
	
}

element(5, totalPage);
```

Totalpage with temporarily become 20, active page page temporarily 5. Now, if the active page is greater than 1, we will create the previous button. If the active page is less than totalPage, we will create the next button. To add this to the ul, we will create a new variable called `li`. We will append the strings using this and add this to the ul tag with `innerHTML`

```js
let pagination = document.querySelector("ul");
const totalPage = 20;

function element (page, totalPage){
	let li = "";
	if(page > 1){
		li += '<li class="btn prev"><span><i class="fa-solid fa-angle-left"></i> Prev</span></li>'
	}

	if(page < totalPage){
		li += '<li class="btn next"><span><i class="fa-solid fa-angle-right"></i> Next</span></li>'
	}

}

element(5, totalPage);
```
 ![[Pasted image 20221029095415.png]]


Now, for the numbers, create 2 variables which will be the range of numbers, the first variable is the first number before the active page and the second is the last after the active page. Use backticks so that we could modify the numbers depending on the page. 
```js
let pagination = document.querySelector("ul");
const totalPage = 20;
let before = page - 1;
let after = page + 1;

function element (page, totalPage){
	let li = "";
	if(page > 1){
		li += '<li class="btn prev"><span><i class="fa-solid fa-angle-left"></i> Prev</span></li>'
	}

	for(let pages = before; pages <= after; pages++){
	    li += `<li class="numb"><span>${pages}</span></li>`
	}

	if(page < totalPage){
		li += '<li class="btn next"><span><i class="fa-solid fa-angle-right"></i> Next</span></li>'
	}

}

element(5, totalPage);
```

![[Pasted image 20221029095844.png]]


Use [[Three.js Click Event]] on click listener to the numbers by [[Recursion]] calls. Prev button will just decrease the active page value while the other is the inverse. Number page will also do this but in their own page. 

```js
let pagination = document.querySelector("ul");
const totalPage = 20;
let before = page - 1;
let after = page + 1;

function element (page, totalPage){
	let li = "";
  if(page > 1){
    li += `<li class="btn prev" onclick="element(${page - 1}, ${totalPage})"><span><i class="fa-solid fa-angle-left"></i> Prev</span></li>`;
	  }
	}

	for(let pages = before; pages <= after; pages++){
	    li += `<li class="numb" onclick="element(${pages}, ${totalPage})"><span>${pages}</span></li>`
	}

	if(page < totalPage){
		li += `<li class="btn next" onclick="element(${page + 1}, ${totalPage})"><span><i class="fa-solid fa-angle-right"></i>Next</span></li>`
	}

}

element(5, totalPage);
```

Now, what we want to do is that we could navigate to the beginning and the last item when we are at the middle, what we could do is to check if the page is greater than 2, we will add the first number, if it is also greater than 3, then we will add dots as the design. We do the same at the last, when the active page is less than totalPage - 1, we will add the last number, then if it is also less than totalPage -2 we will add dots
```js
let pagination = document.querySelector("ul");
const totalPage = 20;
let before = page - 1;
let after = page + 1;

function element (page, totalPage){
	let li = "";
  if(page > 1){
    li += `<li class="btn prev" onclick="element(${page - 1}, ${totalPage})"><span><i class="fa-solid fa-angle-left"></i> Prev</span></li>`;
	  }
	}

	// Changes
	if(page > 2){
	    li += `<li class="numb" onclick="element(1, ${totalPage})"><span>1</span></li>`;
	    if(page > 3){
	      li += `<li class="dots"><span>...</span></li>`;
	    }
  }

	for(let pages = before; pages <= after; pages++){
	    li += `<li class="numb" onclick="element(${pages}, ${totalPage})"><span>${pages}</span></li>`
	}

	// Changes
	if(page < totalPage - 1){
	    if(page < totalPage - 2){
			li += `<li class="dots"><span>...</span></li>`;
	    }
	    li += `<li class="numb" onclick="element(${totalPage}, ${totalPage})"><span>${totalPage}</span></li>`;
  }

	if(page < totalPage){
		li += `<li class="btn next" onclick="element(${page + 1}, ${totalPage})"><span><i class="fa-solid fa-angle-right"></i>Next</span></li>`
	}

}

element(5, totalPage);
```

![[Pasted image 20221029102008.png]]

The problem will then is that when we press the last number it will create a new one, the same problem at the beginning will output 0 to negative. Create a conditional check that if the pages is less than 1, then add 1. If the page is greater than the total, `continue`
```js
let pagination = document.querySelector("ul");
const totalPage = 20;
let before = page - 1;
let after = page + 1;

function element (page, totalPage){
	let li = "";
  if(page > 1){
    li += `<li class="btn prev" onclick="element(${page - 1}, ${totalPage})"><span><i class="fa-solid fa-angle-left"></i> Prev</span></li>`;
	  }
	}

	if(page > 2){
	    li += `<li class="numb" onclick="element(1, ${totalPage})"><span>1</span></li>`;
	    if(page > 3){
	      li += `<li class="dots"><span>...</span></li>`;
	    }
  }

	// Changes
	 for(let pages = before; pages <= after; pages++){
	    if(pages < 1){
	      pages += 1;
	    }
	    if(pages > totalPage){
	      continue;
	    }
	    li += `<li class="numb" onclick="element(${pages}, ${totalPage})"><span>${pages}</span></li>`
  }
  
	if(page < totalPage - 1){
	    if(page < totalPage - 2){
			li += `<li class="dots"><span>...</span></li>`;
	    }
	    li += `<li class="numb" onclick="element(${totalPage}, ${totalPage})"><span>${totalPage}</span></li>`;
  }
  
	if(page < totalPage){
		li += `<li class="btn next" onclick="element(${page + 1}, ${totalPage})"><span><i class="fa-solid fa-angle-right"></i>Next</span></li>`
	}
}

element(5, totalPage);
```

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---