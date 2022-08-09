# Update Method

To update a certain object in the database. the syntax to use in mongoose is `Model.updateOne()` or `updateMany()`

![[Pasted image 20220602025503.png]]

This accepts 3 parameters, first is the filter, in the example above, we selected the specific id of the object to be modified, second parameter is the value to be added or modify. Last but not the least is the callback function which checks if an error occurs or not. 

This is very similar to [[MongoDB Update Operation]] when using the terminal