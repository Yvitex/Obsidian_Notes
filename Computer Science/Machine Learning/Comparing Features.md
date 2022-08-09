# Comparing Features
The job of a [[Machine Learning Algoritm]] is to find patterns throughout the data, but before that, our job is to find this pattern before we feed it to the data in order to understand what each feature does. 

To compare one [[(DM)Feature|feature]] to another, the most basic tool is the [[Comparing Data|crosstab()]]
![[Pasted image 20220804093434.png]]

If we compare the freqeuncy of values of sex, 1 or male is greater than 0 or female. How we knew this can be found on the data dictionary at [[Introductory Definitions]].
![[Pasted image 20220804093523.png]]

207 males and one 93 have a heart disease compared to 96 of the females and 72 of them have a heart disease which is almost 75% of the female clients. So therefore, if there is a female client, the machine will already recognize it as having a 75% change of having a heart disease. 

In this section, we are trying to familiarize ourselves witht he data, we are findins some patterns ourselves.

To establish communivation, use a [[Bar Plot(Pd)]]
![[Pasted image 20220804093958.png]]


See what features are interesting and compare it with the [[Target]] value. For example in this [[Dataframe (Pandas)|dataframe]]
![[Pasted image 20220804103109.png]]

We could compare the age, the thalach and the target at the same time. 
- thalach : maximum heart rate
- age : in years
- target : with disease or not

We could see that there must be some kind of connection between the three, we use a [[Scatter Plot]] rather than bar plot when it comes to large numbers of possible values in different frequency. 
![[Pasted image 20220804103232.png]]

And guess we are right, ther eis some form of [[Negative Correlation]] between age and heart rate. The older they are, the less their heart rate becomes. HEart disease is also clustered in younger ages compared to older, and the no heart disease fraction is denser in older age. But it is not a legitimate source of answer, it is a legitimate source of question,

The purpose of our [[Data Exploration]] is to get more questions, rather than answers. Why is it the data shows that there are less heart disease as the older they are?
![[Pasted image 20220804103710.png]]

We see in this diagram that 50 - 60 age is lot more denser than the rest and forms a [[Normal Distribution]]

Another way to comapre feature is through [[Correlation Matrix]]. To do this, simply call the `.corr()` method then insert it to a [[Seaborn Heatmap]]
![[Pasted image 20220804113114.png]]

Because classification values doesn't give legitimate values in terms of [[Correlation]], we focus on linear data or having [[Linearity]]
For example is maximum heart rate and target, target is [[Binary]] value but 0 is none and 1 is having, we could deduce something out of correlation using it but more than 2 classification would mess the correlation values like forexample, chest pain variable having 4 categories. 
We could see that the higher the heart rate is associated with appearance of heart disease. 




