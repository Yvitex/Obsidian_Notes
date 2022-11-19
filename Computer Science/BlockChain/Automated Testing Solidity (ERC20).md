---
aliases: []
---
Test driven development is good. Though we are forced to write more test than contracts. This will aid you to test your [[Smart Contract]] my automatically deploying it and checking the transactions happening. 
![[Pasted image 20221102094737.png]]

At this case, we are using mocha framework for [[Javascript]]. It will have this main methods called `describe`, `beforeEach`, and `it`

It generally look like this![[Pasted image 20221102094829.png]]
To do exactly this, create a folder called test, inside here we will create a file of the naming we want in [[Typescript]]. 
![[Pasted image 20221102161325.png]]

What we will test is the code we create in the [[ERC-20 Token Creation]]. In the starting setup file for [[ERC-20 Token Creation|hardhat]], we already have the test samples, we could just remove the base code

The first element we need is the `describe` keyword, this will output something in the console. Enter any string for this. 
```ts
import { expect } from "chai";
import { ethers } from "hardhat";

describe("ERC20 Token Test", async function(){
	
})
```

This will have a callback function which is an [[Async and Await|async]]. We could initialize the ContractFactory for this. But before that, we compile first our contract using 
```shell
$ npx hardhat compile
```

Then we do initializations to get the contract out of compiled contract using ethers. We will put it inside the `beforeEach` keyword which has a callback [[Async and Await|async]] function. We store it in variables using [[Async and Await|await]]. 
```ts
import { expect } from "chai";
import { ethers } from "hardhat";

describe("ERC20 Token Test", function(){
	beforeEach(async function(){
		// Get the contract which is named ERC20
		const ERC20ContractFactory = await ethers.getContractFactory("ERC20");
		// Deploy the Contract
		const myERC20Contract = await ERC20ContractFactory.deploy("Hello", "Sym");
		// Check if the contract is deployed before proceeding
		await myERC20Contract.deployed();
	})
})
```

`beforeEach` keyword is executed before any other following `describe` method. Now we could follow it with `describe`. The first describe that we will do is to set up the address so that it have some tokens in it. We do create some dummy account using `signers` from `hardhat-ethers` module. 

Extract the `myERC20Contract`, or initialize it outside the `beforeEach`. The type will be `Contract`. 
```typescript
import { expect } from "chai";
import { ethers } from "hardhat";

describe("ERC20 Token Test", function(){
	let myERC20Contract: Contract;

	beforeEach(async function(){
		const ERC20ContractFactory = await ethers.getContractFactory("ERC20");
		myERC20Contract = await ERC20ContractFactory.deploy("Hello", "Sym");
		await myERC20Contract.deployed();
	})
})
```

We will use the contract to transfer token in the First Address. Before that, we will mint some token by adding some functions in the Contract source code. Create a function that is an internal [[Solidity Function Scope]]. 

```solidity
function _mint(address to, uint256 amount) internal{
	require(to != address(0), "ERC20 ERR: No Address Found");
	// ADD to total supply
	totalSupply += amount;
	balanceOf[to] += amount;
}
```

Add this to the contructor, the to address will be the sender and the amount is 100 tokens, literllau in our case it has 100 x 10 ^ 18 but actually its the smallest construct so it still has 100 token just like wei to ether. 
```solidity
constructor(string memory _name, string memory _symbol){
	name = _name;
	symbol = _symbol;
	_mint(msg.sender, 100e18);
}
```

The sender will have that many token. We could use it now inside [[Typescript]] test
```ts
import { expect } from "chai";
import { ethers } from "hardhat";

describe("ERC20 Token Test", function(){
	let myERC20Contract: Contract;

	beforeEach(async function(){
		const ERC20ContractFactory = await ethers.getContractFactory("ERC20");
		myERC20Contract = await ERC20ContractFactory.deploy("Hello", "Sym");
		await myERC20Contract.deployed();
	})

	describe("I have 10 Tokens", function(){
		beforeEach(async function(){
			await myERC20Contract.transfer();
		})
	})
})
```

Uh oh, we don't have dummy address. Lets create one, create a variable which is a `SignerWithAddress`. We could get this type in `hardhat-ether` module. Install it if you don't have. Create 2 address for now. 
```ts
import { expect } from "chai";
import { ethers } from "hardhat";
import {SignerWithAddress} from "@nomiclabs/hardhat-ethers/signers"

describe("ERC20 Token Test", function(){
	let myERC20Contract: Contract;
	let address1: SignerWithAddress;
	let address2: SignerWithAddress;

	beforeEach(async function(){
		const ERC20ContractFactory = await ethers.getContractFactory("ERC20");
		myERC20Contract = await ERC20ContractFactory.deploy("Hello", "Sym");
		await myERC20Contract.deployed();

		// Initialize it here
		address1 = (await ethers.getSigner())[1];
		address2 = (await ethers.getSigner())[2];
	})

	describe("I have 10 Tokens", function(){
		beforeEach(async function(){
			// Fill the first address with 10 tokens
			await myERC20Contract.transfer(address1.address, 10);
		})
	})
})
```

We use before each because we do this before anything else in after it. If not, it will likely to run parallel with the test. `(await ethers.getSigner())[0]` is the msg.sender. We don't need to specify it but you could. We also need to call `.address` to call the address inside signers.

Now put each describe methods which are test cases after the `beforeEach`
```ts
describe("ERC20 Token Test", function(){
	let myERC20Contract: Contract;
	let address1: SignerWithAddress;
	let address2: SignerWithAddress;

	beforeEach(async function(){
		const ERC20ContractFactory = await ethers.getContractFactory("ERC20");
		myERC20Contract = await ERC20ContractFactory.deploy("Hello", "Sym");
		await myERC20Contract.deployed();

		address1 = (await ethers.getSigner())[1];
		address2 = (await ethers.getSigner())[2];
	})

	describe("I have 10 Tokens", function(){
		beforeEach(async function(){
			await myERC20Contract.transfer(address1.address, 10);
		})

		describe("I transfer 10 tokens", function(){
		
		})

		describe("I transfer 15 tokens", function(){
		
		})
	})
})
```

Inside this test cases, they will have an `it` keyword where we run the test and have labels string as a marker. We also use `expect` to check if the function we did has an effect and that effect is what we expect. We could call global variables from the contract using my `myERC20Contract`. Also, `connect` specifies the sender of the balance so that we won't send it using the msg.sender orginals. 
```ts
describe("I have 10 Tokens", function(){
	beforeEach(async function(){
		await myERC20Contract.transfer(address1.address, 10);
	})

	describe("I transfer 10 tokens", function(){
		it("10 Tokens Successfully Transfered", async function(){
			// Transfer 10 token to second account using the first
			await myERC20Contract.connect(address1).transfer(address2.address, 10);
		})
		// Check if address2 has 10 in his balance
		expect(await myERC20Contract.balanceOf(address2.address)).to.equals(10);
	})

	describe("I transfer 15 tokens", function(){
	
	})
})
```

If we already expect an error, we could merge the `it` and `expect` keyword like this
```ts
describe("I transfer 15 tokens", function(){
	it("Reverts Back the Transaction", async function(){
		await myERC20Contract.connect(address1).transfer(address2.address, 15);
	})
})
```

We merge by putting expect inside it, during the [[Async and Await|await]]. We already know that this will be reverted becuase our balance is not enough, we could detect it using this chaining methods `.to.be.revertedWith("")`
```ts
describe("I transfer 15 tokens", function(){
	it("Reverts Back the Transaction", async function(){
		await expect(myERC20Contract
			.connect(address1)
			.transfer(address2.address, 15))
			.to.be.revertedWith("ERC20 ERR: Not Enough Balance"); // what error we expect that causes the reversion. 
	})
})
```



# Metatags
###### Related: 
###### Tags: 
###### Source: 

---