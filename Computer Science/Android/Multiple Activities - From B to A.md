---
aliases: []
---
We could pass data also from activity second to activity first. 
Using the previous code from [[Multiple Activities - From A to B]]. We add another logic to the second activity
```java
showGuess.setOnClickListener(view -> {  
    Intent intent = getIntent();  
    intent.putExtra("gagu", "Supot na bata");  
    setResult(RESULT_OK, intent);  
    finish();  
});
```

We get the intent, put an extra to that intent, set the result which accepts 2 argument, `RESULT_OK` which states the success and the intent. In the end we `finish()` this to avoid activity stacking and go out of that activity. 

Set up a requestCode
```java
private final int requestCodeInt = 2;
```

In the main activity, we change the `startAcitivity` to `startActivityForResult`
```java
startActivityForResult(intent, requestCodeInt);
```

Override onActivityResult
```java
@Override  
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {  
    super.onActivityResult(requestCode, resultCode, data);  
}
```

We could get data from this, be sure to create conditional check
```java
@Override  
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {  
    super.onActivityResult(requestCode, resultCode, data);  
  
    if(requestCode == requestCodeInt){  
        assert data != null;  
        String name = data.getStringExtra("gagu");  
        Log.d("Coder", name);  
        Toast.makeText(this, data.getStringExtra("gagu"), Toast.LENGTH_LONG).show();  
    }  
}
```

# Metatags
###### Related: 
###### Tags: #deprecated-no-solution
###### Source: 

---
