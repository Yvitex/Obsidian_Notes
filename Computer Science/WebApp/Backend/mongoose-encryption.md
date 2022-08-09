# How to use mongoose-encryption?
Read the documentation [here](https://www.npmjs.com/package/mongoose-encryption)

## Installation
First is to install it using the terminal. 

```
npm i mongoose-encryption
```

After this, we shall import it inside node.js

```
const encryption = require('mongoose-encryption')
```

## How to encrypt fields?
First of, the easiest way to do this is by creating a **secrete string**
```
const secret = "helloworld"
```

Then we use this secret string inside a plugin called **enrypt** for our [[Mongoose Create Operations|schema]]
```
var userSchema = new mongoose.Schema({
    name: String,
    age: Number
    // whatever else
});

const secret = "helloworld"

userSchema.plugin(encrypt, {secret: secret})
```

By default, this will   encypt eveyrthing in the [[Databases|database]] except from the `_id` and `_v`, but we could do this for specific variables. Just add the `encyptedFields` key inside the javascript object of the plugin

```
userSchema.plugin(encrypt, {secret: secret, encyptedFields: ["password"]})
```

Make sure you wrote this code just before creating the model.
The code above will only encrypt the passwork field, creating 2 encrypted variable in the [[Databases|database]]
![[Pasted image 20220614040944.png]]

loging into the website causes the password to be jumbled up like this
![[Pasted image 20220614041017.png]]

