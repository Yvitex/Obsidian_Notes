---
aliases: [hardhat]
---
## Setup
This will be done using hardhat. Create a new folder. Initialize the project
```shell
$ mkdir tokenFile
$ cd tokenFile
$ npm init --y
```

Install the hardhat
```shell
$ npm i --save-dev hardhat
```

Execute the installed file
```shell
$ npx hardhat
```

## Typescript
Choose the option to create with [[Typescript]]. This will automatically do the file structure. ![[Pasted image 20221101145423.png]]

We install the required dependencies
```shell
$ npm i --save-dev typescript ts-node
$ npm i @nomicfoundation/hardhat-toolbox
$ npm install @openzeppelin/contracts
```

We could call some commands using this guide
```shell
$ npx hardhat help
```

We could compile using 
```shell
$ npx hardhat compile
```

This will output the [[Solidity Language|application binary interface]] and opscode. 
Sometimes there would be an error and this is because of the dependencues, we could instead choose the empty config file at the beginning. The use this to create a transaction. Just don't forget the contracts, script and test folder. 

## Javascript
We could also choose [[Javascript]]
```bash
$ npm install --save-dev chai @nomiclabs/hardhat-ethers ethers @nomicfoundation/hardhat-toolbox @nomicfoundation/hardhat-chai-matchers
```

Go take a look at our `hardhat.cofig.js`
```js
require("@nomicfoundation/hardhat-toolbox");

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.17",
};
```

We will add some accounts using `ethers`  getSigners. We would call it in terminal and we code it as a task
```js
require("@nomicfoundation/hardhat-toolbox");

task("accounts", "Get the accounts sample from getSigners", async (taskArgs, hre) => {
	const accounts = hre.ethers.getSigners();
	let index = 1;
	for (account in accounts){
		console.log(index + ": " + account);
		index++;
	}	
})


/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.17",
};

```

We could get the ethers inside the second parameter async function. If we use this like:
```shell
$ npx hardhat accounts
```

![[Pasted image 20221106110605.png]]

THat is the power of task.

## Constructor
We could [[Debug in Solidity]] by importing `hardhat/console.sol`
```solidity
pragma solidity 0.8.17;
import "hardhat/console.sol";

contract ERC20 {
	constructor(){
		console.log("Hwllo");
	}
}
```

Contract will start by declaring state variables.
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity 0.8.17;

contract ERC20 {
	uint256 public totalSupply;
	string public name;
	string public symbol;
	uint8 public decimal;
}
```

We will set the name and symbol using a variable using a constructor
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity 0.8.17;

contract ERC20 {
	uint256 public totalSupply;
	string public name;
	string public symbol;
	uint8 public decimal;

	constructor(string memory _name, string memory _symbol){
		name = _name;
		symbol = _symbol;
	}
}
```

Alternatively, we could just create a function for the decimal that will return the value
```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity 0.8.17;

contract ERC20 {
	uint256 public totalSupply;
	string public name;
	string public symbol;

	constructor(string memory _name, string memory _symbol){
		name = _name;
		symbol = _symbol;
	}

	function getDecimal() external pure returns (uint8){
		return 18;
	}
}
```

Read the [[Solidity Memory, Calldata, Storage Keys]]

## Transfer Function
This will involves [[Solidity Mapping]] to store the balance of accounts. 
```solidity
contract ERC20 {
	uint256 public totalSupply;
	string public name;
	string public symbol;

	mapping(address => uint256) public balanceOf;

	constructor(string memory _name, string memory _symbol){
		name = _name;
		symbol = _symbol;
	}

	function getDecimal() external pure returns (uint8){
		return 18;
	}
}
```

We then create a function that will check if their is an address recipient and check if the balance is enough for the transaction to occur using the art of [[Reverting a Contract]]. That function will take the receiver account and the amount to send. We could check if the address is 0, using `address(0)`.
```solidity
contract ERC20 {
	uint256 public totalSupply;
	string public name;
	string public symbol;

	mapping(address => uint256) public balanceOf;

	//...

	function transfer(address recipient, uint256 amount) external returns (bool){
		require(recipient != address(0), "ERC20 ERR: Found Zero Address");
		uint256 senderBalance = balanceOf[mgs.sender];
		require(senderBalance >= amount, "ERC20 ERR: Not Enough Balance");
	}
}
```

Now, we reduce the balance of user, then add it to the receiver. 
```solidity
function transfer(address recipient, uint256 amount) external returns (bool){
	require(recipient != address(0), "ERC20 ERR: Found Zero Address");
	uint256 senderBalance = balanceOf[msg.sender];
	require(senderBalance >= amount, "ERC20 ERR: Not Enough Balance");

	balanceOf[msg.sender] = senderBalance - amount;
	balanceOf[recipient] += amount;
	return true;
}
```

## Transfer From 
This function is a way to transfer balance in behalf of the other using their balance. This could be only done if the owner allowed you to. The first thing we need to do is to map the owner to the spender and amount. So this is a 3 columned mapping. 
```solidity
contract ERC20 {
	uint256 public totalSupply;
	string public name;
	string public symbol;

	mapping(address => uint256) public balanceOf;
	mapping(address => mapping(address, uint256)) public allowance;
}
```

What we are going to do is to transform the transfer function into a private variable. Copy paste it as a new function, add a sender parameter and adapt it to the previous function
```solidity
function _transfer(address sender, address recipient, uint256 amount) private returns (bool){
	require(recipient != address(0), "ERC20 ERROR: Zero Address Found");
	uint256 senderBalance = balanceOf[sender];

	require(senderBalance >= amount, "ERC20 ERROR: Not Enough Balance");
	balanceOf[sender] = senderBalance - amount;
	balanceOf[recipient] += amount;
	return true;
}

// Modify the prev function
function transfer(address recipient, uint256 amount) external returns (bool){
	return _transfer(msg.sender, recipient, amount);
}
```

Create a new function called transfer from. Do the same as the previous, just don't use the msg.sender for the sender parameter.
```solidity
function transferFrom(address sender, address recipient, uint256 amount) external returns (bool){
	return _transfer(sender, recipient, amount);
}
```

Now, we check if the amount is sufficient to the allowance. If yes, then we reduce the allowance with the amount.
```solidity
function transferFrom(address sender, address recipient, uint256 amount) external returns (bool){
	uint256 allowedBalance = allowance[sender][msg.sender];
	require(allowedBalance >= amount, "ERC20: Not enough balance");
	allowance[sender][msg.sender] = allowedBalance - amount;
	return _transfer(sender, recipient, amount);
}
```

## Approve
This function is accompanied by tranfer from in which we allow something to be transfered in a specified amount. This function will accept 2 parameters which is the spender and the amount. This function will set the mapping for where how much the owner allows the spender to spend. 
```solidity
function approve(address spender, uint256 amount) external returns (bool){
	require(spender != address(0), "ERC20: Zero Spender Address");
	allowance[mgs.sender][spender] = amount;
	return true;
}
```

After some tweaks in order to mint and log tokens with [[Solidity Events]]. Here is the full code
```solidity
// SPDX-License-Identifier: UNLICENSED

pragma solidity 0.8.17;

contract ERC20 {
    uint256 public totalSupply;
    string public name;
    string public symbol;

    event Transfer(address indexed to, address indexed from, uint256 amount);
    event Approve(address indexed owner, address indexed spender, uint256 amount);

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    constructor(string memory _name, string memory _symbol){
        name = _name;
        symbol = _symbol;
        _mint(msg.sender, 100e18);
    }

  

    function getDecimal() external pure returns (uint8){
        return 16;
    }

    function transfer(address recipient, uint256 amount) external returns (bool){
        return _transfer(msg.sender, recipient, amount);
    }

    function transferFrom(address sender, address recipient, uint256 amount) external returns (bool){
        uint256 allowedBalance = allowance[sender][msg.sender];
        require(allowedBalance >= amount, "ERC20: Not enough balances");
        allowance[sender][msg.sender] = allowedBalance - amount;

        emit Approve(sender, msg.sender, amount);

        return _transfer(sender, recipient, amount);
    }

    function approve(address spender, uint256 amount) external returns (bool){
        require(spender != address(0), "ERC20 ERR: No Spender Address");
        allowance[msg.sender][spender] = amount;

        emit Approve(msg.sender, spender, amount);

        return true;
    }

    function _transfer(address sender, address recipient, uint256 amount) private returns (bool){
        require(recipient != address(0), "ERC20 ERROR: Zero Address Found");
        uint256 senderBalance = balanceOf[sender];
        require(senderBalance >= amount, "ERC20 ERROR: Not Enough Balance");
        balanceOf[sender] = senderBalance - amount;
        balanceOf[recipient] += amount;
        emit Transfer(recipient, sender, amount);
        return true;
    }

    function _mint(address to, uint256 amount) internal {
        require(to != address(0), "ERC20 ERR: No Address Found");
        totalSupply += amount;
        balanceOf[to] += amount;
        emit Transfer(to, address(0), amount);
    }
}
```

Now we could perform [[ERC-20 Deployment]]
# Metatags
###### Related: [[ERC-20]], [[Automated Testing Solidity (ERC20)]]
###### Tags: 
###### Source: 

---