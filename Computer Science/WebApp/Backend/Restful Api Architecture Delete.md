# Delete

Delete in general is a way of wiping out all contents of a collection in a database

To demonstrate this, switch to delete http request in the [[Postman Software]]
![[Pasted image 20220602035426.png]]


In our code. Use the` app.delete()` method to receive the http delete request and inside, we will use mongoose deleteMany method without condition to delete all data.

![[Pasted image 20220602035430.png]]

Related: [[HTTP Request Verbs]]
