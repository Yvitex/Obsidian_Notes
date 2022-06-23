# How does Hashing works?
Let me ask you a question: find 2 numbers that when multiplied will result into 377. How long does it takes you to find the answer?

Now, multiply 13 by 29. How fast did you do it?

Fundamentally, that is how hashing functions work, easy to [[Encryption|encrypt]], hard to decrypt. And that is the point of it.

## MD5
One of the types of hashing is MD5. dunno the difference yet but to import it in node.js, we could use this module called [md5](https://www.npmjs.com/package/md5) 
```
npm i md5
```

Now import it inside the source code. To use it, just treat it as a function that will accept a string argument.
```
const md5 = require(md5)

encrypted = md5("Helloworld")
```

In an instance we are using it to encrypt a password in a registration form, we could just hash the password whenever they login to enter the webapplication.

## Bcrypt
A more secure algoritm than MD5. If md5 hashes can be generated, 20billion hashes per second, this algorithm could only be generated, 17 thousand hashes per second. It encourages the use of [[Salting|salt rounds]] to increase the complexity of hashes. 

```
npm install bcrypt
```

To hash:
```
const bcrypt = require('bcrypt');
const saltRounds = 10;

bcrypt.hash(stringpassword, saltRounds, function(err, result){
	// Here we will save data to datavase
})
```

To compare
```
bcrypt.compare(whatUserTyped, DB.password, function(error, res){
	if(res == true){
		//what to do?
	}
})
```