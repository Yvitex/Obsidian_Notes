---
aliases: [normal function, view function]
---

# Solidity Main Functions
After creating the [[Solidity Smart Contract Setup]], next is we must know the types of functions available
There are 2 main types of functions called *normal* functions and *view* functions in [[Solidity Language]]

## View Function
View functions are used to view data and cannot change the state of something.
First is we create a name for our function such as:
```solidity
function calculateNum()
```

Then we append the type of the function, in our case, a view function
```solidity
function calculateNum() public view 
```

The compuler may warn us to use the pure type function
```solidity
function calculateNum() public pure
```

Next is we declare the return type
```solidity
function calculateNum() public pure return(uint){

}
```

Lastly is we create the code block
```solidity
function calculateNum() public pure return(uint){
	return 1;
}
```


## Normal Functions
Are used to change the state of something. 

First is to name the function in camel case
```solidity
function sendSomething()
```

Next is to declare the type of the function, normal function comes in varieety of types, in our case, it wll be `payable`
```solidity
function sendSomething() public payable{
	payable(msg.sender).transfer(calculateNum())
}
```

We could notice that for every function, we use some [[Solidity Function Scope]] declaration

[[MSG Variables Solidity]]