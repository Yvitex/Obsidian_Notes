# Atlas

A cloud database provided by mongoDB. This will enable a web application to utilize the databse 24/7 without the local workstation but through a server.

Set-Up

1. Sign-up
![[Pasted image 20220602030331.png]]

2. Select AWS for a free cluster tier

![[Pasted image 20220602030338.png]]

![[Pasted image 20220602030347.png]]



3. Create new user in security and set privelege to admin.

![[Pasted image 20220602030354.png]]

![[Pasted image 20220602030402.png]]

4. Set whitelist for select access anywhere

![[Pasted image 20220602030450.png]]

5. Now connect to your cluster and choose connect with mongo shell

![[Pasted image 20220602030456.png]]
6. Now, select your version and copy the command provided to be pasted on the command line
![[Pasted image 20220602030503.png]]


7. Enter the command to the CLI and enter the password from the user in step 3

![[Pasted image 20220602030612.png]]

8. Now you can control the cloud database using the command line

![[Pasted image 20220602030515.png]]

9. To connect your app, simply select the connect you app option

![[Pasted image 20220602030529.png]]

10. Now copy the provided url

![[Pasted image 20220602030535.png]]

11. Apply the url inside the applicaiton code, if using mongoose, do not remove the last part whcih is /databaseName and apply the password in the specified part

![[Pasted image 20220602030540.png]]

