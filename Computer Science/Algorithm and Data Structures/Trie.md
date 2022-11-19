---
aliases: [Prefix Tree]
---
# Trie
Also called as prefix tree from the word "retrieval".
This is another type of [[Tree Data Structure]] that is specialized on searching strings. 
![[Pasted image 20221005031419.png]]

Think of it like an auto-completion system, when you input "A", it immediately knew that it might be "ARE" or "AS". Google use this too to store sentences or words. 

As we could see, this is not a [[Binary Tree]] because the first layer might have 26 nodes in total. But this is more efficient than that when it comes to strings, it outperforms based on [[Big O Asymptotic Analysis|time complexity]] and [[Space Complexity]]. 

The [[Big O Asymptotic Analysis|time complexity]] of this part is O(length of word), if we are searching for "NEWS", it will only traverse into 4 nodes rather than all nodes so the lookup is fast. 










# Metatags
###### Related: [[Tree Data Structure]]
###### Tags: #incomplete 
###### Source: 

---