# Using Patch method

Using the [[Mongoose Route Chaining Method]], we can also chain the patch method by using `.patch()` to the syntax. 

![[Pasted image 20220602061757.png]]

In here, we will call the `.updateOne()` method to select the item we will update
![[Pasted image 20220602062149.png]]

In here, we will use `$set: req.body` for a dynamic selection of keys but only to the already existing keys. Remember that patch, as well as [[Restful Api Architecture Put|put]] are only used for updating keys and not for adding them. With this, we could select any keys and update the document without affecting other keys.

Related: [[HTTP Request Verbs]], [[Mongoose Update Operation]]
