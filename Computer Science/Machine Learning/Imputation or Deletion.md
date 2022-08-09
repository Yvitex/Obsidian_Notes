# Imputation or Deletion
This is the continuation section of [[Dealing With Missing Values]]. We could either drop or add missing values. 
OF course, during [[Get the Data Ready|Data preparation]], when we want to encode strings into [[Binary]], it wont work because some have missing values, what we could do are the following.

To imputate, we may want to replace some missing categorigal string with "missing" string. For numbers integer, we may want to use the [[Mean]] of every possible values. For missing [[Target]] data. we may choose to drop the entire row

![[Pasted image 20220730100449.png]]

We could do this in 2 ways: 
[[Using Pandas Imputation and Deletion]]
[[Using Scikit-learn Imputation and Deletion]]

