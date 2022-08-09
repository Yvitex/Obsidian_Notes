# Request Header
Are things like `X-USER-TOKEN` that is used to hide the token name in the url parameters, When we construct some [[API]] request that needs authentication, we always construct it like this in [[Python]]
```python
requests.get(url=some_url, params=some_params)
```

Despite our knowledge, this is exactly equivalent to the exact url appended with some appersand and queries like
https://web/something?apiKey=1241423424&color=black

The api key is visible for everyone though [[Common Ports|port]] https is encrypted which means it is safer than http. 

To avoid this, we use this thing called request header, an example could be found in [[Pixe.la]] tutorial

To include this on python program, we do this
```python
token_key = {
	"X-USER-TOKEN": "12121313"
}

requests.get(url=some_url, params=some_params, headers=token_key)
```