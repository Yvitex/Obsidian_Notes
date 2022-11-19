---
aliases: []
---
# Selection Sort
Is another [[Sorting Algorithm]] that finds the smalelst number and switch it with the first and proceeding index.

```ad-Danger
title: NOT FOR USE
collapse: open
This algorithm is not for use in real life

```


![[Pasted image 20221006141826.png]]

In here, the first minimum is 8, we will start the scan at the second item and because 5 is less than 8, then we will replace the minimum as 5. We do this again to the next
![[Pasted image 20221006141930.png]]

Because 2 is less than 5, 2 will be our current minimum
Because 2 is not smaller than 6 then we'll move on
![[Pasted image 20221006142015.png]]

We repeat this until we find the current minimum value. Once it finds the lowest, switch this item to the first index, proceed with the second item neglecting the first item. 
![[Pasted image 20221006142059.png]]

The code for this is:
```js
function selectionSort(array) {
  let length = array.length
  for(let i = 0; i < length; i++){
    let smallest = i; // store the smallest index
    let temp = array[i]; // temporary container
    for(let j = i + 1; j < length; j++){ // starts at the next of the item index
      if(array[j] < array[smallest]){
        smallest = j // update the smallest index when their is a lesser number
      }
    }
    array[i] = array[smallest]; // switch
    array[smallest] = temp;
  }
  return array;
}
```

This is a lot worse than [[Bubble Sort]] with the same [[Quadratic Time|O(n^2)]] time complexity. 










# Metatags
###### Related: 
###### Tags: 
###### Source: 

---