---
aliases: []
---
There is a method that will revert a contract before even sending it to the receipient and that is through the method `revert()`. 

With this method in the [[Ethereum Virtual Machine]], this will cancel all methods and prevent it from having any state changes, though you still have to pay for the [[Gas Fees]] but relatively less. 

So the thing looks like this with if and else statement
```solidity
function getLessValue() external payable{
	uint256 randomNumber = getRandomNumber();
	uint256 ethRefund;
	if(randomNumber < 5){
		ethRefund = msg.value / randomNumber;
		payable(msg.sender).transfer(ethRefund);
	}
	else{
		revert();
	}
}
```

So if our random number is not less than 5, we revert back ok. But we have a shorter version of this and that is using `requrie()`

So the alternative would be
```solidity
function getLessValue() external payable{
	uint256 randomNumber = getRandomNumber();
	uint256 ethRefund;
	require(randomNumber < 5, "Not less than 5");
	ethRefund = msg.value / randomNumber;
	payable(msg.sender).transfer(ethRefund);
}
```

So if the random Number is not less than 5, we send a note that it is not less than 5. ![[Pasted image 20221101102934.png]]








# Metatags
###### Related: 
###### Tags: 
###### Source: 

---