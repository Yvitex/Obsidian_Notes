# Three Sets
This is we did during the [[Splitting the Training and Testing Dataset]], but practically there is 3 sets we need to split, not only the training or test. 

This is a very important concept in [[Machine Learning]] where we split all [[(DM)Data]] into three different sets and they are
- [[Training Sets]]
- [[Validation Sets]]
- [[Test Sets]]

![[Pasted image 20220725150512.png]]

We set the trainign set to atleast 70% and the rest with 15%. 
This is like reviewing for the exam, we first train by reviewing some training set. Afterwards during the test, even though some questions might be different, we could make sense of it because we already saw something similar using the training set. We separate it, as because come and think of it, if we review the training set while having a test, then it is not called learning but cheating!!


```ad-Upset
title: They Can't be Together
collapse: open
The [[Training Sets]], the [[Validation Sets]] and the [[Test Sets]] do not see each other. They are alienated from one another

```

How can we create the 3 sets, we could do this using [[Python Slicing]]. Read [[Three Sets in Code]]


