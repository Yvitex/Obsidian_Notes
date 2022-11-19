---
aliases: []
---
Can be used its function only internally and public. If we declare it as public, it creates a new contract. This is not  the common use of Library but rather we use it internally. 

We state the libary ising the `libary` keyword
```solidity
library Math{
	function something(uint256 a, uint256 b) internal pure returns(uint256) {
		// ...
	}
}

// We call it like this
Math.something(1, 2);

// Or we could as type 
contract Calculate{
	using Math for uint256
	function ss() public pure returns(uint256){
		2.something(3);
	}
}
```












# Metatags
###### Related: [[Solidity Language]]
###### Tags: 
###### Source: 

---