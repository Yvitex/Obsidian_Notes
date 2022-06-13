# How to deploy a web app in heroku?

For a much better tutorial: just read the documentation here (for node.js): https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up

 Install the Heroku CLI, check if everything is updated in your side. 
![[Pasted image 20220602032939.png]]


Go to your node.js folder you want to deploy and initialize it

![[Pasted image 20220602032946.png]]

Log-in to heroku

![[Pasted image 20220602032951.png]]

Create a heroku app

![[Pasted image 20220602032955.png]]

Create a file named Procfile
![[Pasted image 20220602033000.png]]

Inside procfile, assign web: node <filename> that you want to execute

![[Pasted image 20220602033048.png]]

Change your server to a dynamic port

![[Pasted image 20220602033438.png]]

Inside the package.json, under the lisence document, we add the engine-node version. Make sure your version is appropriate to the node you are using. 

![[Pasted image 20220602033029.png]]

Create a .gitignore hidden file

![[Pasted image 20220602033445.png]]

Inside the .gitignore, specify the node modules to be excluded. Heroku will just install their own instead. 
![[Pasted image 20220602033450.png]]


Commit everything again into git.

![[Pasted image 20220602033503.png]]

Push the files to heroku using command git push heroku main. 

![[Pasted image 20220602033101.png]]

Done

