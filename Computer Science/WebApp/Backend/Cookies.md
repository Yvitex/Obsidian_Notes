# What are Cookies?

![[Pasted image 20220618032308.png]]

That's one thing but another is what we could use to store a user's activity inside the browser when using a certain web application.

When adding cart items in the e-commerce website such as amazon, even if we suddenly close our activity tab, the website do not forget our activity in that website. The reason is, because of what we called *Cookies*
The process in fact. as soon as we create a [[Restful Api Architecture Post|post request]] to add an item to the cart, cookies are sent to our browser so that when we exit, and reenter the website once again, the browser will send the cookies to the website and renders the activity of the user.   
![[Pasted image 20220618033315.png]]

When we delete all cookies, then the added item cart will reset. Does this means those what we add to the cart is still not being saved to the server's [[Databases|database]]?

Cookies are also used in authentication to remember the user instead of repeatedly logging in, and that is through the use of [[Passport]]
