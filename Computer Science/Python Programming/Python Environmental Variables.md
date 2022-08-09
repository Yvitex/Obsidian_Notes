# Environmental Variable
[[Python]] way of creating [[Environmental Variables]]

First is to initialize the use of a virtual environment
```shell
$ py -3 -m venv venv
```

This will create a venv file when we `ls` print [[File Manipulation Command|command]]. NExt is to activate it
```shell
$ venv/Scripts/activate
```

If, microsoft blocks this command, set the execution policy to remote-signed in window powershell
```shell
$ Set-ExecutionPolicy RemoteSigned
```

To set it back
```shell
$ Set-ExecutionPolicy Restricted
```

Next is to install the dot env library
```shell
$ pip install python-dotenv
```

Create a new file called *.env*
Inside it, we will create the environment variables. 
```text
HELLO=HWLLO UWU
```

Inside the python source code, we import the following
```py
import os
from dotenv import load-dotenv, find-dotenv 
```

Load the dot env's `find-dotenv`
```py
import os
from dotenv import load-dotenv, find-dotenv 

load-dotenv(find-dotenv)
```

Next is to use the `os` module to ouput the dotenv values
```js
import os
from dotenv import load-dotenv, find-dotenv 

load-dotenv(find-dotenv)
print(os.getenv('HELLO'))
```
![[Pasted image 20220720042052.png]]


