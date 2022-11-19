---
aliases: []
---
Struct is a combinator of other [[Solidity Data Types]].
```solidity
struct Something{
	uint255 myNumber;
	address owner;
	mapping(address => bool) isValid;
}
```

We could do this including [[Solidity Mapping]]. If there is a mapping, we could set the value like this
```solidity
Something public something;

something.myNumber = 1;
something.owner = 0x123...;
```

Or if there is none, we could do it like a parameter
```solidity
something = Something(1, 0x123...);
```

One thing to note is that we can't use Struct as a key inside mapping, but we could use Struct as a value
```solidity
mapping(Something => uint256) wrongMapping;
mapping(uint256 => Something) correctMapping;
```


# Metatags
###### Related: [[Solidity Language]]
###### Tags: 
###### Source: 

---