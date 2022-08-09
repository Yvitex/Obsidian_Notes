# Pixe.la
Is a habit tracking [[API]]. This is a more advance server that could do the 4 [[HTTP Request Verbs]] such as `get`, `delete`, `post`, `update` but in [[Python]]

Visit the website [here](https://pixe.la/) as well as its [documentation](https://docs.pixe.la/)

## Setup
Following the instruction from the documentation. We first need to setup the user account
![[Pasted image 20220720145508.png]]

In the page, we need exactly 4 parameters to be authentiticated
![[Pasted image 20220720145547.png]]

Import then the [[Requests module]] and ise the parameters
```python
import requests

pixe_url= "https://pixe.la/v1/users"
user_create_params = {  
    "token": "****",  
    "username": "****",  
    "agreeTermsOfService": "yes",  
    "notMinor": "yes",  
}

data = requests.post(url=pixe_url, json=user_create_params)
```

`requests.post` accepts 2 parameter which is `url` and `json`. It will return the status and we could view it using either the `.json` format or `.text` format
```python
import requests

pixe_url= "https://pixe.la/v1/users"
user_create_params = {  
    "token": "****",  
    "username": "****",  
    "agreeTermsOfService": "yes",  
    "notMinor": "yes",  
}

data = requests.post(url=pixe_url, json=user_create_params)
print(data.text)
```
![[Pasted image 20220720150252.png]]


## Create a Graph
Reading the documentation [here](https://docs.pixe.la/entry/post-graph). It is the same process but different parameters. Fetch the endpoint from the documentation and create a parameter dictionary that will store the required data
```python
import requests

TOKEN = "****" # our token password
USER = "****" # our username
```

Create this url, 
![[Pasted image 20220720154140.png]]

```python
import requests

TOKEN = "****" # our token password
USER = "****" # our username

create_graph_url = f"https://pixe.la/v1/users/{USER}/graphs"
```

Create the parameters
```python
import requests

TOKEN = "****" # our token password
USER = "****" # our username

create_graph_url = f"https://pixe.la/v1/users/{USER}/graphs"
graph_params = {
	"id": "work1",
	"name": "Work-out Frequency",
	"unit": "reps",
	"type": "int",
	"color": "kuro",
}
```

Then submit a post request using this parameters
```python
import requests

TOKEN = "****" # our token password
USER = "****" # our username

create_graph_url = f"https://pixe.la/v1/users/{USER}/graphs"
graph_params = {
	"id": "work1",
	"name": "Work-out Frequency",
	"unit": "reps",
	"type": "int",
	"color": "kuro",
}

data = requests.post(url=create_graph_url, json=graph_params)
```

Congratulation, you created an error
![[Pasted image 20220720154600.png]]

In the documentation, we could see this information, 
![[Pasted image 20220720154623.png]]

We forgot to apply the passwork which is our token. To do this is just to create an object that will handle it and include it as a parameter to the post request. This thing is called [[Request Header]]

We could do this
```python
import requests

TOKEN = "****" # our token password
USER = "****" # our username

create_graph_url = f"https://pixe.la/v1/users/{USER}/graphs"
graph_params = {
	"id": "work1",
	"name": "Work-out Frequency",
	"unit": "reps",
	"type": "int",
	"color": "kuro",
}

token_key = {
	"X-USER-TOKEN": TOKEN,
}

data = requests.post(url=create_graph_url, json=graph_params, token_key)
```
![[Pasted image 20220720155835.png]]

we could now visit it using this url
https://pixe.la/v1/users/YOURUSERNAME/graph/GRAPHID.html

## Create Input Pixel
To input a value to the graph we created, read this [documentation](https://docs.pixe.la/entry/post-pixel)
![[Pasted image 20220720182804.png]]

So the endpoint looks like this. And the parameters we need are
![[Pasted image 20220720183021.png]]

Example URL endpoint: https://pixe.la/v1/users/{username}/graphs/{id}

Simply do the following
```python
import requests

USER="yvitex"
id_name="workout1"

pixel_create_url= f"https://pixe.la/v1/users/{USER}/graphs/{id_name}"
```

Set the parameters
```python
import requests

USER="yvitex"
id_name="workout1"

pixel_create_url= f"https://pixe.la/v1/users/{USER}/graphs/{id_name}"
pixel_create_params= {
	"date": "something",
	"quantity": "200",
}
```

`date` parameter needs to be in this kind of format 20220720, which is year then month then day, we use teh [[Datetime]]
```python
import requests

USER="yvitex"
id_name="workout1"

pixel_create_url= f"https://pixe.la/v1/users/{USER}/graphs/{id_name}"
pixel_create_params= {
	"date": "something",
	"quantity": "200",
}

data = requests.post(url=pixel_create_url, json={pixel_create_params})
```

Don't forget the token
```python
import requests

USER="yvitex"
id_name="workout1"
TOKEN = ****

pixel_create_url= f"https://pixe.la/v1/users/{USER}/graphs/{id_name}"
pixel_create_params= {
	"date": "something",
	"quantity": "200",
}

token_key = {
	"X-USER-TOKEN": TOKEN
}

data = requests.post(url=pixel_create_url, json={pixel_create_params, token_key})
```


## Edit Pixels
```python
import requests
from datetime import datetime

USER="yvitex"
id_name="workout1"
TOKEN = ****

date_today = datetime.now()
edit_pixel_url = f"https://pixe.la/v1/users/{USER}/graphs/{id_name}/{date_today.strftime("%Y%m%d")}"

edit_pixel = {
	"quantity": "10"
}
```

Now we use the put request in order to update, remember the [[HTTP Request Verbs]]
```python
import requests
from datetime import datetime

USER="yvitex"
id_name="workout1"
TOKEN = ****

date_today = datetime.now()
edit_pixel_url = f"https://pixe.la/v1/users/{USER}/graphs/{id_name}/{date_today.strftime("%Y%m%d")}"

edit_pixel = {
	"quantity": "10"
}

token_key = {
	"X-USER-TOKEN": TOKEN
}

data = requests.put(url=edit_pixel_url, json=edit_pixel, headers=token_key)
```


# Deleting Input
We need the same url as editing the input pixels. Then authenticate it using the `headers` property
```python
import requests
from datetime import datetime

USER="yvitex"
id_name="workout1"
TOKEN = ****


token_key = {
	"X-USER-TOKEN": TOKEN
}

date_today = datetime.now()
edit_pixel_url = f"https://pixe.la/v1/users/{USER}/graphs/{id_name}/{date_today.strftime("%Y%m%d")}"
```

Use the delete request
```python
import requests
from datetime import datetime

USER="yvitex"
id_name="workout1"
TOKEN = ****

token_key = {
	"X-USER-TOKEN": TOKEN
}

date_today = datetime.now()
edit_pixel_url = f"https://pixe.la/v1/users/{USER}/graphs/{id_name}/{date_today.strftime("%Y%m%d")}"

requests.delete(url=edit_pixel_url, headers=token_key)
```
