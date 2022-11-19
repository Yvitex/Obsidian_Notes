---
aliases: []
---
# Bubble Sort
This is the simplest and least efficient [[Sorting Algorithm]] where we compare each item from one another until we finally sorted the items in order. 

```ad-Attention
title: NOT FOR USE
collapse: open
This [[Sorting Algorithms]] is not for use in real life but for teaching purpose

```


First we comapre the first 2 items
![[Pasted image 20221006131442.png]]

If the first item is greater than the second, switch them. Move on to the next step which we will compare the second value to the third value
![[Pasted image 20221006131427.png]]

Because 6 is greater than 3, we switch them
![[Pasted image 20221006131540.png]]

We repeat this process until the end of the array
![[Pasted image 20221006131622.png]]

When we reach the end of the array, return back to the first item and compare it with the second. ![[Pasted image 20221006131706.png]]
This algorithm unfortunately has a [[Big O Asymptotic Analysis|Time Complexity]] of [[Quadratic Time|O(n^2)]] but its [[Space Complexity]] is [[Constant Time|O(1)]].

The code for thisn in [[Javascript]] is:
```js
const numbers = [99, 44, 6, 2, 1, 5, 63, 87, 283, 4, 0];

function bubbleSort(array) {
  for(let i = 0; i < array.length; i++){
    for(let j = 1; j < array.length; j ++){
      if(array[j - 1] > array[j]){
        let placeholder = array[j];
        array[j] = array[j-1];
        array[j-1] = placeholder;
      }
    }
  }
  return array;
}
```

Here we use 2 for loops, i, and j index, where j = 1 to avoid exceeding the array. If the previous index is greater than the next index, then we switch them up. Continue this loop depending on the number of items. 









# Metatags
###### Related: 
###### Tags: 
###### Source: 

---