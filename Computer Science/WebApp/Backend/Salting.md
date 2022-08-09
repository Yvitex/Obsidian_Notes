# Salting
![[Pasted image 20220618041612.png]]


*Salting* simply means adding a random character to a person's password to increase it's hashing complexity, if a user's password is just a string with 5 or 6 characters such as 'qwerty' or 'iluvu', we could add a randomly generated string to increase the complexity of its [[Hashing Function]]

To increase its complexity more, we could do a *salting rounds* which is basically adding the same salt string to the end of the hash, then hashing it again, repeatedly. Two salt rounds means hashing it two times, 10 salt rounds means hashing it 10 times. The recommended hashing rounds is 10 because the more you do this, the slower the algorithm would function. 

Aside from [[Hashing Function|MD5 hashing]] algoritm, we have a Bcrypt hashing algo. 

## BCrypt
```
npm install bcrypt
```

Here is the documentation of [bcrypt](https://www.npmjs.com/package/bcrypt) 

First is we need to indicate a saltting round after importing module
```
const bcrypt = require('bcrypt');
const saltRounds = 10;
```

After so, we could use this to generate a bcrypt hashes using `hash` method, first parameter will accept the normal plain string, next is the saltRoounds consisting of integer and lastly is the result error calback function
```
bcrypt.hash(plainText, saltRounds, function(err, res){
	
})
```
Inside that method, we will use a [[Mongoose Create Operations]] to save the data to database


To compare it to a user input such as when logging in with their password, we do use the `compare` method
```
User.findOne({email: email}, function(err, userFound){
	if(userFound){
		bcrypt.compare(plainText, userFound.password, function(error, result){
			if(result == true){
				res.render()
			}
		})
	}
})

```
Here we use a [[Mongoose Read Operation]] to find the data needed

(Note: Bcrypt does not work in unstable version of nodes)