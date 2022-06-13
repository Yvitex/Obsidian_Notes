# Get

Functions: Simply printing out the data whenever a client enter the url endpoint. 

In general endpoint:

Create a get request using express that when typed, will print out the data from the database to the browser. Refer here 

![[Pasted image 20220602035101.png]]

This will output

![[Pasted image 20220602035108.png]]

To a more specific route. We do use a route parameter. Depending on the value of the route parameter, we can input this value to the mongoose findOne() method to output it

![[Pasted image 20220602035114.png]]

But remember that to get the data, we must mind in our url encoding such as spaces is replaced by %20 and ? replaced by %3f

![[Pasted image 20220602035119.png]]

![[Pasted image 20220602035126.png]]

See the link below for more info about urlencoding

https://www.w3schools.com/tags/ref_urlencode.asp


Related: [[HTTP Request Verbs]]




