---
aliases: []
---
This android module is almost like [[Toast Module]] but with a little bit more functionality like having another click method such as "show more". We could simply replace the Toast Function with this, the arguments include the view, the string message, then the duration. The view must be the whole layout but it could work into any view, and everything shown in the application is a view. 
```java
Snackbar.make(view, R.string.see_status Snackbar.LENGTH_LONG).show()
```

What we could do to improve the functionality is to create a see mroe option. And we could do this by chaining another method called `setAction`
```java
Snackbar.make(view, R.string.see_status Snackbar.LENGTH_LONG)
	.setAction("Show More", new View.OnClickListener(){
		@Override
		public void onClick(View view){
			Log.d("Snackbar", "Working");
		}
	})
	.show()
```

Or in [[Lambda]] mpde
```java
Snackbar.make(view, R.string.see_status Snackbar.LENGTH_LONG)
	.setAction("Show More", view1 -> {
		Log.d("Snackbar", "working")
	})
	.show()
```

# Metatags
###### Related: 
###### Tags: #java-module 
###### Source: 

---