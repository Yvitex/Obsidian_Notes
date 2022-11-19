#python
# API 
API is a set of protocol that enable 2 software devices to communicate with each other 

There are many ways we could utilize an API, We just first need to identify their *endpoints*, read the parameters and voila. 
Here is an example of api providers call [Open Weather Map](https://openweathermap.org/api/one-call-api). To utilize their API, we need to authenticate first ourselves and then find their endpoints. 

Enpoint Example: https://api.openweathermap.org/data/2.5/onecall?lat={lat}&lon={lon}&exclude={part}&appid=[{API key}]

![[Pasted image 20220619040021.png]]
 Code 401 is a [[Http Status Code]] that means unauthorized. We can't access it without first getting an api key. But once we do and input all required parameters, then we could see the avaiable data for us.![[Pasted image 20220619040358.png]]
## Python
To call api inside python, we use the `requests` module.Note that this is not `request` but with s
```
import requests as rq
```
 
After that, we construct a parameter using a python dictionary. In open weather map, the required param are lat, lon, and appid which is the authentication key
```
params = {
	"lat": 14.131070,
	"long": 121.414570,
	"appid": "somerandomlygeneratedstring"
}
```

We will pass this parameter when we call our endpoint
```
response = rq.get(url="https://api.openweathermap.org/data/2.5/onecall", params)
```

Then we will check for error using `raise_for_status`
```
response.raise_for_status()
```

We will then convert the response into a [[Javascript|json]] format and pass the result to a variable
```
data = response.json()
```

Now we could print the data to access the json data.












One thing i noticed while reading the API is that the time date of sunset is gibbering incomplehensible mess of number string?? I found out that this was actually a time date based on [[UNIX Time]] that can be converted into [[UTC]] using this website called [Epoch Converter](https://www.epochconverter.com/)

Also, here is a good website for weather visualization : [Ventusky](https://www.ventusky.com/?p=60.1;20.2;5&l=temperature-2m&t=20220618/2100)


See an example of API using [[Twillio]]
