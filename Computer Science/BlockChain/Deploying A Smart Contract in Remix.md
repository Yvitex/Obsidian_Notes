---
aliases: []
---
Go to the [[Ethereum]] icon and choose London Virtual Machine or berlin whatever.
![[Pasted image 20221101095030.png]]

This is good if you are just testing something, press deploy. Set the value to ether so that it could be easier to understand rather than in gwei
![[Pasted image 20221101095124.png]]

The deployment is just another contract without a recipient. That is its true nature. So when we press deploy, we reduce the amount of ether that we have as you could see
![[Pasted image 20221101095308.png]]

This contract:
```solidity
// SPDX-Licence-Identifier: MIT
pragma solidity 0.8.17;

contract MyContract{
    function getRandomNumber() public pure returns(uint){
        return 9;
    }

    function getLessValue() external payable{
        uint256 randomNumber = getRandomNumber();
        uint256 ethRefund = msg.value / randomNumber;
        payable(msg.sender).transfer(ethRefund);
    }
}
```

Will create this contract. 

![[Pasted image 20221101095331.png]]



Of courl, get random will only show the values which is indicated as 9![[Pasted image 20221101095442.png]]

While get less value will reduce our token. Set the value to 1 ether, 
![[Pasted image 20221101095532.png]]

Then press getLessvalue function
![[Pasted image 20221101095608.png]]

Our cash had been reduced to ashes. 

We could also use Metamask in this case. Choose injected provider
![[Pasted image 20221101095651.png]]

We have 0.05 ether. ![[Pasted image 20221101095708.png]]
Once you press deploy, metamask will create a contract that will show you the [[Gas Fees]]. Yep, because it is a contract. 
If we press the function get less and set the wei value to 1000000. It will show this. The transaction will take a little while to finish. 

![[Pasted image 20221101100017.png]]

Now, our token had been reduced to nothingness. 






# Metatags
###### Related: [[Smart Contract]], [[Ethereum Virtual Machine]]
###### Tags: 
###### Source: 

---