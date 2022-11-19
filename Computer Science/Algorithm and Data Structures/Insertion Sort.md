---
aliases: []
---
# Insertion Sort
Is a better [[Sorting Algorithm]] for nearly sorted data or for small data set, better than the [[Bubble Sort]] and [[Selection Sort]].

```ad-Notice
title: Use this algorithm, only when necessary
collapse: open
Thia [[Sorting Algorithm]] is only good for small arrays and nearly sorted array. Don't use considering the [[Scalability]]

```


First we need to look for the first item
![[Pasted image 20221007045538.png]]

go then to the next item which is 5, because 5 is less than 6, we switch it up
![[Pasted image 20221007045703.png]]

Now we go to the next item which is 3 then because they are lower than 5 and 6, we put it before them
![[Pasted image 20221007045749.png]]

Repeat until the end of the list
![[Pasted image 20221007045809.png]]

![[Pasted image 20221007045826.png]]

## Code

The [[Javascript]] code for this could be,
Create a new array
```js
function insertionSort(array) {
  let newArray = []
}
```

We take the first item in the list
```js
function insertionSort(array) {
  let newArray = []
  newArray.push(array[0])
}
```

Create a for loop, the first check is if the first item in the array is greater than the item at hand, unshift the item to the array. If the item is greater than the last item of the new Array, then push it to the end of the array, else, find the right spot in the new array and then splice it if suddenly the item is less than the item in the j. As we could see, the [[Big O Asymptotic Analysis|Time Complexity]] could be [[Linear  Time Complexity|O(n)]] or worse case, [[Quadratic Time|O(n^2)]]
```js
function insertionSort(array) {
  let newArray = []
  newArray.push(array[0])
  for (let i = 1; i < array.length; i++) {
    if (newArray[newArray.length - 1] < array[i]) {
      newArray.push(array[i])
    }
    else if(newArray[0] > array[i]){
      newArray.unshift(array[i])
    }
    else {
      for (let j = 0; j < newArray.length; j++) {
        if (array[i] < newArray[j]) {
          newArray.splice(j, 0, array[i])
          break // break the loop once this is executed
        }
      }
    }
  }
  return newArray
}
```

The [[Space Complexity]]  though in this solution is [[Linear  Time Complexity|O(n)]]. We could improve this by not creating a new array. 

Create a for loop base on length
```js
function insertionSort(array) {
 for(let i = 1; i < array.length; i++){
 }
  return array
}
```

Inside this array, we will make some conditions, if the first item is greater than the selected item, unshift the selected item and delete it using `splice`. If the last item is less than the selected item, push the selected item and delete it using `splice`
```js
function insertionSort(array) {
 for(let i = 1; i < array.length; i++){
   if(array[0] > array[i]){
     array.unshift(array.splice(i, 1)[0]);
   }
   else if(array[array.length - 1] < array[i]){
     array.push(array.splice(i, 1)[0]);
   }
 }
  return array
}
```

To insert at the middle, create another for loop base on the length of the sorted data which is based on the index i. If the selected item is less than the current item in that loop and smaller than the current item - 1, then, splice it and delete the selected item
```js
function insertionSort(array) {
 for(let i = 1; i < array.length; i++){
   if(array[0] > array[i]){
     array.unshift(array.splice(i, 1)[0]);
   }
   else if(array[array.length - 1] < array[i]){
     array.push(array.splice(i, 1)[0]);
   }
   for(let j = 0; j < i; j++){
     if(array[i] < array[j] && array[i] > array[j - 1]){ // we use && to avoid the use of break
       array.splice(j, 0, array.splice(i, 1)[0])
     }
   }
 }
  return array
}
```


In conclusion, we will use insertion sort only for small data and nearly sorted data. 



# Metatags
###### Related: 
###### Tags: 
###### Source: 

---