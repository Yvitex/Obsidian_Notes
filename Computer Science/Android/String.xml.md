# String xml
This contains all the string text contain in buttons and all kind of text displayed on the user interface.
![[Pasted image 20220711141834.png]]

As we could see on the image above, The IDE is giving us some warnings we must fix. The problem is, the text are hard coded, we need to get the string we display from string.xml and not just typing it directly. To fix this, just tap into the error and press fix.
![[Pasted image 20220711142033.png]]

This will extract the string to the strings.xml.![[Pasted image 20220711142059.png]]
We need to rename it properly Make it very descriptive
![[Pasted image 20220711142148.png]]

Now the string is not dependent on the moneyValue name coming fron the string.xml. Here are the resources from strings.xml now that we extracted all strings
![[Pasted image 20220711142506.png]]

Another way to refactor this is by clicking the button in the right of the text field in attribute
![[Pasted image 20221021053346.png]]

We could add resource to it by clicking the plus symbol then click <u>string value</u>. We could simply choose the created resources to be applied. 
![[Pasted image 20221021053425.png]]

