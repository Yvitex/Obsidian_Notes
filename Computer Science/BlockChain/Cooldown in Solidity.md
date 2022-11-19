---
aliases: []
---
This is quite easy to do with the help of `block.timestamp`. We could store the values in a [[Solidity Mapping]]. 
```solidity
mapping(address => uint256) public lastWavedAt;
```

Now when we call a function, we could include a [[Reverting a Contract]] function like require just like this that will revert the function if it detects that the block.timestamp is less than the lastWave plus 15 minutes
```solidity
require(lastWavedAt[msg.sender] + 15 minutes < block.timestamp, "Wait 15 Minutes");
```

If this succeds update the lastWavedAt
```solidity
lastWavedAt[msg.sender] = block.timestamp;
```


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---