---
aliases: []
---
We already know that we could use functions such as `call` or `staticall` in the address. For example
```solidity
(bool success,) = someAddress.call{value: amount, gas: forwardGas}(abiCode);
(bool success,) = someAddress.staticcall{value: amount, gas: forwardGas}(abiCode);
```

`staticcall` is simply like `call` but doesn't change anything, only used for `pure` and `view` function.

abiCode contains the function to call. 
The same could go for [[Smart Contract]]s. We could put it in a variable and use their functions inside
```solidity
ERC20 public erc20;
IERC20 public ierc20;

erc20.transfer(address, amount);
uint balance = ierc20.balanceOf(address);
```

`IERC20` is an [[Interface Class]] and we use this class best for other contracts that is not ours.
Take note of these parameters
```solidity
contract.pay{gas:2000, value: 1 ether}(param1, param2);
```

We have function parameters and transaction parameters. Transaction parameters are enclosed with curly braces and function parameters is what we indicated in the function. Transaction parameter is the amount of gas and amount to be sent in a transaction, etc.






# Metatags
###### Related: 
###### Tags: 
###### Source: 

---