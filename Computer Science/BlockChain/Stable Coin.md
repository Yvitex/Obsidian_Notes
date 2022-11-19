---
aliases: []
---
Is another aspect of the [[BlockChain]] in which the coin does not change in price for example, theater. We could exchange tether with a collateral or usd. This stable coin is backed by a certain service in which promise that you could widraw the token anytime. The problem is that, this is a centralized token. 

We could also use an [[ERC-20]] token as a collateral. The problem is that, it will change the value everytime. To fix this, we could implement some over collaterlization or spending more and getting less technique. ![[Pasted image 20221103143923.png]]

They should pay for 1000 usd and get 500usd. This will make a safety margin for when the value of ether drops. But, this will be done hidden from sight. We use the depositors money in order to pay for the overcollaterization. 

Our stable coin is just like [[ERC-20]] volatile tokens but with additional functionalities. This includes, redeeming and minting the token, a way for people to exchange [[ERC-20]] token for stable coins and a way to deposite excess tokens as an over collaterization
![[Pasted image 20221103150606.png]]

Of course, there is a benefit for depositing some tokens. The first incentive is that, the price of token may rise in the future which, ![[Pasted image 20221103150756.png]]

If we exchange usd for stable token at 1000 usd, and the depositor over collateralize the pool with 500 usd. The exchnager will get 1000usd worth of stable token, the depositor gets none. But in the future, if the token rice in price, the depositor will get more thean the exchanger. ![[Pasted image 20221103150953.png]]
The pool now is worth 2250 usd butt, the exchanger will still get 1000 usd while the other have more. Second incentive is that we will pay some extra token to the depositor which comes from depositors redeeming their tokens and minting them.

Why? If the price of token goes below, then the depositor will lose money rather than earning them![[Pasted image 20221103151319.png]]
Since the extra token from our original pool is lessm then the excess would fo for the depositor which is less than the primary deposited. 

Furthermore, they have a chance to get liquedated![[Pasted image 20221103151429.png]]
At this case, we will kick the depositor out of the pool. First we do is to redeem their coins to prevent further decrement, second we kick out depositors whos cash value is 0, then add another depositor in replacement that could repay the loss value
 ![[Pasted image 20221103151812.png]]


# Metatags
###### Related: [[ERC-20]], [[Solidity Inheritance]], [[Smart Contracts Popular Types|stable coins]]
###### Tags: 
###### Source: 

---