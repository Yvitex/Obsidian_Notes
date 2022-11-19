---
aliases: [color.xml]
---

We could change the color in [[Android Studio]] by getting the view through their id then tweak the method `setTextColor`. This will have some strange arguments but we could do it easily using `Color.parseColor()`

```java
moneyValue.setTextColor(Color.parseColor());
```

This will accept a [[Hexadecimal Notation]] value
```java
moneyValue.setTextColor(Color.parseColor("#00ff00"));
```

We could also use the builtin Colors
```java
moneyValue.setTextColor(Color.Magenta);
```

But, we could see that [[Android Studio]] actually provide us with a Color.xml. We could input our values here
```xml
<color name="myColor">#0BE486</color>
```

Then how we will import this into our [[JAVA]] code is through `ContextCompat`
```java
moneyValue.setTextColor(ContextCompat.getColor(MainActivity.this, R.color.myColor));
```

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---
