---
aliases: []
---
This is a way for us to Inherit the functionality and variables of a [[Smart Contract]]. 
This could be either, single, multilevel, heirarchical, multiple, hybrid inheritance
![[Pasted image 20221103154304.png]]

In our [[Solidity Function Scope]], we state our functions as either public, private, external or internal. This play a huge role in inheritance as things that is declared as internal or public could be inherited. 

In order to inherit the contract for another contract, we use this. 
```solidity
contract B{} contract A is B{}
```

The construct is to declare the contract, then state the parent then the child. 
```solidity
contract C{} contract B is C {} contract A is B {} // multilevel
contract B{} contract C{} contract A is B, C{} // Hierarchical
contract C{} contract A is C{} contract B is C{} // Multiple
contract D{} contract B is D{} contract C is D{} contract A is B, C{} // Hybrid
```

There are things to keep in mind:
- No state variable clashes
Meaning, we don't want variables with similar names, Function could have similar names because they run based on context through
- Polymorphism
Alternatively we could call the super keyword or the contract name plus functions.
- constructor() ERC20("name", "sym"){}
Calling the parent contructor needs you to specify the contract. 

We could override functions of the parent contract
```solidity
contract BaseContract{
	function myFunction() public virtual{
	
	}
}

contract DerivedContract{
	function myFunction() public override(BaseContract){
	
	}
}
```

We could also create an [[Abstract Class]] or [[Interface Class]]
```solidity
abstract contract MyContract{}
interface IERC20{}
```


# Metatags
###### Related: [[Multiple Inheritance]], [[Java OOP Inheritance]], [[Javascript Inheritance]], [[Solidity Function Scope]]
###### Tags: 
###### Source: 

---