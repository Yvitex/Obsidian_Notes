---
aliases: []
---
One of the main features of [[Solidity Language]] is that its ability to detect overflows and underflow. 

What is that? This occured when the resulting value of a unsigned integer became negative causes an underflow, this will output a very high positive number rathern than negative. Overflow on the other hand is adding the maximum number that can be handled by the uint or int then with 1 or more. This will output 0. 

Luckily for us, we don't need to worry because [[Solidity Language]] will detect the overlows and underflow as well as [[Reverting a Contract]] when this problems occur. 

```solidity
function checkedSub() pure public returns (uint256){
	return type(uint256).min - 1; // causes a very huge number
}

function checkedAdd() pure public returns (uint256){
	return type(uint256).max + 1; // causes a very small number
}
```

![[Pasted image 20221104095046.png]]

If we don't want this check, we could enclose the substraction, addition, multiplication and any other operation with `unchecked {}`

```solidity
function checkedSub() pure public returns (uint256){
	return unchecked { type(uint256).min - 1 }; // causes a very huge number
}

function checkedAdd() pure public returns (uint256){
	return unchecked {type(uint256).max + 1 }; // causes a very small number
}
```




# Metatags
###### Related: [[Solidity Data Types]]
###### Tags: 
###### Source: 

---