---
aliases: []
---
We could read it through the [documentation](https://google.github.io/volley/requestqueue.html)
Here is the full code
```java
public class MySingleton {
    private static MySingleton instance;
    private RequestQueue requestQueue;
    private ImageLoader imageLoader;
    private static Context ctx;

    private MySingleton(Context context) {
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

    public static synchronized MySingleton getInstance(Context context) {
        if (instance == null) {
            instance = new MySingleton(context);
        }
        return instance;
    }

    public RequestQueue getRequestQueue() {
        if (requestQueue == null) {
            // getApplicationContext() is key, it keeps you from leaking the
            // Activity or BroadcastReceiver if someone passes one in.
            requestQueue = Volley.newRequestQueue(ctx.getApplicationContext());
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

Put this code to another file which will be then used to the main activity code. This code will actually prevents your [[Volley Module]] from instantiating multiple times which is not efficient for the memory specially when you are making request many times. This is called [[Singleton Pattern]]

This code is specialized to store the images into the [[CPU Cache|cache]] rather than fetching it multiple times from an external server.
```java
private MySingleton(Context context) {
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
```

This code is where the magic happens. It will check if its instance is null, and if yes, it will create a new one, if it is not, it will return the instance in which we could use for a request.
```java
public static synchronized MySingleton getInstance(Context context) {
        if (instance == null) {
            instance = new MySingleton(context);
        }
        return instance;
    }
```

This code will get the RequestQueue that creates a queue where we could add the request. If and only if the requestQueue is null that we create a new queue. 
```java
public RequestQueue getRequestQueue() {
        if (requestQueue == null) {
            // getApplicationContext() is key, it keeps you from leaking the
            // Activity or BroadcastReceiver if someone passes one in.
            requestQueue = Volley.newRequestQueue(ctx.getApplicationContext());
        }
        return requestQueue;
    }
```

This code will add a request to the queue
```java
public <T> void addToRequestQueue(Request<T> req) {
        getRequestQueue().add(req);
    }
```

Now, import the necessary class to run this code. 

In our main activity code, we declare a variable first with a data type of RequestQueue. This will store our queue that we will get on the Singleton
```java
RequestQueue queue;
```

Now using the singleton, get its instance and provide the context, then get the queue
```java
queue = MySingleton.getInstance(this.getApplicationContext()).getRequestQueue();
```

We could also use `this` or `MainActivity.this` as the context, its the same. Then we could use the queue to add a request
```java
queue.add(requestObject);
```

# Metatags
###### Related: [[Singleton Pattern]], [[Volley Module]], 
###### Tags: 
###### Source: 

---