---
aliases: []
---
Are like [[Hash Table]]. 
```solidity
mapping(address => uint256) myMapping;
```
![[Pasted image 20221102052519.png]]

But also we could store it like in triple columned table
```solidity
mapping(address => mapping(bool => uint256)) myMapping;
```
![[Pasted image 20221102052643.png]]

The main difference of this from [[Hash Table]] is that, when we leave a value blank, it will default into 0, in case of strings, "", in boolean, False. They have default values
![[Pasted image 20221102053344.png]]

Another difference is that there is no concept of length, and keys so we can't traverse the mapping. But rather we could use an array side by side with it. 

So we create a mapping and a Solidity Array
```solidity
mapping(address => uint256) myMapping;
address[] public myMappingKeys;
```

For everytime that we add something in the mapping, we add the keys in the array
```solidity
myMapping[theKeys] = values;
myMappingKeys.push(theKeys);
```

# Metatags
###### Related: [[Hash Table]], [[Address Type Solidity]]
###### Tags: 
###### Source: 

---