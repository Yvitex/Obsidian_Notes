# Requests
[[Python]] way of utilizing various external [[API]] though the [[HTTP Request Verbs]] such as get, post, delete, update

## Get
```py
import requests

data = requests.get(url=some_url, params=some_params)
```

## Post
```py
data = requests.post(url=some_url, json=some_params)
```
