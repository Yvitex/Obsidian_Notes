---
aliases: []
---
# Quick Sort
Another complicated but efficient [[Sorting Algorithm]] that have bettern [[Space Complexity]] compared to [[Merge Sort]]. 

The benefit of this is that the space compelxity is [[Logarithmic Time Complexity|O(log n)]] but the worse sceneario is that the [[Big O Asymptotic Analysis|Time Complexity]] could be [[Quadratic Time|O(n^2)]]
```ad-Attention
title: Best Algorithm
collapse: open
Use this [[Sorting Algorithm]] if you are sure that the worse case won't occur or you don't care. Use this for efficient [[Big O Asymptotic Analysis|Time Complexity]] but with efficent [[Space Complexity]]

```

The [[Algorithm]] says that first, we need to choose a pivot point
![[Pasted image 20221007153838.png]]

In our case that is the 4, numbers that are higher than 4 will go to its left and number that is lower will go to the right. Now we will divide it by half maintaining the position of the previous pivot point
![[Pasted image 20221007154007.png]]

Now, if the array contains only 3 items, it does not need any further division. Choose another pivot point and move the items as necessary. The second array will choose a pivot point and after everything is set, will be broken down againinto smaller piecces and choose another pivot point. We will merge it to one array

The code for this is pretty tough:

First, define the necessary variables such as tracker such as the pivot index and the partition index.
If you are wondering, partition index is simply the separator which will be the center. Parition Index will take over the value of the pivot
```js
function quickSort(array, left, right){
  let pivot;
  let partitionIndex;
}
```
![[Pasted image 20221007193315.png]]

Next is the conditional statement for the left and right. If left is less than the right value, as it should be then we will execute this code, by the way, we will execute the code like this
```js
quickSort(numbers, 0, numbers.length - 1);
console.log(numbers);
```

So the left is 0 and the right is the last index of the array. We set the pivot as the last array index, the partition index will get its value from another function we will create later
```js
function quickSort(array, left, right){
  let pivot;
  let partitionIndex;

  if(left < right){
    pivot = right;
    partitionIndex = getPartitionIndex(array, left, right, pivot);
  }
}
```

The function `getPartitionIndex` will count the values lower than the `array[pivot]` and that will be our partition Index as well as the position of the pivot value. 

Temporariy, we will set the pivot value as the pivot value, and the parititionIndex as the first item in that array
```js
function getPartitionIndex(array, left, right, pivot){
  let pivotValue = array[pivot];
  let partitionIndex = left;
}
```

We will create a for loop to scan each value in that array and if a value is lower than the pivot value, we will send it to the partitionIndex which is temporarily the first part of the array. We will also increment the `paritionIndex` as the counter of all lower value than the pivot. This will also serve where we will place the pivot value in the array
```js
function getPartitionIndex(array, left, right, pivot){
  let pivotValue = array[pivot];
  let partitionIndex = left;
  for(let i = left; i < right; i++){
    if(array[i] < pivotValue){
      swap(array, i, partitionIndex); // place the lower than pivot value to the beginning of the array
      partitionIndex++; // increase our counter
    }
  }
  swap(array, partitionIndex, pivot) // place the pivot value at its right place
  return partitionIndex; // return the partition index
}
```

Swap function is simply switching the first and second index 
```js
function swap(array, firstIndex, secondIndex){
  let temp = array[secondIndex];
  array[secondIndex] = array[firstIndex];
  array[firstIndex] = temp;
}
```

Now, going back to our function, we will form 2 recursion, one is for the left division, one is for the right division. Left division will start from the `left` variable or 0 or the start of the array up to the partitionIndex - 1, while the right division will start from the paritionIndex + 1 up to the last of that array or length - 1 aka `right` variable 
```js
function quickSort(array, left, right){
  let pivot;
  let partitionIndex;

  if(left < right){
    pivot = right;
    partitionIndex = getPartitionIndex(array, left, right, pivot);
    quickSort(array, left, partitionIndex - 1)
    quickSort(array, partitionIndex + 1, right)
  }
  return array;
}
```

Return the array




# Metatags
###### Related: 
###### Tags: 
###### Source: 

---