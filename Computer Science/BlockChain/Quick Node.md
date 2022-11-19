---
aliases: []
---
This is a [website](www.quicknode.com) we could use to immediately deploy our transaction fast to the [[BlockChain]] networks.

To create a key, then select [[Ethereum]]
![[Pasted image 20221107092948.png]]

Our network is goerli for now. Then don;'t add some addons and press continue or create
![[Pasted image 20221107093133.png]]

We already created our deploy.js at [[Hardhat Node Local Server]]
```solidity
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

We could then setup our hardhat.config.js. Add the network configuration along with the url and private key account in metamask
```js
module.exports = {
  solidity: "0.8.17",
  networks: {
    goerli: {
      url: process.env.QUICKNODE_GOERLI_URL,
      accounts: [process.env.PRIVATE_KEY],
    }
  }
};
```

With this command
```shell
$ npx hardhat run scripts.deploy.js --network goerli
```

![[Pasted image 20221107100011.png]]

Copy the address somewhere which could be used in other frontend app, you could see the contract [here](https://goerli.etherscan.io/address/0xC01966CDABd824fFF06AFbA2f50C64d47F9fDef8)

# Metatags
###### Related: [[BlockChain]], [[ERC-20 Deployment]], [[Environmental Variables]]
###### Tags: 
###### Source: 

---