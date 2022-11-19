---
aliases: []
---
The problem of our previous appraoch in getting the component views in the [[JAVA]] code was we are using this:
```java
item = findById(R.id.item);
```

This is a very expensive method that will traverse the whole component to find this specific id, if we have more components, then the time it takes to load this will be very slow [[Linear  Time Complexity|O(n)]].

Luckily, we have this technique method called Data Binding. 

How we do this is a quite strange process, We need to access the Gradle folder, and modify the `build.gradle` module
![[Pasted image 20221021152711.png]]

This is the second file in the gradle script. Inside the android brackets, we set a new property called `buildFeatures`
```gradle
android {
	buildFeatures {
		dataBinding true
	}
}
```

Sync it to update the changes made in the gradle. Now update our xml and enclose all the component inside a layout tag.  IT is also required to transfer the first 3 xlmns to the layout. 
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools">  
      
    <androidx.appcompat.widget.LinearLayoutCompat  
        android:layout_width="match_parent"  
        android:layout_height="match_parent"  
        android:background="#009688"  
        android:orientation="vertical"  
        tools:context=".MainActivity">  
        
    </androidx.appcompat.widget.LinearLayoutCompat>  
  
</layout>
```

Now, declare a variable of `ActivityMainBinding` type. 
```java
private ActivityMainBinding binding;
```

Now we assign it on the onCreate function with `DataBindingUtil.setContentView()`, this will have 2 arguments, 
```java
binding = DataBindingUtils.setContentView()
```

This will have 2 arguments, the context and the view, the view is the layout we are using
```java
binding = DataBindingUtils.setContentView(this, R.layout.activity_main);
```

Now we could use this binding to call the ids.
```java
binding.submitMyHobbies.setOnClickListener(new View.OnClickListener() {  
    @Override  
    public void onClick(View view) {  
        binding.hiddenText.setText(String.format("Hobbies: %s", binding.hobbyInput.getText().toString().trim()));  
        binding.hiddenText.setVisibility(View.VISIBLE);  
  
        InputMethodManager inputmngr = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);  
        inputmngr.hideSoftInputFromWindow(view.getWindowToken(), 0);  
    }  
});
```

If you are using data binding, then surely you must have this generated automatically
![[Pasted image 20221024145628.png]]




# Metatags
###### Related: [[Android Studio]]
###### Tags: 
###### Source: 

---