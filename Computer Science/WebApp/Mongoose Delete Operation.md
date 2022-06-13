# Delete Method

![[Pasted image 20220602025554.png]]

We use deleteOne or deleteMany in this situation where first parameter is a filter or selector, second parameter is optional querym and third is a callback function. 

## Delete Many

![[Pasted image 20220602025607.png]]

This is the general syntax, where Person is the model, inside the first parameter is the limiter and we could also pass additional parameter inside by separating it with comma then stating a mongoDB query, 

![[Pasted image 20220602025625.png]]

We could also find the Id itself and delete that item using `findByIdAndRemove()` method,

![[Pasted image 20220602025631.png]]

The problem with this is that, it won't work if the callback error is not defined. So don't forget it. 

To remove a value in an array using MongoDB, what do we do? We could use the 
`$pull operator`

![[Pasted image 20220602025707.png]]

field1 is an array and the value| condition is the thing to be removed, each part encapsulated by 3 overlaying layers of curly braces. To delete, for an instance, a collection of document where one document stores an array of object such as

![[Pasted image 20220602025715.png]]

What can we do? Instead of using deleteOne or deleteMany that deletes the whole document itself rather than a specific element inside array, we could use...

![[Pasted image 20220602025721.png]]

This syntax will find find the name of the listItems and when found, will update the array. 

![[Pasted image 20220602025728.png]]

That's all.

This is very similar to [[MongoDB Delete Operation]] when using the terminal
