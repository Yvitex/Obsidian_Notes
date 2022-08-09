# Remove the Non Dominant
Notice that we in [[Big O Asymptotic Analysis]], we only care about the [[Worst Case]]. Therefore we remove the non dominant. 

For instant e
```js
function printAllNumbersThenAllPairSums(numbers) {

  console.log('these are the numbers:');
  numbers.forEach(function(number) {
    console.log(number);
  });

  console.log('and these are their sums:');
  numbers.forEach(function(firstNumber) {
    numbers.forEach(function(secondNumber) {
      console.log(firstNumber + secondNumber);
    });
  });
}

printAllNumbersThenAllPairSums([1,2,3,4,5])
```

This should have O(n + n^2), but it will became [[Quadratic Time|O(n^2)]] at the end as it is the worser scenario. 
IF we have this kind of complexity O(n^2+100+n/2), it will just became [[Quadratic Time]] complexity in the end

