---
aliases: []
---
Modify the code inside `deploy.ts`
![[Pasted image 20221103092010.png]]

 It will initially have some sample codes like this
 ```ts
 import { ethers } from "hardhat";

async function main() {
  const currentTimestampInSeconds = Math.round(Date.now() / 1000);
  const ONE_YEAR_IN_SECS = 365 * 24 * 60 * 60;
  const unlockTime = currentTimestampInSeconds + ONE_YEAR_IN_SECS;
  const lockedAmount = ethers.utils.parseEther("1");
  
  const Lock = await ethers.getContractFactory("Lock");
  const lock = await Lock.deploy(unlockTime, { value: lockedAmount });
  await lock.deployed();

  console.log(`Lock with 1 ETH and unlock timestamp ${unlockTime} deployed to ${lock.address}`);

}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

Simply change the name of the codes so that it will get our [[ERC-20]] contract
```ts
import { ethers } from "hardhat";
async function main() {

  const ERC20 = await ethers.getContractFactory("ERC20");
  const erc20 = await ERC20.deploy("YAMETE", "YAM");
  await erc20.deployed();
  console.log(`Token deployed to ${erc20.address}`);
}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

Now, our token name is yamete the symbol is yam. 
In our hardhat.config.ts, specify this
```ts
const config: HardhatUserConfig = {
	solidity: "0.8.4",
	networks: {
		ropsten: {
			url: process.env.ROPSTEN_URL || "",
			accounts: process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
		},
	},
	gasReporter: {
		enabled: process.env.REPORT_GAS !== undefined,
		currency: "USD",
	},
	
	etherscan: {
		apiKey: process.env.ETHERSCAN_API_KEY,
	},
};
```

As you could see, we must use [[Environmental Variables]] for this one. On our env files, get your [[API]] key from [Infuria](https://infura.io/)

There is also a warning that ropsten is already deprecated, so we use Sepolia and Goeli instead
```solidity
const config: HardhatUserConfig = {
  solidity: "0.8.17",
  networks: {
    sepolia: {
      url: process.env.SEPOLIA_URL || "",
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
    },
    goerli: {
      url: process.env.GOERLI_URL || "",
      accounts: process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
    },
  },
  gasReporter: {
    enabled: process.env.REPORT_GAS !== undefined,
    currency: "USD",
  },
  etherscan: {
    apiKey: process.env.ETHERSCAN_API_KEY,
  },
};
```

We could get the goerli and sepolia testnet using the [infuria documentation](https://docs.infura.io/infura/networks/ethereum/how-to/choose-a-network) which is only a link appended by the key

```
PRIVATE_KEY=PrivateKey
SEPOLIA_URL=https://sepolia.infura.io/v3/<key>
GOERLI_URL=https://goerli.infura.io/v3/<key>
```

Private key could be get through Metamask, go to account detail then export private key.
Now, we could deploy it for real. Run the scripts we modified, and specify the network to be used
```shell
$ npx hardhat run scripts/deploy.ts --network goerli
```

This will cost a [[Gas Fees]]. It will automatically compile and be deployed to [[Ethereum]] and you could see this in [etherscan](https://etherscan.io/)

We could call the functions to transfer tokens inside [Remix IDE](https://remix.ethereum.org/) by calling the contract here![[Pasted image 20221103114440.png]]
We could also call flatten so that the whole code will be on one file that could be run in remix IDE
```shell
$ npx hardhat run contracts/ERC20.sol >> ERC20Flatten.sol
```

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---