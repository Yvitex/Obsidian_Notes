---
aliases: []
---
Here, we will use a query `$push` combined with `model.updateOne`  method. 
```js
function pushNewBook(User, username, Book){
    User.updateOne({username: username}, {$push: {uploadedBooks: [Book]}} ,function(err, resultUser){
	if(err){
		console.log(err)
	}
	else{
		console.log("No err")
	}
```

User is the mongoose model, we are finding a data with the same username and when we get the data, we will use the query to push a data to the uploadedBooks property. We enclose it with \["data"]. 


# Metatags
###### Related: [[Mongoose Update Operation]]
###### Tags: 
###### Source: 

---