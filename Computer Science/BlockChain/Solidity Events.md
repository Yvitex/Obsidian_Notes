---
aliases: []
---
In [[BlockChain]], we want our [[ERC-20]] to log its transaction, not just the current one but also the past transactions that occured. In this, we have things like Logs that uses [[Bloom Filter]]

We could write events like this using the `event` filter
```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value)
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

When we do this, things will be hashed to the bloom filter. 
- keccack256(contractAddress)
- keccack256(Transfer/Approval())
- keccack256(to)
- keccack256(from)

Since our [[Bloom Filter]] could store 4 topics, and 3 indexes that could be 4 if some topics are anonymous them it might look like this.![[Pasted image 20221103052330.png]]
If these are empties, then there is no transaction. But hey, do we really need to do this?
Well, it depends. ![[Pasted image 20221103052512.png]]
We could choose not to implment anything. But if you really wanna query it, then use events. 

To do this in actual code. Insert this to the solidity source code just below the [[Solidity State Variable]]
```solidity
event Transfer(address indexed to, address indexed from, uint256 amount);
event Approve(address indexed owner, address indexed spender, uint256 amount);
```

Then we use this for transactions using `emit` key
```solidity
function _transfer(address sender, address recipient, uint256 amount) private returns (bool){
	//...
	emit Transfer(sender, recipient, amount);
	return true;
}

function transferFrom(address sender, address recipient, uint256 amount) external returns (bool){
	// ...
	emit Approve(sender, msg.sender, amount);
	return _transfer(sender, recipient, amount);
}

function approve(address spender, uint256 amount) external returns (bool){
	// ...
	emit Approve(msg.sender, spender, amount);
	return true;
}

function _mint(address to, uint256 amount) internal {
	// ...
	emit Transfer(address(0), to, amount);
}
```

Yeah, this are every transactions including mint, approve, transfer and transferFrom which specifically emit 2 events, one is for the approval and one is for the transfer. 

# Metatags
###### Related: [[Solidity Language]]
###### Tags: 
###### Source: 

---