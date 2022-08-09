# Datetime Module
Here is the [documentation](https://www.w3schools.com/python/python_datetime.asp) regarding it.

## Date today
```python
from datetime import datetime

date_now = datetime.now()
print(date_now)
```

The other way is using the `date` method
```python
from datetime import date

date_now = date.today()
print(date_now)
```

## String Time
One of the most cool thing about this module is its ability to be formatted easily using the `strftime` method
```python
from datetime import datetime

date_now = datetime.now()
print(date_now.strftime("%Y%m%d"))
```

Here are the list of formatting
![[Pasted image 20220720184152.png]]

Included in the documentation.

## Relative Delta
It is a way to create an offset from the datetime object, like calculating the date of tommorow
```python
from datetime import date, relativedelta

date_now = date.today()
print(date_now + relativedelta(days=1))
```
