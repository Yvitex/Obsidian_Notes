---
aliases: []
---
Address is a unique type in [[Solidity Language]]. Generally there are 2 types of address which is an ordinary address and a payable which could look like this in code:
```solidity
address myAddress1;
address payable myAddress2;
```

Payable keyword is used to state that the address will have to receive a token or something else. It is the receiver while the ordinary one is the sender. We could easily convert between the 2 using their methods
```solidity
address(myAddress2);
payable(myAddress1);
```

Address have several methods builin to its class. 
- balance
- transfer
- call

This is used to upload the user balance.
```solidity
address.balance()
```

This is the non recommended way to transfer or send token to a receiver
```solidity
payable(msg.sender).transfer(amount);
```

This is the same as using
```solidity
(bool success,) = payable(msg.sender).call{gas: 2300, value: amount}("");
require(success, "Transfer Failed");
```

They have fixed gas price and will cause a failure if the gas price required is greater than what we have set up. We do this to prevent the [[Re-Entrancy Problem]] but hell, this is very non flexible code for doing so. Instead it is recommended to use this
```solidity
(bool success,) = payable(msg.sender).call{value: amount}("");
require(success, "Transfer Failed");
```

No gas fixed. Also, we put [[Solidity Language|ABI]] inside the parenthesis with strings quotes and [[Reverting a Contract]] when this fails. 

# Metatags
###### Related: [[Solidity Language|ABI]], [[Solidity Data Types]]
###### Tags: 
###### Source: 

---