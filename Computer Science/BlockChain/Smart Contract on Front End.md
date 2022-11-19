---
aliases: []
---
Using the codes from [[Metamask on FrontEnd]]. We will then talk to our [[Smart Contract]] in our application. To do this, we need to import Ethers, but not that same ethers libray for [[Automated Testing Solidity (ERC20)]] of hardhat

Import the ethers library
```js
import {ethers} from "ethers";
```

Create a function inside application that will handle the wave() function when we press the button. Surround it with try and catch
![[Pasted image 20221107105110.png]]

```js
const wave = async () => {
	try{
	}
	catch (error){
		console.log(error);
		return;
	}
}
```

The whole function is this
```js
  const wave = async () => {
    console.log("waving")
    try{
      const ethereum = getEthereumObject();

      if(ethereum){
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signers = provider.getSigner();
        const waveContractPortal = new ethers.Contract(contractAddress, contractAbi, signers);

        let count = await waveContractPortal.getTotalWaves();
        console.log("Total Waves: " + count);

        let waving = await waveContractPortal.wave();
        console.log("Mining: " + waving.hash);

        await waving.wait();
        console.log("Mined: " + waving.hash);

        count = await waveContractPortal.getTotalWaves();
        console.log("Total Waves: " + count);
        
      }
      else{
        console.log("No ethereum object found");
        return;
      }
    }
    catch (error){
      console.log(error);
      return;
    }
```

Lets dissect this a bit further:
Check if the ethereum object exist, if not, exit the function
```js
if(ethereum){
}
else{
	console.log("No ethereum object found");
	return;
}
```

If etherum exist, Create the new provider, we could do this using ethers with its method providers, set it to Web3Provider with the [[Ethereum]] as the argument.
```js
const provider = new ethers.providers.Web3Provider(ethereum);
```

Now, get the signers, signer is the abstraction of ethereum account that sends signed messages or transaction to ethereum blockchain. This could be get with signers.
```js
const signer = provider.getSigner();
```

Now we that we have a signer, which is an important part as the argument of a [[Smart Contract]] portal. We could now create that portal using ethers contract method. THis will have 3 arguments which is the address of that contract, the [[Solidity Language|ABI]], and then signer. 
```js
const waveContractPortal = new ethers.Contract(contractAddress, abiContract, signer);
```

Obviously we do not yet met the requirements, we need the value of the contractAddress which is found after we deployed our contract in [[Quick Node]] or [[ERC-20 Deployment]]
![[Pasted image 20221107100011.png]]

abiContract can be found as a json file in the artifacts folder on the root. We could find a folder that states the name of our contract and under here it have the json file for the ABI. Copy paste it on a new file called WaveContract.json, which must be on a folder called utils with the App.jsx
![[Pasted image 20221107144018.png]]
We could simply import it
```js
import abi from "./utils/WavePortal.json";
```

Then use the import to call the abi
```js
const contractAbi = abi.abi;
```

Then copy paste the contract address
```js
const contractAddress = 0x12131...;
```

Using the contractPortal, we could freely call the functions however we want. To call the `getTotalWave`. This call fucntion doesn't cost [[Gas Fees]] because we are reading in the [[BlockChain]], not changing it. 
```js
let count = await waveContractPortal.getTotalWaves();
console.log("Total Waves: " + count);
```

But if we want to create changes, we need to pay. We could also see what hash block is the transaction being compiled using variable.hash
```js
// Write to blocks
let waving = await waveContractPortal.wave();
console.log("Mining: " + waving.hash);

// Wait to finish
await waving.wait();
console.log("Mined: " + waving.hash);
```

Then we could call the totalFunction to see the changes. The transaction may take a while though.
![[Pasted image 20221107144903.png]]


This is quite plain and too simple for our taste, yknow wha? Let's allow user to send a message for it. Of course, we want to log this transaction so we will use [[Solidity Events]] inside the contract.

```solidity
// SPDX-License-Identifier: Unlicense

pragma solidity 0.8.17;

import "hardhat/console.sol";

contract WavePortal{

    uint256 totalWaves;
    event NewWave(address indexed from, uint256 timestamp, string message);

    struct Wave{
        address waver;
        string message;
        uint256 timestamp;
    }

    Wave[] waves;

    constructor(){
        console.log("Wave Portal");
    }

    function wave(string memory message) public{
        totalWaves++;
        console.log("%s has waved and says %s", msg.sender, message);

        waves.push(Wave(msg.sender, message, block.timestamp));
        emit NewWave(msg.sender, block.timestamp, message);
    }

    function getAllWaves() public view returns (Wave[] memory){
        return waves;
    }

    function getTotalWaves() public view returns (uint256){
        console.log("We have total of %s waves", totalWaves);
        return totalWaves;
    }
}
```

Create an event that includes the address of the sender, the message string and the timestamp of the block
```solidity
event NewWave(address indexed from, uint256 timestamp, string message);
```

Create a [[Solidity Struct]] composed of that same arguments
```solidity
struct Wave{
	address waver;
	string message;
	uint256 timestamp;
}
```

Create an array that will sore our structs
```soldity
Wave[] waves;
```

When we wave, we create a struct object and push it inside the array
```solidity
waves.push(Wave(msg.sender, message, block.timestamp));
```

Then we emit the event with those same parameters
```solidity
emit NewWave(msg.sender, block.timestamp, message);
```

Create a function that will return that array
```js
function getAllWaves() public view returns (Wave[] memory){
	return waves;
}
```

We are going to test this functions accordingly in the run.js
```js
const run = async () => {
    const [owner, otherAddress] = await hre.ethers.getSigners();
    const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
    const waveContract = await waveContractFactory.deploy();
    await waveContract.deployed();
    console.log("Contract deployed to: " + waveContract.address);
    console.log("Contract deployed by: " + owner.address);

    await waveContract.getTotalWaves();

	// Wave with message
    const waveFunction1 = await waveContract.wave("Hi my bro");
    await waveFunction1.wait();

    const waveFunction2 = await waveContract.connect(otherAddress).wave("Sup, how's going?");
    await waveFunction2.wait();

	// Get all waves
    const allWaves = await waveContract.getAllWaves();
    console.log(allWaves);

    await waveContract.getTotalWaves();

```

![[Pasted image 20221107162610.png]]



# Metatags
###### Related: [[Metamask on FrontEnd]]
###### Tags: 
###### Source: 

---