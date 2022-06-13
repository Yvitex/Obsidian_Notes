# What is a Dummy Variable?
This stores [[Binary ]] Information in a data table. So it can only have one of two values such as true or false, yes or no, male or female etc.

## Example
![[Pasted image 20220605154157.png]]

![[Pasted image 20220605153907.png]]

To find the number of houses located near Charles River. We could use [[Pandas]] `value_counts()` to extract this information

```
import pandas as pd
river_houses = data["CHAS"].value_counts()
print(river_houses)
```

this will output:
![[Pasted image 20220606101251.png]]
Reading the descriptions of the object data. We could say that there are 35 total houses recorded near the Charles River and a total of 471 who are not.





Related: [[First Step of Data Exploration]], [[Exploring the Data (Methodology)]]