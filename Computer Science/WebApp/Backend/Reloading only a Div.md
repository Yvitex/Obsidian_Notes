---
aliases: []
---
We could reload a specific part of a div using JQuery. Upon request of a certain server method in the node.js, we will fetch the data and reload a part of a div.

Upon click we will fetch a link to delete the data
```js
$(".bi-check-square-fill").click(function(){
})
```

Using JQUERY, we will reload the page using the .load function after fetching a certain method
```js
$(".bi-check-square-fill").click(function(){
	fetch("/delete/" + id, {method: "DELETE"}).then(() => {
        $("#refresh").load(window.location.href + " #refresh");
})
```

Becayse we only want to refresh the div element with the same items in that element only updated, then we use the window location reference plus the div element. 

We could also refresh the whole page using js
```js
$(".bi-check-square-fill").click(function(){
	fetch("/delete/" + id, {method: "DELETE"}).then(() => {
        $("#refresh").load(window.location.href + " #refresh");
        setTimeout(() => {location.reload()}, 300);
})
```













# Metatags
###### Related: [[AJAX]]
###### Tags: 
###### Source: 

---