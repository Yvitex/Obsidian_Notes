---
aliases: []
---

Is a way to organize your android application views in linear stack either horizonally or vertically. By default, [[Android Studio]] uses ContrainLayout but we could change it inside the [[Android Studio|xml]] by changing the first line whichis:
```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent">
```

A contraintLayout to
![[Pasted image 20221021052251.png]]

We have 2 choices, either we use the traditional LinearLayout or the advance, we will use the advance because it is the latest

```xml
<androidx.appcompat.widget.LinearLayoutCompat xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:tools="http://schemas.android.com/tools"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent">
```

I inserted 2 items which is an ImageView and a TextView. And then shit happens and it look like this
![[Pasted image 20221021052539.png]]

```ad-Attention
title: TextView Problem
collapse: open
Some TextView like the profile picture won't be shown in real application so use it just as a reference. 

```

I want it to stack vertically, what we could do is to go to the <u>Orientation</u> attribute and click vertical![[Pasted image 20221021052635.png]]

To center the Views, use the attribute <u>LayoutGravity</u> and set it to center
![[Pasted image 20221021052757.png]]

![[Pasted image 20221021052817.png]]

I did also apply <u>Bold</u>, adjust the <u>TextSize</u> of the name and apply <u>Padding</u> of 8[[Density Independent Pixel|dp]] for all sides.

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---