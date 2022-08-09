# Python Project
We will utilize the [[Python OOP]] to do this.
First, we need to search how we could fetch datas regarding the price of flights, the [[API]] we could use is [Tequila Api](https://tequila.kiwi.com/portal/docs/tequila_api/search_api). 
![[Pasted image 20220721103034.png]]

![[Pasted image 20220721103044.png]]

![[Pasted image 20220721103654.png]]

There are 5 required parameters to fetch some data, and first, we need to create a solution. 
![[Pasted image 20220721103125.png]]

We choose the meta search API integration. Then choose one way and return
![[Pasted image 20220721103153.png]]

Name the solution then create
![[Pasted image 20220721103223.png]]

Extract the given [[API]] to a [[Python Environmental Variables]]
![[Pasted image 20220721103250.png]]

Using [[Python OOP]], we create a new class called FlightSearch, the attributes we need are simply the given parameters we already knew
```python
class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
```

One of the required parameters too is the range of dates for flights and it should be arranged in this format day/month/year. We need a [[Datetime]] module to cure this. Also the [[Python Environmental Variables]] should use [[OS module]] and dot-env
```python
from datetime import date
from dotenv import load_dotenv, find_dotenv
import os

class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()
```

`date.today` is another method other than using `datetime.now` in [[Datetime]] module. Using the data on that variable, we will calculate the date for tommorow, but we need not be hasty, if you are thinking we could just add 1 to the day, you are wrong as some months there are only 30 days, some have 31. We need to use an offset method called `relativedelta`
Create a method that will calculate the date tommorow
```python
from datetime import date
from dotenv import load_dotenv, find_dotenv
import os

class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()

	def get_date_tomorrow(self):  
	    date_tomorrow = self.date_today + relativedelta(days=1)  
	    return date_tomorrow
```

Simply add the date today and the `relativedelta` with offset of 1 day. Next is to create another method that will get the date 6 months after tommorow. The problem is, we can't use the relativedelta to do this, i mean we could like setting the days as 365/2 if it accepts float value but there is a more efficient way on doing this using a module called `dateutil`
```python
from datetime import date
from dotenv import load_dotenv, find_dotenv
from dateutil.relativedelta import relativedelta
import os

class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()

	def get_date_tomorrow(self):  
	    date_tomorrow = self.date_today + relativedelta(days=1)  
	    return date_tomorrow
```
[Source](https://stackoverflow.com/questions/546321/how-do-i-calculate-the-date-six-months-from-the-current-date-using-the-datetime)

Using the `relativedelta` method, we could do the same thing but now with months!
```python
from datetime import date
from dotenv import load_dotenv, find_dotenv
from dateutil.relativedelta import relativedelta
import os

class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()

	def get_date_tomorrow(self):  
	    date_tomorrow = self.date_today + relativedelta(days=1)  
	    return date_tomorrow

	def future_month(self):  
	    return self.get_date_tomorrow() + relativedelta(months=6)
```

The remaining problem is that the date is not arranged in the desired order. Create a function that will do this and convert it into a string.
```python
class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()

	def get_date_tomorrow(self):  
	    date_tomorrow = self.date_today + relativedelta(days=1)  
	    return date_tomorrow

	def future_month(self):  
	    return self.get_date_tomorrow() + relativedelta(months=6)

	def arrange_date(self, old_date):
		day = old_date.day  
		months = old_date.month  
		year = old_date.year  
		return f"{day}/{months}/{year}"
```

Now, we could create a function that will search for flights and price baby. Import the request module
```python
from datetime import date
from dotenv import load_dotenv, find_dotenv
from dateutil.relativedelta import relativedelta
import os
import requests
```

Create a method that will accept 2 parameter code, which is the airport location and then the destination location
```python
class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()

	def get_date_tomorrow(self):  
	    date_tomorrow = self.date_today + relativedelta(days=1)  
	    return date_tomorrow

	def future_month(self):  
	    return self.get_date_tomorrow() + relativedelta(months=6)

	def arrange_date(self, old_date):
		day = old_date.day  
		months = old_date.month  
		year = old_date.year  
		return f"{day}/{months}/{year}"

	def flight_search(self, from_destination, to_destination):
		params = {  
		    "fly_from": from_destination,  
		    "fly_to": to_destination,  
		    "date_from": self.arrange_date(self.get_date_tomorrow()),  
		    "date_to": self.arrange_date(self.future_month())  
		}
```

Fill the required parameters like the above. Get the token to an object then proceed to the request
```python
class FlighSearch():
	def __init__(self):
		self.endpoint = "https://tequila-api.kiwi.com/v2/search"  
		self.token = os.getenv("TEQUILA_KEY")  # API key
		self.date_today = date.today()

	def get_date_tomorrow(self):  
	    date_tomorrow = self.date_today + relativedelta(days=1)  
	    return date_tomorrow

	def future_month(self):  
	    return self.get_date_tomorrow() + relativedelta(months=6)

	def arrange_date(self, old_date):
		day = old_date.day  
		months = old_date.month  
		year = old_date.year  
		return f"{day}/{months}/{year}"

	def flight_search(self, from_destination, to_destination):
		params = {  
		    "fly_from": from_destination,  
		    "fly_to": to_destination,  
		    "date_from": self.arrange_date(self.get_date_tomorrow()),  
		    "date_to": self.arrange_date(self.future_month())  
		}
		token_auth = {  
		    "apikey": self.token  
		}  
		  
		response = requests.get(url=self.endpoint, params=params, headers=token_auth)  
		return response
```

When we create an object, we should see this as the response
![[Pasted image 20220721110533.png]]





