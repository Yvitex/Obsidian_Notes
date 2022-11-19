---
aliases: []
---
## Setup
We are just going to inherit from our new created [[ERC-20 Token Creation]]. Create 2 files for the logic of StableCoin.sol and DepositorCoin.sol

For our stable coin, import the contract from [[ERC-20]]. Create a new contract that inherits from it
```solidity
import { ERC20 } from "./ERC20.sol"

contract StableCoin is ERC20{
	
}
```

This will have an error because we haven't yet specify the constructor from ERC20 contract. As we know from our [[Solidity Inheritance]], we do this
```solidity
import { ERC20 } from "./ERC20.sol"

contract StableCoin is ERC20{
	constructor() ERC20("StableCoin", "STC") {}
}
```

Do the same for the DepositorCoin
```solidity
import { ERC20 } from "./ERC20.sol"

contract DepositorCoin is ERC20{
	constructor() ERC20("DepositorCoin", "DPC") {}
}
```

In here, we are going to get the address of the msg.sender
```
import { ERC20 } from "./ERC20.sol"

contract DepositorCoin is ERC20{
	address public owner;
	constructor() ERC20("DepositorCoin", "DPC") {
		owner = msg.sender;
	}
}
```

We are going to make it so that the stable coin contract is the owner of the depositor coin contract as logically it is

Import the contract from DepositorCoin and then initialize it in the StableCoin
```solidity
import { ERC20 } from "./ERC20.sol";
import { DepositorCoin } from "./DepositorCoin.sol";

contract DepositorCoin is ERC20{
	DepositorCoin public depositorCoin;
	constructor() ERC20("DepositorCoin", "DPC") {}
}
```

## Burning and Minting
In our [[ERC-20 Token Creation]] code, we add a burning functionality. This is used to destroy coins.
```solidity
function _burn(address from, uint256 amount) internal{
	require(from != address(0), "ERC20 ERR: Zero Address Found");
	totalSupply -= amount; // destroy coins from total supply
	balanceOf(from) -= amount; // remove coins from balance

	emit Transer(address(0), from, amount);
}
```

In our <u>DepositCoin</u> code, add a burn and mint functionality based on the [[ERC-20]] token code. We just need to filter if the owner is from the StableCoin code address. This functions will be used externally or be called outside. We will only allow the owner or the person deploying this contract to control this 2 functions.
```solidity
function mint(address to, uint256 amount) external{
	require(owner == msg.sender, "Only Owner Can Mint");
	_mint(to, amount); // call the inherited function from erc20 code
}

function burn(address from, uint256 amount) external{
	require(owner == msg.sender, "Only Owner Can Mint");
	_brun(from, amount); // call the inherited function from erc20 code
}
```

Now in our <u>StableCoint.sol</u> code. We could first start by creating the mint function
```solidity
function mint() external payable{
	_mint(msg.sender, msg.value);
}
```

We do not want to directly mint the user specified value. Rather we want the value equivalent to USD. Therefore it is a user specified value multiplied by its value in USD. msg.value is the collateral in ETH
```solidity
function mint() external payable{
	uint256 stableCoinAmount = msg.value * ETH_VALUE_IN_USD;
	_mint(msg.sender, stableCoinAmount);
}
```

We have no way yet of knowing the ETH to USD value so we create a dummy at first in the state variable.
```solidity
contract StableCoin is ERC20{
	DepositorCoin public depositorCoin;
	uint256 ETH_VALUE_IN_USD = 2000;
	constructor() ERC20("StableCoin", "STB"){}
	
	function mint() external payable{
		uint256 stableCoinAmount = msg.value * ETH_VALUE_IN_USD;
		_mint(msg.sender, stableCoinAmount);
	}
}
```

Also, we will apply some fees, fees will be reduced to the total stable coin amount and will be given to the depositor. We will create as separate internal function for the calculation of the fees. Get the remaining eth and this will be converted to the stable coin 
```solidity
function mint() external payable{
	uint256 fees = _getFee(msg.value); // get fees
	uint256 remainingEth = msg.value - fees; // substract fees
	uint256 stableCoinAmount = remainingEth * ETH_VALUE_IN_USD;
	_mint(msg.sender, stableCoinAmount);
}
```

For our get fees function, we will simply multiply the fees percentage to the amount of eth then divide by 100;
```solidity
function _getFee(uint256 ethAmount) internal view returns (uint256){        
	return (feeRatePercentage * ethAmount) / 100;
}
```

We initialize the `feeRatePercentage` in the contructor
```solidity
contract StableCoin is ERC20{
	DepositorCoin public depositorCoin;
	uint256 private ETH_VALUE_IN_USD = 2000;
	uint256 public feeRatePercentage; // declare
	constructor(uint256 _feeRatePercentage) ERC20("StableCoin", "STB"){
		feeRatePercentage = _feeRatePercentage // initialize
	}
}
```

The thing is, we will only give fees if there is a depositor, create a check for this.
```solidity
function _getFee(uint256 ethAmount) internal view returns (uint256){ 
	bool hasDepositor = address(depositorCoin) != address(0) && depositorCoin.totalSupply() > 0; // if there is an address and totalSupply is not 0 in depositor coin
	if(!hasDepositor){
		return 0; //instead
	}
	return (feeRatePercentage * ethAmount) / 100;
}
```

In our burn function we could have this
```solidity
function burn(uint256 amount) external{
	_burn(msg.sender, amount);
}
```

We also want to add a functionality where we could refund or return the ETH from burning the [[Stable Coin]]. 
```solidity
function burn(uint256 burnStableAmount) external{
	_burn(msg.sender, burnStableAmount);

	uint256 refundingEth = burnStableAmount / ETH_VALUE_IN_USD; // calculate refund
    uint256 fees = _getFee(refundingEth); // get fees for refund
    uint remaningRefundingEth = refundingEth - fees; // get the remaining eth
}
```

We would widraw it to the sender using the `call` keyword
```solidity
function burn(uint256 amount) external{
	_burn(msg.sender, amount);

	uint256 refundingEth = burnStableAmount / ETH_VALUE_IN_USD; // calculate refund
    uint256 fees = _getFee(refundingEth); // get fees for refund
    uint remaningRefundingEth = refundingEth - fees; // get the remaining eth

	(bool success,) = msg.sender.call{value: remainingRefundingEth}("");
	require(success, "STC: Burn refund transaction failed");
}
```

## Oracle

Create an [[Oracle Class]]. This will have 2 state variables which is the owner address and the price. Create a getter and setter and constructor for the owner which will be set to deployer
```solidity
contract Oracle{
	address public owner;
	uint256 private price;
	
	constructor(){
		owner = msg.sender;
	}
	
	function getPrice() external view returns (uint256){
		return price;
	}
	
	function setPrice(uint256 _price) external {
		require(owner == msg.sender, "Oracle: Set by owner only");
		price = _price;
	}
}
```

Update our code in StableCoin.sol, replace variable `ETH_VALUE_IN_USD` with the Contracts getPrice method
```solidity
import { Oracle } from "./Oracle.sol";

contract StableCoin is ERC20{
	DepositorCoin public depositorCoin;
	uint256 public feeRatePercentage;
	Oracle public oracle;

	constructor(uint256 _feeRatePercentage, Oracle _oracle) ERC20("StableCoin", "STC"){
		feeRatePercentage = _feeRatePercentage;
		oracle = _oracle; // initialize
	}
	
	//...

	function mint() external payable{
		uint256 fees = _getFee(msg.value);
		uint256 remainingEth = msg.value - fees;
		uint256 stableCoinAmount = remainingEth * oracle.getPrice(); // get price
		_mint(msg.sender, stableCoinAmount);
	}
```

## Depositor
Now, we are going to implement a depositor feature in StableCoin.sol code. The first function that we want is a private function that returns the surplus or deficit, if there is an extra or no extras in the depositor coins.

The formula to get the deficit or surplus is the totalSupply minus the balance of this contract. 
```solidity
function _getDeficitOrSurplus() private view returns (uint256){
	uint256 ethContractBalanceInUsd = (address(this).balance - msg.value) * oracle.getPrice(); 
	uint256 totalStableCoinBalance = totalSupply;
	int256 surplusOrDeficit = int256(totalStableCoinBalance) - int256(ethContractBalanceInUsd) ;
	return surplusOrDeficit;
}
```

Get the contract balance with `address(this).balance` minus msg.value because we want the balance before transaction, then multiply them to [[Oracle Class]] `getPrice()` to get the usd equivalence.

TotalSupply is already inherited from [[ERC-20]] code. We then substract these 2 into an int256 variable because it could be either negative or positive.

Create a function in which calculates the amount of DepositorCoin to mint in the stable coin sol. We could do this by [[Calling Contracts]] function. Check if there is a surplus or deficit, if there is a surplus, we will do this

```solidity
function dfcCollateralBuffer() external payable{
	int256 deficitOrSurplus = __getDeficitOrSurplus(); // this is usd

	if(deficitOrSurplus <= 0){
		return;
	}
	// If Surplus
	uint256 surplus = uint256(deficitOrSurplus);
}
```

If there is a surplus, we will get the price of depositor coin. The formula for this is depositor coin total supply divide by surplus. We will then calculate the amount od dpc to be minted by multiplying the user specified value of msg.value to the dpc price then divide it by eth price in usd to convert it into token? That is the amount of token to be minted
```solidity
function dfcCollateralBuffer() external payable{
	int256 deficitOrSurplus = __getDeficitOrSurplus(); // this is usd

	if(deficitOrSurplus <= 0){
		return;
	}
	// If Surplus
	uint256 surplus = uint256(deficitOrSurplus);
	uint256 dpcInUsdPrice = _getDPCInUsd(surplus);
	uint256 mintDPCAmount = ((dpcInUsdPrice * msg.value) / oracle.getPrice());
	depositorCoin.mint(msg.sender, mintDPCAmount); // mint DPC to sender
}
```

```solidity
function __getDPCInUsd(uint256 surplus) private view returns (uint256){
	return depositorCoin.totalSupply() / surplus; // use method to call variable from another contract
}
```

Now, what if there is a deficit. Specify a certain percentage ratio that we need in order to reduce or disperse the deficit in the [[Solidity State Variable]].
```solidity
uint256 public constant INITIAL_COLLATERAL_PERCENTAGE = 10; // 10 percent
```

Now in our fucntion we do this. 
We get the surplus and make it positive, convert it into eth from usd. Get the percentage value of the totalSupply and check if the user's msg.value is greater than the percentage plus surplus in eth.
```solidity
function dfcCollateralBuffer() external payable{
	int256 deficitOrSurplus = __getDeficitOrSurplus(); // this is usd

	if(deficitOrSurplus <= 0){
		uint256 deficitInUsd = uint256(deficitOrSurplus * -1);
		uint256 ethPrice = oracle.getPrice();
		uint256 deficitInEth = deficitInUsd / ethPrice;

		uint256 requiredInitialSurplusPercentage = (totalSupply * INITIAL_COLLATERAL_PERCENTAGE) / 100;
		uint256 requiredInitialPercentageInEth = requiredInitialSurplusPercentage / ethPrice;
		require(msg.value >= requiredInitialSurplusInEth + deficitInEth, "STC: Required Surplus Not met");
		return;
	}
	//...
}
```

Next is that we reduce the msg.value by the deficitInEth variable, convert it into USD. Create a new DepositorCoin contract and then calculate the amount of DepositorCoin to be minted by the usd value.
```solidity
function dfcCollateralBuffer() external payable{
	int256 deficitOrSurplus = __getDeficitOrSurplus(); // this is usd

	if(deficitOrSurplus <= 0){
		uint256 deficitInUsd = uint256(deficitOrSurplus * -1);
		uint256 ethPrice = oracle.getPrice();
		uint256 deficitInEth = deficitInUsd / ethPrice;

		uint256 requiredInitialSurplusPercentage = (totalSupply * INITIAL_COLLATERAL_PERCENTAGE) / 100;
		uint256 requiredInitialPercentageInEth = requiredInitialSurplusPercentage / ethPrice;
		require(msg.value >= requiredInitialSurplusInEth + deficitInEth, "STC: Required Surplus Not met");

		uint256 newInitialSurplus = msg.value - deficitInEth;
		uint256 newInitialSurplusInUsd = newInitialSurplus * ethPrice;

		// Create new depositor'
		depositorCoin = new DepositorCoin();
		uint256 mintDepositorCoin = newInitialSurplusInUsd;
		depositorCoin.mint(msg.sender, mintDepositorCoin);

	}
	//...
}
```

Also, we must prevent burning if there is deficit so that w
```solidity
function burn(uint256 burnStableAmount) external {
	int256 deficitOrSurplus = _getDeficitOrSurplus();
	require(deficitOrSurplus >= 0, "STC: Cannot burn while deficit"); // filter
	
	_burn(msg.sender, burnStableAmount);

	// ...
```

## Withdraw Function
Now we must make a withdraw function.
This function will take one argument which is the amount of DPC to be burned in exchange for the [[ERC-20]] token. This will include 2 checks, the first check is to ensure that the msg.sender actually have a balance that is sufficient for the transaction and the second is to ensure that there is not deficit in the balance of the contract which means there is no funds to withdraw. 

Since, we do not send eth, but we get eth, we use external function that is not payable
```solidity
function withdrawCollateralBuffer(uint256 depositorCoinAmount) external{
	require(depositorCoin.balanceOf(msg.sender) >= depositorCoinAmount, "STC: Balance is less than the Burn Amount");

	int256 deficitOrSurplus = _getDeficitOrSurplus();
	require(deficitOrSurplus > 0, "STC: No funds to withdraw");
}
```

Next, if these 2 succeeds, we burn the depositor coin
```solidity
function withdrawCollateralBuffer(uint256 depositorCoinAmount) external{
	require(depositorCoin.balanceOf(msg.sender) >= depositorCoinAmount, "STC: Balance is less than the Burn Amount");

	int256 deficitOrSurplus = _getDeficitOrSurplus();
	require(deficitOrSurplus > 0, "STC: No funds to withdraw");
	depositorCoin.burn(msg.sender, depositorCoinAmount);
}
```

Now, we will calculate the ETH in return. Get the Surplus, get the current price of DPC, get the refund with the formula of depositor coin amount multiplied by the current price of DPC then convert it into ETH by dividing the result with the current price of ETH in usd.
```solidity
function withdrawCollateralBuffer(uint256 depositorCoinAmount) external{
	require(depositorCoin.balanceOf(msg.sender) >= depositorCoinAmount, "STC: Balance is less than the Burn Amount");

	int256 deficitOrSurplus = _getDeficitOrSurplus();
	require(deficitOrSurplus > 0, "STC: No funds to withdraw");
	depositorCoin.burn(msg.sender, depositorCoinAmount);

	uint256 surplus = uint256(deficitOrSurplus);
	uint256 dpcPrice = _getDPCInUsd(surplus);
	uint256 refundingUSD = depositorCoinAmount * dpcPrice;
	uint256 refundingETH = refundingUSD / oracle.getPrice();
}
```

Call the amount of refunding eth to the sender address
```solidity
function withdrawCollateralBuffer(uint256 depositorCoinAmount) external{
	require(depositorCoin.balanceOf(msg.sender) >= depositorCoinAmount, "STC: Balance is less than the Burn Amount");

	int256 deficitOrSurplus = _getDeficitOrSurplus();
	require(deficitOrSurplus > 0, "STC: No funds to withdraw");
	depositorCoin.burn(msg.sender, depositorCoinAmount);

	uint256 surplus = uint256(deficitOrSurplus);
	uint256 dpcPrice = _getDPCInUsd(surplus);
	uint256 refundingUSD = depositorCoinAmount * dpcPrice;
	uint256 refundingETH = refundingUSD / oracle.getPrice();

	(bool success, ) = msg.sender.call{value: depositorCoinAmount}("");
	require(success, "STC: Withdrawal Failed");
}
```

## WadLib Library
We don't have floating data types in [[Solidity Language]], so how do we handle fractions, multiplcation and division in this language. Fixed point. 
![[Pasted image 20221105104827.png]]

Fixed point has a fractional part and integer part. Solidity don't have direct support with fixed point but we could just implement it ourselves. 

Create a [[Solidity Library]] for this in a new file called WadLib. Have a state variable that is 10 ^ 18 or any range that will represent the decimal
```solidity
library WadLib{
	uint256 public constant MULTIPLIER = 10 ** 18;
}
```

Create a struct called Wad that will have the value of the second parameter.
```solidity
library WadLib{
	uint256 public constant MULTIPLIER = 10 ** 18;

	struct Wad{
		uint256 value;
	}
}
```

Create the functions multiplaction, division and fraction
```solidity
library WadLib{
	uint256 public constant MULTIPLIER = 10 ** 18;

	struct Wad{
		uint256 value;
	}

	function mulWad(uint256 num1, Wad memory wad) internal pure returns (uint256){
		return (num1 * wad.value) / MULTIPLIER;
	}
	
	function divWad(uint256 num1, Wad memory wad) internal pure returns (uint256){
		return (num1 * MULTIPLIER) / wad.value;
	}

	// Third function is like the second but we return wad than int
	function fromFraction(uint256 numerator, uint256 demominator) internal pure returns (Wad memory){
	return Wad((numerator * MULTIPLIER) / demominator);
	}
}
```

Or more efficiently, is not to use [[Solidity Struct]] but with `type` keyword. In this case, when using the value of Wad, we `unwrap` it first, if want to create a Wad, we then `wrap` it. We also don't need to store it in the memory ebcause it is not a struct
```solidity
library WadLib{
	uint256 public constant MULTIPLIER = 10 ** 18;

	type Wad is uint256;

	function mulWad(uint256 num1, Wad wad) internal pure returns (uint256){
		return (num1 * Wad.unwrap(wad)) / MULTIPLIER;
	}
	
	function divWad(uint256 num1, Wad wad) internal pure returns (uint256){
		return (num1 * MULTIPLIER) / Wad.unwrap(wad);
	}

	// Third function is like the second but we return wad than int
	function fromFraction(uint256 numerator, uint256 demominator) internal pure returns (Wad){
	return Wad.wrap((numerator * MULTIPLIER) / demominator);
	}
}
```


Import it to the StableCoin code, change the division or multiplcation operation with that technique. For example
```solidity
import { WadLib } from "./WadLib.sol";

contract StableCoin is ERC20{
	using WadLib for uint256; // enable the use with integers
	// ...

	function _getDPCInUsd(uint256 surplus) private view returns(WadLib.Wad){
		return WadLib.fromFraction(depositorCoin.totalSupply(), surplus) ;
	}

    function depositCollateralBuffer() external payable{
	    // ...
		uint256 surplus = uint256(deficitOrSurplus);
		WadLib.Wad dpcInUsdPrice = _getDPCInUsd(surplus); // use Wad as type
		uint256 mintDPCAmount = ((msg.value.mulWad(dpcInUsdPrice )) / oracle.getPrice()); // call functions using uint values
		// ...
	}
}
```



# Metatags
###### Related: [[Stable Coin]], [[Solidity Inheritance]], [[MSG Variables Solidity]], [[Solidity Function Scope]], [[ERC-20 Token Creation]], [[Calling Contracts]]
###### Tags: 
###### Source: 

---