---
aliases: []
---

Initialize varaibles
```solidity
import {expect} from "chai"
import { ethers } from "hardhat"
import { Contract } from "hardhat/internal/hardhat-network/stack-traces/model";

describe("StableCoin", function(){
  let ethUsdPrice: number;
  let feeRatePercentage: number;
  let StableCoin: Contract;
  
})
```

The first part is just to deploy and declare some values
```solidity
import {expect} from "chai"
import { ethers } from "hardhat"
import { Contract } from "hardhat/internal/hardhat-network/stack-traces/model";

describe("StableCoin", function(){
  let ethUsdPrice: number;
  let feeRatePercentage: number;

  this.beforeEach(async () => {
    feeRatePercentage = 3;
    ethUsdPrice = 4000;

    const OracleFactory = await ethers.getContractFactory("Oracle");
    const ethUsdOracle = await OracleFactory.deploy()
    await ethUsdOracle.setPrice(ethUsdPrice);
    
    const StableCoinFactory = await ethers.getContractFactory("StableCoin");
    const StableCoin = await StableCoinFactory.deploy(feeRatePercentage, ethUsdOracle.address);
    await StableCoin.deployed();
  })
})
```

To get the oracle, use the deployed oracle variable then get the address. We then check if we could mint and the rate of the StableCoin is equal to what we set in the start of the test
```solidity
import {expect} from "chai"
import { ethers } from "hardhat"
import { Contract } from "hardhat/internal/hardhat-network/stack-traces/model";

describe("StableCoin", function(){
	let ethUsdPrice: number;
	let feeRatePercentage: number;
	
	this.beforeEach(async () => {
		feeRatePercentage = 3;
		ethUsdPrice = 4000;
		
		const OracleFactory = await ethers.getContractFactory("Oracle");
		const ethUsdOracle = await OracleFactory.deploy()
		await ethUsdOracle.setPrice(ethUsdPrice);
		
		const StableCoinFactory = await ethers.getContractFactory("StableCoin");
		const StableCoin = await StableCoinFactory.deploy(feeRatePercentage, ethUsdOracle.address);
		await StableCoin.deployed();
	
		it("Should set fee rate percentage",async ( ) => {
			expect(await StableCoin.feeRatePercentage()).to.equal(feeRatePercentage);
		})
	
		it("Should allow minting", async () => {
			const ethAmount = 1;
			const expectedMintAmount = ethAmount * ethUsdPrice;
			await StableCoin.mint({
				value: ethers.utils.parseEther(ethAmount.toString())
			}); 
			expect(await StableCoin.totalSupply()).to.equal(
				ethers.utils.parseEther(expectedMintAmount.toString())
		    )
		});	
	})
})
```

`parseEther` is a function that convert a string from a constant number into ether value.

Now, next is that we check if we could burn tokens as expected.
```solidity
import {expect} from "chai"
import { ethers } from "hardhat"
import { Contract } from "hardhat/internal/hardhat-network/stack-traces/model";

describe("StableCoin", function(){
	//...

	describe("With minted tokens", function(){
		let mintAmount: number;
		this.beforeEach(async () => {
		  const ethAmount = 1;
		  mintAmount = ethAmount * ethUsdPrice;
		
		  await StableCoin.mint({
			value: ethers.utils.parseEther(ethAmount.toString()) // generate
		  });
		});
		
		it("Should allow burning", async () => {
		  const remainingStableCoinAmount = 100;
		  await StableCoin.burn(
			ethers.utils.parseEther(
			  (mintAmount - remainingStableCoinAmount).toString()
			)
		  )
		  expect(await StableCoin.totalSupply()).to.equal(
			ethers.utils.parseEther(remainingStableCoinAmount.toString())
		  );
	});
})
```

It will actually output, the totaySupply() to be 100 x 10 ^ 18 but because of `parseEther`. We matched the constant integer number that exacts this

After the should allow burning test case, we also test if the collateralBuffer in depositing is working.
```solidity
import {expect} from "chai"
import { ethers } from "hardhat"
import { Contract } from "hardhat/internal/hardhat-network/stack-traces/model";

describe("StableCoin", function(){
	//...
	
		it("Should prevent depositing collateral", async () => {
		  const expectedMininmumAmount = 0.1;
		  const stableCoinCollateralBuffer = 0.05;
		
		  await expect(StableCoin.depositCollateralBuffer({
			value: ethers.utils.parseEther(stableCoinCollateralBuffer.toString())
		  })).to.be.revertedWith("STC: Required Surplus Not met");
		})
		
		it("Should allow depositing collateral Buffer", async () => {
			  const stableCoinCollateralBuffer = 0.5;
			  await StableCoin.depositCollateralBuffer({
			  value: ethers.utils.parseEther(stableCoinCollateralBuffer.toString())
		  });
		
		  const DepositorCoinFactory = await ethers.getContractFactory("DepositorCoin");
		  const DepositorCoin = await DepositorCoinFactory.attach(await StableCoin.depositorCoin());
		  const newInitialSurplusInUsd = stableCoinCollateralBuffer * ethUsdPrice;
		
		  expect(await DepositorCoin.totalSupply()).to.equal(
			ethers.utils.parseEther(newInitialSurplusInUsd.toString())
		  )
		})
	});
})
```

Since  we are creating a new DepositorCoin in the contract. we are using some special methods in here. We get another new contract of DepositorCoin, then attach to it an instance of a depositorCoin inside StableCoin. 


# Metatags
###### Related: [[Automated Testing Solidity (ERC20)]]
###### Tags: 
###### Source: 

---