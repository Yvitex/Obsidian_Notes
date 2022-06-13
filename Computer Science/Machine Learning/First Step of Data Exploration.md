# Exploring the Data
To demonstrate this, we will use skylearn's sample data

![[Pasted image 20220605153738.png]]

![[Pasted image 20220605153747.png]]

Outputting it will product this data

![[Pasted image 20220605153800.png]]

A [[Python Programming|python]] dictionary of some sort. To disseminate the attributes of this object, we could use the python function named `dir()`

![[Pasted image 20220605153849.png]]

This will show the attributes we could use, Now we could tap into this attribute using either dot notation or bracket notation.

![[Pasted image 20220605153902.png]]

![[Pasted image 20220605153907.png]]

This says that there are 13 features, 506 [[Exploring the Data (Methodology)|data points]], the name of each features and etc. We could also tap inside the data to confirm it by printing

![[Pasted image 20220605153939.png]]

Now we could see that there are 506 rows of data with 13 columns. Also, data attribute of boston_dataset is of type ndarray or n-dimensional array

To view the column names we could tap into the feature_names... Feature is also called an attribute in machine learning and it is infact the independent variable of our data.

![[Pasted image 20220605153956.png]]

As we can see, we can't see the prices in the table, because it was separated to another set of array, we could tap into this using target attribute.

![[Pasted image 20220605154010.png]]


### Using Pandas DataFrame
We could organize this data into table using [[Pandas|panda's module]].

![[Pasted image 20220605154108.png]]

Using the module, we could set each data and column names into a beautiful table by using DataFrame attribute.

![[Pasted image 20220605154126.png]]

In here, we set each data using boston's data attribute and the columns with each of their own names.  
  
Now, the data will look like this

![[Pasted image 20220605154143.png]]

Now we add the boston's target namely the price to the table using bracket notation

![[Pasted image 20220605154157.png]]

To check wether the numbers of data for each column, we could use the `count()` method
![[Pasted image 20220605154213.png]]

Each rows in this table or datapoints is also called number of instances.  
  
To check wether the data is incomplete, or has a null value we could use an `isnull()` method

![[Pasted image 20220605154229.png]]

This will print out the whole table, if everything is false, they good to go but to simplify it further we could attach a `.any()` method that will print out if any of the column has missing values.

![[Pasted image 20220605154241.png]]

Alternatively we could also use `.info()` method

![[Pasted image 20220605154252.png]]

float64 means it is a decimal number with lots of accuracy and takes up a lot of memory. 64 bits to be exact or 8 bytes. This also show the total memory usage which is 55.5 kb



[[Exploring the Data (Methodology)]]

