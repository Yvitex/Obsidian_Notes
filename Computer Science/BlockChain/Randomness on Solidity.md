---
aliases: []
---
Randomess in computer programming have algorithm that get numerical information from certain attributes of the computer such as temperature, fan speed, etc. 

In the blockchain, there is hardly no source of randomness so what do we do? We rely on something else but the easiest thing to get that randomness is through block difficulty and timestamp

To create randomness, create a seet variable
```solidity
uint256 seed;
```

Set the seed on the constructor base on block difficulty and timestamp. Modulo 100 so that it won't exceed more than 99
```js
constructor() payable{
	console.log("Wave Portal");
	seed = (block.difficulty + block.timestamp) % 100;
}
```

To a certain function which we wish to get the random number, reiterate the calculation and add the initial seed modulo 100
```js
function something() public{
	seed = (block.difficulty + block.timestamp + seed) % 100;
}
```

# Metatags
###### Related: [[Solidity Language]], [[Random Seed]],
###### Tags: 
###### Source: 

---