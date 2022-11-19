---
aliases: []
---
We could create a test run, or test deployment of our contract in the [[Ethereum Virtual Machine]]
Perhaps, we have this simple contract that we want to test out.
```solidity
// SPDX-License-Identifier: Unlicense
pragma solidity 0.8.17;
import "hardhat/console.sol";

contract WavePortal{
    constructor(){
        console.log("Hellow World");
    }
}
```

We could start a test deployment of a virtual hardhat [[Ethereum Virtual Machine]] by doing thisi
```js
const run = async () => {
    const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
    const waveContract = await waveContractFactory.deploy();
    await waveContract.deployed();
    console.log("Address: " + waveContract.address);
}
```

This code compiles the contract called WavePortal and generates the artifacts. As we could see, we have `hre` which is not imported by the code, rather it was automatically generated when we run `npx hardhat`. `hre` is basically hardhat runtime environment that contains all the functionality offered by [[ERC-20 Token Creation|hardhat]]
```js
const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
```

This deployes the contract to a virtual [[BlockChain]]. Then deletes that chain after running it.
```js
const waveContract = await waveContractFactory.deploy();
```

This waits until the contract is fully deployed
```js
await waveContract.deployed();
```

This outputs the address of our contract in the block chain
```js
console.log("Address: " + waveContract.address);
```

Then next, we input this function inside a try and catch code for safty measures
```js
const runMain = async () => {
	try{
		await run();
		process.exit(0);
	}
	catch(error){
		console.log(error);
		process.exit(1);
	}
}

runMain(); // run this function
```

## Executing Function
We could execute our function inside this run code.
For example, we have this contract in which adds a value to the totalWave when executes the wave function and return the totalWave with getTotalWaves()
```solidity
contract WavePortal{
	uint256 totalWaves; // declared state variable
	
	constructor(){
		console.log("Hellow World");
	}

	// add 1
	function wave() public{
		totalWaves++;
		console.log("%s has waved", msg.sender);
	}

	// return total
	function getTotalWaves() public view returns (uint256){
		console.log("We have total of %s waves", totalWaves);
		return totalWaves;
	}
}
```

We could execute the function by calling the deploed contract then the function to be executed. With this case, we are executing the function with the owner address or the sample [[Public-key Generation|address]] that deployed the [[Smart Contract]]
```js
const run = async () => {
    const [owner, otherAddress] = await hre.ethers.getSigners();
    const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
    const waveContract = await waveContractFactory.deploy();
    await waveContract.deployed();
    console.log("Contract deployed to: " + waveContract.address);
    console.log("Contract deployed by: " + owner.address);

    await waveContract.getTotalWaves();

    const waveFunction = await waveContract.wave();
    await waveFunction.wait();

    await waveContract.getTotalWaves();
}
```

This code gets the owner address or the deployer's address and another random generated address
```js
const [owner, otherAddress] = await hre.ethers.getSigners();
```

We could get this address by using the variable then chain it with its attribute address
```js
console.log("Contract deployed to: " + waveContract.address);
console.log("Contract deployed by: " + owner.address);
```

Now, we could call the function total waves. We wait for it to get executed
```js
await waveContract.getTotalWaves();
```

We then execute the wave() function that adds a value to the wave
```js
const waveFunction = await waveContract.wave();
```

We wait for the function to finish
```js
await waveFunction.wait();
```

Call the `getTotalWaves()` again to see the difference.
![[Pasted image 20221106125415.png]]

We could also use the other account using the `connect()` method like this
```js
const waveFunction2 = await waveContract.connect(otherAddress).wave();
```

![[Pasted image 20221106130722.png]]

# Metatags
###### Related: [[Ethereum Virtual Machine]], [[Hardhat Node Local Server]]
###### Tags: 
###### Source: 

---