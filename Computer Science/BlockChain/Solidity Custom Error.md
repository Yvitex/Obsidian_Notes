---
aliases: []
---
In reverting a contract, we could create custom errors in the `revert` keyword
We first specify what to be displayed as an errror in the state variable section
```solidity
error InitialCollateralRatioError(string message, uint256 minimum);

if( someNumber < 0){
	revert InitialCollateralRatioError(
		"Message",
		someNumber
	)
}
```


# Metatags
###### Related: [[Reverting a Contract]]
###### Tags: 
###### Source: 

---