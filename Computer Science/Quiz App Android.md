---
aliases: []
---
The stucture of the files are as follow
![[Pasted image 20221027090544.png]]

## Controller
In the controller file, create a new class with this name that extends to `Application`. We do this so that we could use the methods inside the `Application` class
```java
public class AppController extends Application {
}
```

Copy the codes from the lesson in [[Singleton Pattern with Volley Module]]. Rename the instances as `AppController` and import all necessary class
```java
public class AppController extends Application {  
    private static AppController instance;  
    private RequestQueue requestQueue;  
    private ImageLoader imageLoader;  
    private static Context ctx;  
  
    private AppController(Context context) {  
        ctx = context;  
        requestQueue = getRequestQueue();  
  
        imageLoader = new ImageLoader(requestQueue,  
                new ImageLoader.ImageCache() {  
                    private final LruCache<String, Bitmap>  
                            cache = new LruCache<String, Bitmap>(20);  
  
                    @Override  
                    public Bitmap getBitmap(String url) {  
                        return cache.get(url);  
                    }  
  
                    @Override  
                    public void putBitmap(String url, Bitmap bitmap) {  
                        cache.put(url, bitmap);  
                    }  
                });  
    }  
  
    public static synchronized AppController getInstance(Context context) {  
        if (instance == null) {  
            instance = new AppController(context);  
        }  
        return instance;  
    }  
  
    public RequestQueue getRequestQueue() {  
        if (requestQueue == null) {  
            // getApplicationContext() is key, it keeps you from leaking the  
            // Activity or BroadcastReceiver if someone passes one in.            requestQueue = Volley.newRequestQueue(ctx.getApplicationContext());  
        }  
        return requestQueue;  
    }  
  
    public <T> void addToRequestQueue(Request<T> req) {  
        getRequestQueue().add(req);  
    }  
  
    public ImageLoader getImageLoader() {  
        return imageLoader;  
    }  
}
```

We could remove unnecessary codes such as the image [[CPU Cache|cache]] mechanism with [[Java Constructor]] also the if `instance == null` conditional check as we are using the `Application` class's this as the context constantly so we don't need also the parameters. 
```java
public class AppController extends Application {  
    private static AppController instance;  
    private RequestQueue requestQueue;  

	// Removed Constructor image cache
  
    public static synchronized AppController getInstance() {  
	    // Remove Conditional statement
        return instance;  
    }  
  
    public RequestQueue getRequestQueue() {  
        if (requestQueue == null) {  
		    // Use this as the context
			requestQueue = Volley.newRequestQueue(this.getApplicationContext());  
        }  
        return requestQueue;  
    }  
  
    public <T> void addToRequestQueue(Request<T> req) {  
        getRequestQueue().add(req);  
    }  
  
    @Override  
    public void onCreate() {  
        super.onCreate();  
        instance = this;  
    }  
}
```

The link [[API]] of the application will be 
```java
String url = "https://raw.githubusercontent.com/curiousily/simple-quiz/master/script/statements-data.json";
```

This looks like
![[Pasted image 20221027094513.png]]

An array so
Now to request this do:
```java
JsonArrayRequest arrayRequest = new JsonArrayRequest(Request.Method.Get, url, null, response -> {
	Log.d("Result", response.toString());
}, error -> {
	Log.d("Result", error.toString());
})
```

To make a queue. we will import the `AppController` class to the maina ctivity then
```java
AppController.getInstance().addToRequestQueue(arrayRequest);
```

## Model
Our model will be the questions. What we could do is create a class based on it with getter and setter and constructor. Put the file inside the model folder
```java
public class Question {  
     private String question;  
     private Boolean answer;  
  
    public Question(String question, Boolean answer) {  
        this.question = question;  
        this.answer = answer;  
    }  
  
    public Question() {  
    }  
  
    public String getQuestion() {  
        return question;  
    }  
  
    public void setQuestion(String question) {  
        this.question = question;  
    }  
  
    public Boolean getAnswer() {  
        return answer;  
    }  
  
    public void setAnswer(Boolean answer) {  
        this.answer = answer;  
    }  
}
```

## Data
Our data will be the collection of question called repository. Create a new file called repository and Create a [[Hash Table]] for this based on Question Model
```java
public class Repository{
	private ArrayList<Question> questionArrayList = new ArrayList<Question>;
}
```

Now, create a method that will get the question. Simply, we will move our previous code in the main activity and make it functional in this class
```java
import android.util.Log;  

import com.android.volley.Request;  
import com.android.volley.toolbox.JsonArrayRequest;  
import com.yvitex.quizapp.controller.AppController;  
import com.yvitex.quizapp.model.Question;  
  
import java.util.ArrayList;  
  
public class Repository {  
    String url = "https://raw.githubusercontent.com/curiousily/simple-quiz/master/script/statements-data.json";  
    private ArrayList<Question> questionArrayList = new ArrayList<>();  
  
    public ArrayList<Question> getQuestion(){  
  
        JsonArrayRequest jsonArray = new JsonArrayRequest(Request.Method.GET, url, null, response -> {  
            Log.d("Result", response.toString());  
        }, error -> {  
            Log.d("Result", error.toString());  
        });  
  
        AppController.getInstance().addToRequestQueue(jsonArray);  
  
        return null;  
    }  
}
```

The result will be null temporarily. We will modify this so that we could add this to questionArrayList as an object. The first thing we need to do is to create a for loop with index that could output the Question and Answer
```java
public ArrayList<Question> getQuestion(){  
  
    JsonArrayRequest jsonArray = new JsonArrayRequest(Request.Method.GET, url, null, response -> {  
        for (int i = 0; i < response.length(); i++) {  
            try {  
                Log.d("Response", "Question: " + response.getJSONArray(i).get(0));  
                Log.d("Response", "Answer: " + response.getJSONArray(i).getBoolean(1));  
            } catch (JSONException e) {  
                e.printStackTrace();  
            }  
  
        }  
  
    }, error -> {  
        Log.d("Result", error.toString());  
    });  
  
    AppController.getInstance().addToRequestQueue(jsonArray);  
  
    return null;  
}
```

Create a question object and apply these values and then add it to the jsonArrayList [[Hash Table]]. 
```java
public class Repository {  
    String url = "https://raw.githubusercontent.com/curiousily/simple-quiz/master/script/statements-data.json";  
    private ArrayList<Question> questionArrayList = new ArrayList<>();  
  
    public ArrayList<Question> getQuestion(){  
  
        JsonArrayRequest jsonArray = new JsonArrayRequest(Request.Method.GET, url, null, response -> {  
            for (int i = 0; i < response.length(); i++) {  
                try {  
                    Question newQuestion = new Question(  
                            response.getJSONArray(i).getString(0),  
                            response.getJSONArray(i).getBoolean(1)  
                    );  
  
                    questionArrayList.add(newQuestion);  
                      
                } catch (JSONException e) {  
                    e.printStackTrace();  
                }  
  
            }  
  
        }, error -> {  
            Log.d("Result", error.toString());  
        });  
  
        AppController.getInstance().addToRequestQueue(jsonArray);  
  
        return questionArrayList;  
    }  
}
```

Remember to use Error-Catch etc to fail gracefully when there is an error. Now, the problem left at hand is the fact that when we instantiate and catch the return value to a variable, it produce an empty array
```java
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);  
  
    ArrayList<Question> questions = new Repository().getQuestion();  
    Log.d("Question", questions.toString());  
}
```

![[Pasted image 20221027110207.png]]

## Interface Class
we fix this using [[Asynchronous programming]] technique, because we don't have such thing like [[Async and Await]], we will use an [[Interface Class]]. To do this, using the method in our Repository class that is supposed to return an array list of data, we will apply a callback in which is an interface class. This is  the key code: `final InterfaceMethodName variable`
```java
public ArrayList<Question> getQuestion(final AsyncInterfaceQuestionArray callback){  
  
    JsonArrayRequest jsonArray = new JsonArrayRequest(Request.Method.GET, url, null, response -> {  
    // ...
    AppController.getInstance().addToRequestQueue(jsonArray);  
    return questionArrayList;  
}
```

Now, right click and create an interface class in this keycode. ![[Pasted image 20221028114143.png]]

```java 
public interface AsyncInterfaceQuestionArray {  

}
```

Create a method that will indicate weather the method creates a result or not. This will have a parameter of supposed to be the result data type
```java
import com.yvitex.quizapp.model.Question;  
import java.util.ArrayList;  
  
public interface AsyncInterfaceQuestionArray {  
    void processFinished(ArrayList<Question> questionArrayList);  
}
```

Don't create a body. Just stay right there. Now in our Repository class, we will add a conditional check in which if the callback is not null, then we will call the method `processFinished()` with the result as the argument
```java
public ArrayList<Question> getQuestion(final AsyncInterfaceQuestionArray callback){  
  
    JsonArrayRequest jsonArray = new JsonArrayRequest(Request.Method.GET, url, null, response -> {  
        for (int i = 0; i < response.length(); i++) {  
            try {  
                Question newQuestion = new Question(  
                        response.getJSONArray(i).getString(0),  
                        response.getJSONArray(i).getBoolean(1)  
                );  
                questionArrayList.add(newQuestion);  
            } catch (JSONException e) {  
                e.printStackTrace();  
            }  
			// Callback check
            if( callback != null) {  
                callback.processFinished(questionArrayList);  
            }  
        }  
    }, error -> {  
        Log.d("Result", error.toString());  
    });  
    AppController.getInstance().addToRequestQueue(jsonArray);  
    return questionArrayList;  
}
```

Now, int he MainActivity class, from this code.
```java
ArrayList<Question> questions = new Repository().getQuestion();  
Log.d("Question", questions.toString());
```

We will use to callback to override the method from the interface and get the information with it.
```java
ArrayList<Question> questions = new Repository().getQuestion(new AsyncInterfaceQuestionArray(){
	@Override  
	public void processFinished(ArrayList<Question> questionArrayList) {  
	    Log.d("Question", questionArrayList.toString());  
	}
});  
```

Now we could output its [[Memory address]]
![[Pasted image 20221028115610.png]]

We could override the `toString()` method in the Question Model Class to output the thing exactly, not the memory.
```java
@Override  
public String toString() {  
    return "Question{" +  
            "question='" + question + '\'' +  
            ", answer=" + answer +  
            '}';  
}
```


# Metatags
###### Related: [[Model-View-Controller Architecture]], [[Volley Module]], [[Singleton Pattern with Volley Module]]
###### Tags: 
###### Source: 

---