---
aliases: []
---

```solidity
constructor(string memory _name, string memory _symbol){
	name = _name;
	symbol = _symbol;
}
```

We could see the use of memory key in this example but what exactly is this?
We have 3 different keys that direct a storage and they are:
- Storage
- Memory
- Calldata

storage is used when we are trying to store data to the [[BlockChain]].
memory is used when we are trying to store data that exist only when the function is called
calldata is used which is stored in a special location like memory but cheaper. 

We only use this keys for [[Reference Type]] which in [[Solidity Language]] are strings, structs, array and maps. Everytime we do this, we are creating a new copy of values. 

# Metatags
###### Related: [[ERC-20 Token Creation]]
###### Tags: 
###### Source: 

---