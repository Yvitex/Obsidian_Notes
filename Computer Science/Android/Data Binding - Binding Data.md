---
aliases: []
---
It is  similar to the [[Data Binding - Binding Views]] concept except we are going to create a new class and set the text in real time compilatio rather than setting it to the [[String.xml]]. 

The first thing to do is to create a new package beside MainActivity.java under the java directory. 
![[Pasted image 20221024092441.png]]


Under the data packag, create a class called Bio
![[Pasted image 20221024092650.png]]

Create a private variables for all TextView in the android application
```java
package com.example.bio.data;

public class Bio  {  
    private String name;  
    private String hiddenHobbies;  
}
```

Create a constructor that will set the values of this
```java
public class Bio  {  
    private String name;  
    private String hiddenHobbies; 

	public Bio(String name, String hiddenHobbies){
		this.name = name;
		this.hiddenHobbies = hiddenHobbies;
	}
	// since we also want this to have an empty arguments, we could overload
	public Bio(){  
      
	}
}
```

Set then a getter and setter
```java
public class Bio  {  
    private String name;  
    private String hiddenHobbies;  
  
    public Bio(String name, String hiddenHobbies){  
        this.name = name;  
        this.hiddenHobbies = hiddenHobbies;  
    }

	public Bio(){  
      
	}

    public String getName(){  
        return this.name;  
    }  
  
    public void setName(String name){  
        this.name = name;  
    }  
  
    public String getHiddenHobbies() {  
        return hiddenHobbies;  
    }  
  
    public void setHiddenHobbies(String hiddenHobbies){  
        this.hiddenHobbies = hiddenHobbies;  
    }  
}
```

We are done here for now, next is to go to the main activity layout. After setting the layout, Set a data tag
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools">  
  
    <data></data>
    ...
</layout>
```

Inside this data tag, we will set a variable
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools">  
  
    <data>
    <variable 
	    name=""
	    type=""
    />
    </data>
    ...
</layout>
```

We could set the name as anythign, type should be the class we just created which is the package name + the file name
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:app="http://schemas.android.com/apk/res-auto"  
    xmlns:tools="http://schemas.android.com/tools">  
  
    <data>
    <variable 
	    name="bio"
	    type="com.example.bio.data.Bio"
    />
    </data>
    ...
</layout>
```

we then modify any existing TextView that we have. 
```xml
<TextView  
    android:id="@+id/name"  
    style="@style/paragraphStyle"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:layout_gravity="center"  
    android:shadowColor="#090909"  
    android:text="@string/name"  
    android:textColor="#000000"  
    android:textColorLink="@color/teal_200" />
```

Instead of having the text refer to the [[String.xml]]. We are going to use the class. SO. We change the `android:text="@string/name"` to something like `android:text="@{bio.name}"` This is just  a curly braces enclosing the variable name in the xml layout and the variable name in the Bio class.
```xml
<TextView  
    android:id="@+id/name"  
    style="@style/paragraphStyle"  
    android:layout_width="wrap_content"  
    android:layout_height="wrap_content"  
    android:layout_gravity="center"  
    android:shadowColor="#090909"  
    android:text="@{bio.name}"  
    android:textColor="#000000"  
    android:textColorLink="@color/teal_200" />
```

Since the other one have this parameters
```xml
<TextView  
    android:id="@+id/hiddenText"  
    style="@style/paragraphStyle"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    android:visibility="gone" />
```

We could create another parameter for `android:text=""`
```xml
<TextView  
    android:id="@+id/hiddenText"  
    style="@style/paragraphStyle"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    android:text="@{bio.hiddenHobbies}"
    android:visibility="gone" />
```

Now in the main activity java, we could set the class
```java
private ActivityMainBinding binding;
private Bio bio = new Bio();
```

Next is that we could set the name from that class and the using the binding created in the [[Data Binding - Binding Views]] section bind the bio class
```java
binding = DataBindingUtils.setContentView(this, R.layout.activity_main);
bio.setName("Yvitex");
binding.setBio(bio);
```

![[Pasted image 20221024095801.png]]

When we enter something to the input or plaintextview, and press done. it should be the corresponding string for our hidden textview.

```java
binding.submitMyHobbies.setOnClickListener(new View.OnClickListener() {  
    @Override  
    public void onClick(View view) {  
        bio.setHiddenHobbies(String.format("Hobbies: %s", binding.hobbyInput.getText().toString().trim()));  
        binding.hiddenText.setVisibility(View.VISIBLE);  
    }  
});
```

This won't work as expected, but. We must clear up first all the binding after setting the hobbies. Add `binding.invalidateAll()`
```java
binding.submitMyHobbies.setOnClickListener(new View.OnClickListener() {  
    @Override  
    public void onClick(View view) {  
        bio.setHiddenHobbies(String.format("Hobbies: %s", binding.hobbyInput.getText().toString().trim()));  
        binding.invalidateAll();
        binding.hiddenText.setVisibility(View.VISIBLE);  
    }  
});
```

![[Pasted image 20221024101035.png]]



# Metatags
###### Related: 
###### Tags: 
###### Source: 

---