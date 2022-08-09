# Big O Removing Constants
```js
function printFirstItemThenFirstHalfThenSayHi100Times(items) {
    console.log(items[0]); // O(1)

    var middleIndex = Math.floor(items.length / 2); // O(1)
    var index = 0; // O(1)

    while (index < middleIndex) { // O(n / 2)
        console.log(items[index]); // O(n / 2)
        index++; // O(n / 2)
    }

    for (var i = 0; i < 100; i++) {
        console.log('hi'); // O(100)
    }
}
```

We could say that it is O(3 + 3n/2 + 100) or O(1 + n/2 + 100) but removing the constants, we would be left with O(n) which means this is a [[Linear  Time Complexity]]


