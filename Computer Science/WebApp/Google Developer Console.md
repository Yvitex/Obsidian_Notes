# Google Developer Console
## How to setup your first app?
In dropdown menu, click new project
![[Pasted image 20220620155112.png]]

Next is to select your project name
![[Pasted image 20220620155341.png]]

In the OAuth consent screen, create your own popup screen when accessing user information

![[Pasted image 20220620155459.png]]


Set up the baisc informations, you may leave the domain blank.
![[Pasted image 20220620155644.png]]

Next is we could select API, or other permission to get some information  from third party website and edit them. 
![[Pasted image 20220620160246.png]]

We could enable other api by pressing Google API Library. In the most basic case, we just need the email, profile and id. 
![[Pasted image 20220620160329.png]]

Next is we need to create credentials
![[Pasted image 20220620163058.png]]

And of course, in the dropdown, we choose, *OAuth client ID*
![[Pasted image 20220620163122.png]]

In creation, choose the appropriate application to be used
![[Pasted image 20220620163204.png]]

Into the javascript origin, we will write the base url of where we will apply an authentication
![[Pasted image 20220620163529.png]]

In the *Authorized Redirect Link*, we will apply the route in which we will redirect after authentication
![[Pasted image 20220620163644.png]]

This example is based on Angela's tutorial in [[Passport]] where she build's a secret app.

After that, you will be given you authentication keys
![[Pasted image 20220620164320.png]]


