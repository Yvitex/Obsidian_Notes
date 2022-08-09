# Workflow for Security Measures
Level 1:  Storing user information in the [[Databases|database]] such as email and password
Level 2:  [[Encryption]] of user information
Level 3:  Protecting and hiding sensitive variables using [[Environmental Variables]] (please do this before commiting to any version control system like [[Github]])
Level 4: Actually, we could use a [[Hashing Function]] instead rather than normal encryption to avoid hiding keys in an [[Environmental Variables]]. 
Level 5: We could use such modules called [[Passport]]s that could authenticate the user effectively, also have a builtin[[Hashing Function]] and [[Salting]] algorithm. 
Level 6: We could use [[OAuth]], to use third party websites such as fb, twitter, etc to authenticate the user plus backend data like their friend list etc. 













Remember: Mary Queen of Scots took 3 blows in the neck before complete decapitation because her encryption style was super duper weak. 


![[Pasted image 20220614163000.png]]


We could use this website called [password-checker](http://password-checker.online-domain-tools.com/) to evalutate our password and the time it takes to brute force attack it. The basic principle is, the longer the password, the harder it is to brute force the [[Hashing Function|Hash]], thoough some people use a very short password that makes them vulnerable, therefore we could use the art of [[Salting]] to increase their password's strength. 