# Function Scope
There are 4 main types of function scope in [[Solidity Language]]
- public
- private
- internal
- external

| scope    | Call from outside | Call from inside the contract | Call from inherited contract |
| -------- | ----------------- | ----------------------------- | ---------------------------- |
| public   | ✅                | ✅                            | ✅                           |
| private  |         ❌          | ✅                            |         ❌                      |
| external | ✅                |                ❌                |    ❌                           |
| internal |          ❌          | ✅                            | ✅                             |

We could change the code we have on our [[Solidity 2 Main Function]]

```solidity
function calculateNum() private pure return(uint){
	return 1;
}
```

We call this private because we do not need to call it outside the source code and it does not need to be inherited

```solidity
function sendSomething() external payable{
	payable(msg.sender).transfer(calculateNum())
}
```

As we do not need this code to run internally. 

```ad-note
collapse: open
We ended at public vs private function in Solidity fundamentals

```


