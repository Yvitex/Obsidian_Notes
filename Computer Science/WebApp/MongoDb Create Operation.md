Create Operation

Start the server by typing mongod in the command line. The result should be similar like this...

![[Pasted image 20220601032148.png]]

Open another command line interface as the current terminal won't allow you to do anything. Then execute the mongo shell by typing mongo. 

![[Pasted image 20220601032202.png]]

If you need any help, just type help in the console, it will list some available commands.

![[Pasted image 20220601032238.png]]

Typing show dbs prints out the available databases

![[Pasted image 20220601032244.png]]

To create a new database, enter command use nameDB  , this will currently not be printed when you use show dbs in command line. Use any name of your liking for the nameDB

![[Pasted image 20220601032250.png]]

To insert or create data inside the nameDB, we call the create method db.collectionName.insertOne() or db.collectionName.insertMany(),  


![[Pasted image 20220601032257.png]]

Here is the syntax. 

![[Pasted image 20220601032303.png]]


To delete a database, we use... 

![[Pasted image 20220601032310.png]]

We firsr switch to the database to be deleted, and then we can use db.dropDatabase() to purge it down


