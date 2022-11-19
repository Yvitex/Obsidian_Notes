---
aliases: []
---
A function appended to the end of the other function to filter out how the function could be called and what is only allowed. 

```solidity
function payMeBack() external payable onlyOwner{
	...
}
```

`onlyOwner` is the modifier which is another function that filters out so that only the owner could call this
```solidity
modifier onlyOwner{
	require(msg.sender == owner, "Only Owner could send this Request");
	_;
}
```

Notice that we use the modifier key to state that the function is a modifier. Also we use underscore to state that execute the following code of the modified function. We write the code above the underscore but could also be after. Just remember that calling the underscore before the code will execute the modified function before the modifier. 








# Metatags
###### Related: 
###### Tags: 
###### Source: 

---