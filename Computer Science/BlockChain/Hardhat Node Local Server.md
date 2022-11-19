---
aliases: []
---
This simulates how the [[BlockChain]] works in our computer. This is like a local server where we keep it alive for testing.

To do this, go to the terminal and execute this command
```shell
$ npx hardhat node
```

This will output some accounts.
![[Pasted image 20221106133853.png]]

Then we just create under script folder a file called `deploy.js`
```js
const run = async () => {
    const [owner, otherAddress] = await hre.ethers.getSigners();
    const waveContractFactory = await hre.ethers.getContractFactory("WavePortal");
    const waveContract = await waveContractFactory.deploy();
    const ownerBalance = await owner.getBalance();
    await waveContract.deployed();
    console.log("Contract deployed to: " + waveContract.address);
    console.log("Contract deployed by: " + owner.address);
	console.log("Owner's Balance: " + ownerBalance.toString());
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

We add some additional lines here. 
This will get the balance of the address
```js
const ownerBalance = await owner.getBalance();
```

Then print it out
```js
console.log("Owner's Balance: " + ownerBalance.toString());
```

To deploy our contract to the localhost, just command this on the other terminal
```shell
$ npx hardhat run scripts/deploy.js --network localhost
```

![[Pasted image 20221106134402.png]]

In our localhost node we could see this
![[Pasted image 20221106134559.png]]

This provides the information of the block. We have 1 block. This provides the [[Gas Fees]], [[Blocks of Blockchain|blocks]] etc.

# Metatags
###### Related: [[Ethereum Virtual Machine]], [[Server Computer]], [[ERC-20 Deployment]]
###### Tags: 
###### Source: 

---