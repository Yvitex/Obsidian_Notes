# Using Put in Creating an API

`.put()` is included in the  `route()` chains methods, simply type in ,put after the end of the parenthesis

![[Pasted image 20220602054059.png]]

After that. we could update the database using the `Model.update()` method
![[Pasted image 20220602054242.png]]

The skeletal syntax goes like this
![[Pasted image 20220602054352.png]]

where we search the specific document using` {conditions}`, then update is in `{updates}`, and we also need to overwrite it to replace all content of the document and create a callback fucntion that will detects an error

But through my experimentation, theproper functionality of this syntax do not work as of 2022,  with mongoose that do not allow `{overwrite: true } `with `updateOne() `and `update()`already deprecated as in the example above

Removing these outdated methods...
![[Pasted image 20220602054804.png]]

Which is already equivalent to `.patch()` method where we only overwrite specific data rather than the whole document.

See [[Restful Api Architecture Patch]]

In this case, we are inclined to use mongoose's `Model.updateOne()`

![[Pasted image 20220602055856.png]]

Credits : *[StackOverflow](https://stackoverflow.com/questions/67141121/put-method-in-express-giving-empty-array)*

![[Pasted image 20220602060138.png]]


Targetting this document shown in [[Studio3T]]

![[Pasted image 20220602060119.png]]


We could call this endpoint and update the content without touching the title
![[Pasted image 20220602060259.png]]

Database updated into
![[Pasted image 20220602060320.png]]

As we can see, the title disappears. 

Related: [[HTTP Request Verbs]], [[Mongoose Update Operation]], [[Mongoose Route Chaining Method]]

