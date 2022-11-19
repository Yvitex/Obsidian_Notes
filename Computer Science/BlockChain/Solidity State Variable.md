---
aliases: []
---
Are variables that is declared before creating any functions. They could be private or public variables, and could also be constant or immutable

### Public
```solidity
contract MyContract {
	uint256 public contractor = 2;
}
```

Public could be accessed anywhere in the code, externally from the class or even inside the class.

### Private
```solidity
contract MyContract {
	uint256 private contractor = 2;

	function setContractor(uint num) external{
		contractor = num;
	}

	function getContractor() external view returns(uint){
		return contractor;
	}
}
```

With private, we could only access it using getter and setter, don't forget to include the external view, etc in making these functions. 

### Constant and Immutable
```solidity
contract MyContract {
	uint256 constant public CONSTRACTOR = 2;
	uint256 immutable public CONSTRACTOR2 = 2;
}
```

They should be written in all caps. Also, the difference between this 2 is that constant should exist at compile time and immutable could be declared inside the function or class just only one time. 

# Metatags
###### Related: [[Solidity Function Scope]]
###### Tags: 
###### Source: 

---