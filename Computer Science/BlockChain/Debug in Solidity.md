---
aliases: []
---
We could import "hardhat/console.sol" to the code
```solidity
import "hardhat/console.sol";

//...
```

So for example we have this code
```solidity
function getLessValue() external payable{
	uint256 randomNumber = getRandomNumber();
	require(randomNumber < 5, "Not less than 5");
	uint256 ethRefund = msg.value / randomNumber;
	payable(msg.sender).transfer(ethRefund);
}
```

We could output the value of randomNumber variable using console.log(), this must be separated with comma
```solidity
function getLessValue() external payable{
	uint256 randomNumber = getRandomNumber();
	console.log("Random Number: + ", randomNumber);
	require(randomNumber < 5, "Not less than 5");
	uint256 ethRefund = msg.value / randomNumber;
	payable(msg.sender).transfer(ethRefund);
}
```

```ad-Danger
title: Wei Wei
collapse: open
Note that each numbers in the code was in the form of WEI, not ETHER. 

```

Console.log in this case could use %s as a variable where the second parameter could output into meaning this code
```solidity
console.log("The number %s is sus", 10);
```

Outputs: The number 10 is sus

# Metatags
###### Related: [[Solidity Language]], [[Javascript]]
###### Tags: 
###### Source: 

---