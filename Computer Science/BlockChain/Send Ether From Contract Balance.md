---
aliases: []
---
We could send ether from [[Smart Contract]] to other [[Public-key Generation|address]].
We want our smart contract to hold eth that it could pay to the user and to do that, we must first make our constructor payable
```solidity
constructor() payable{
	console.log("Wave Portal");
}
```

Then we make a function like this
```solidity
function wave(string memory message) public{
	totalWaves++;
	console.log("%s has waved and says %s", msg.sender, message);
	
	waves.push(Wave(msg.sender, message, block.timestamp));
	emit NewWave(msg.sender, block.timestamp, message);

	uint256 priceAmount = 0.0001 ether;
	require(priceAmount <= address(this).balance, "Not enough contract balance");

	(bool success, ) = (msg.sender).call{value: priceAmount}("");
	require(success, "Transaction failed");
}
```

We could specidy a value in [[Solidity Language]] as ether amount using `ether` keyword
```solidity
uint256 priceAmount = 0.0001 ether;
```

Revert the transaction if the price is too big for our balance
```solidity
require(priceAmount <= address(this).balance, "Not enough contract balance");
```

To actually send ether to the address, we use the call. This will allow them to widthraw the ether
```solidity
(bool success, ) = (msg.sender).call{value: priceAmount}("");
require(success, "Transaction failed");
```

In our run.js, for testing. When we deploy our contract, we will apply some ether to it. This is the full code. 
```javascript
const run = async () => {
    const [owner, otherAddress] = await hre.ethers.getSigners();
    const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
    const waveContract = await waveContractFactory.deploy({value: hre.ethers.utils.parseEther("0.1")});
    await waveContract.deployed();
    console.log("Contract deployed to: " + waveContract.address);
    console.log("Contract deployed by: " + owner.address);

    await waveContract.getTotalWaves();
    
    let balance = await hre.ethers.provider.getBalance(waveContract.address);
    console.log("Current Balance: " + hre.ethers.utils.formatEther(balance));

    const waveFunction1 = await waveContract.wave("Hi my bro");
    await waveFunction1.wait();

    const waveFunction2 = await waveContract.connect(otherAddress).wave("Sup, how's going?");
    await waveFunction2.wait();
    
    const allWaves = await waveContract.getAllWaves();
    console.log(allWaves);

    balance = await hre.ethers.provider.getBalance(waveContract.address);
    console.log("Current Balance: " + hre.ethers.utils.formatEther(balance));

    await waveContract.getTotalWaves();
}

const runMain = async () => {
    try {
        await run();
        process.exit(0);
    } catch (error) {
        console.log(error);
        process.exit(1);
    }
}

runMain();
```

While deploying our contract, we will send an ether to it using the value transaction parameter. To actually pass it, a string to an ether value, we use the hre's utility function called parseEther to convert it into ether
```js
const waveContract = await waveContractFactory.deploy({
	value: hre.ethers.utils.parseEther("0.001"),
});
```

That is for writing ether. But how about reading the balance. We could do this again using hre's provider method called `getBalance` and accepts an address. We will use the address from where we deployed the contract. To read that balance, we use the reverse function for writing it called `formatEther`
```js
let balance = await hre.ethers.provider.getBalance(waveContract.address);
console.log("Current Balance: " + hre.ethers.utils.formatEther(balance));
```

![[Pasted image 20221108054031.png]]

It's working good. Do the same for the deployment code, But with no testing it.
```js
const run = async () => {
    const [owner, otherAddress] = await hre.ethers.getSigners();
    const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
    const waveContract = await waveContractFactory.deploy({value: hre.ethers.utils.parseEther("0.1")});
    const ownerBalance = await owner.getBalance();
    await waveContract.deployed();
    console.log("Contract deployed to: " + waveContract.address);
    console.log("Contract deployed by: " + owner.address);
    console.log("Deployer Balance: " + ownerBalance.toString());

    await waveContract.getTotalWaves();
}

const runMain = async () => {
    try {
        await run();
        process.exit(0);
    } catch (error) {
        console.log(error);
        process.exit(1);
    }
}

runMain();
```



# Metatags
###### Related: 
###### Tags: 
###### Source: 

---