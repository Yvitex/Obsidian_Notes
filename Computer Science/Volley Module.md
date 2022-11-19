---
aliases: [Requesting API in Android, StringRequest(), JsonArrayRequest(), JsonObjectRequest()]
---
For example, we have this [[API]]
```java
String url = "https://jsonplaceholder.typicode.com/todos";
```

We will use volley module to fetch or get the data. To install it, go to the [documentation](https://google.github.io/volley/)
Do this:
![[Pasted image 20221026110316.png]]

Go to the Gradle and add the line to the dependenies then sync it as necessary
![[Pasted image 20221026110423.png]]


Because we are using the Internet, we need to add permission to the android, in the AndroidManifest [[Android Studio|xml]], add this code
```xml
<uses-permission android:name="android.permission.INTERNET" />
```

Now we could use the volley module. First of all, we create a queue using it.  Inside the OnCreate [[Android App Life Cycle]] method, add this code. This should have an argument which is the context. 
```java
RequestQueue queue = new Volley.newRequestQueue(this);
```

## String Output
IF we are trying getting a string. Create a request after this
```java
StringRequest req = new StringRequest(Request.Method.GET, url, new Response.Listener<String>() {  
    @Override  
    public void onResponse(String response) {  
  
    }  
}, new Response.ErrorListener() {  
    @Override  
    public void onErrorResponse(VolleyError error) {  
          
    }  
});
```

This method have 4 arguments, the first is the type of [[HTTP Request Verbs]]. The second is the url where we are getting the [[API]]. The third is the response detector which is simplu the `Response.Listener`, the fourth is the `Response.ErrorListener` which output an error. This could be simplified using [[Lambda]]. 
```java
StringRequest req = new StringRequest(Request.Method.GET, url, response -> {  
    Log.d("Result", response.substring(0, 100));  
}, error -> {  
    Log.d("Result", "Failed to get" + error.toString());  
});
```

Since we dont want to output all the strings, we limit it to 100 characters. We could get the string to the response and get the error in the error callback. 

Now we want the queue to add that req, we do
```java
queue.add(req);
```

The end. ![[Pasted image 20221026113814.png]]
In this case, this is quite wrong, we are using String to output a [[JSON]] file and there are better ways of doing this.

## JSON
Instead of using a `StringRequest`, use a `JSONArrayRequest`. This will have 4 arguments, the method, the url, the request and the response
```java
JsonArrayRequest arrayRequest = new JsonArrayRequest(Request.Method.GET, url, null ,  response -> {  
    Log.d("Result", response.toString());  
}, error -> {  
    Log.d("Result", "Failed to get" + error.toString());  
});  
  
queue.add(arrayRequest);
```

We temporarily set the 3rd argument to null cos we don't need it yet. 
The output was not enclosed in an array. ![[Pasted image 20221026134258.png]]
Since we are already using an array, we could fetch the length of this array
```java
JsonArrayRequest arrayRequest = new JsonArrayRequest(Request.Method.GET, url, null ,  response -> {  
    Log.d("Result", "Length: " + response.length());  
}, error -> {  
    Log.d("Result", "Failed to get" + error.toString());  
});  
```

We could see this output 200 items. We could also get the specific json object inside the array with an index. This will require us to built a try/catch filter
```java
JsonArrayRequest arrayRequest = new JsonArrayRequest(Request.Method.GET, url, null ,  response -> {  
	JSONObject jsonData = null; // JSON variable type declared
	try {
		jsonData = response.getJSONObject(1);
		Log.d("Result", jsonData.toString());  
	}
	catch (JSONException e) {
		e.printStackTrace();
	}	
	
}, error -> {  
    Log.d("Result", "Failed to get" + error.toString());  
});  
```

![[Pasted image 20221026141848.png]]

We could builf a for loop or whatever to traverse this shit. Either way, we could also get something specific from the object. Perhaps, if you just want the title then we use `getString()` with the argument of the name key. 
```java
JsonArrayRequest arrayRequest = new JsonArrayRequest(Request.Method.GET, url, null ,  response -> {  
	JSONObject jsonData = null; // JSON variable type declared
	try {
		jsonData = response.getJSONObject(1);
		Log.d("Result", jsonData.getString("title"));  
	}
	catch (JSONException e) {
		e.printStackTrace();
	}	
	
}, error -> {  
    Log.d("Result", "Failed to get" + error.toString());  
}); 
```

We could do also `getBoolean()` etc etc. Also, if this request in not an array but a pure JSON object, then we use `JsonObjectRequest()`
```java
JsonObjectRequest objectRequest = new JsonObjectRequest(Request.Method.GET, url, null ,  response -> {  
	Log.d("Result", response.getString("title");  
}, error -> {  
    Log.d("Result", "Failed to get" + error.toString());  
}); 
```


# Metatags
###### Related: [[Android Studio]], [[API]], [[HTTP Request Verbs]]
###### Tags: 
###### Source: 

---