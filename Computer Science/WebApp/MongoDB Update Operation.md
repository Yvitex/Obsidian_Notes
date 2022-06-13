# Update Operation

![[Pasted image 20220602022713.png]]

![[Pasted image 20220602022718.png]]

![[Pasted image 20220602022725.png]]

Using db.collection.updateOne(), we can overwrite the whole document or add and modify a single key-value. the first parameter is the filter that specifies the target and the second parameter is the value being changed. If we forgot the $set method before declaration, it will replace the whole document leaving only a single key-value and the _id key immutable value, becareful. 




