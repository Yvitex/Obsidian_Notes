# Beautiful Soup 4
Here is the [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/), This supports both the html and xml files

To use it, first, import it.
```python
from bs4 import BeautifulSoup
```

After import, open your [[HTML]] or [[Android Studio|xml]] file. 
```python
from bs4 import BeautifulSoup

with open(file="something.html") as file:
	data = file.read()
```

Instantiate the beautiful soup class
```python
from bs4 import BeautifulSoup

with open(file="something.html") as file:
	data = file.read()

reader = BeautifulSoup(data, "html.scrapper")
```

Sometimes, we may want to use another module called `lxml`, [[lxml]]
```python
from bs4 import BeautifulSoup
import lxml

with open(file="something.html") as file:
	data = file.read()

reader = BeautifulSoup(data, "lxml")
```

Now, we could print the reader with preetify method to have indentation
```python
from bs4 import BeautifulSoup
import lxml

with open(file="something.html") as file:
	data = file.read()

reader = BeautifulSoup(data, "lxml")
print(reader.prettify())
```
![[Pasted image 20220721174346.png]]

Or extract specific tag like 
```python
from bs4 import BeautifulSoup
import lxml

with open(file="something.html") as file:
	data = file.read()

reader = BeautifulSoup(data, "lxml")
print(reader.title)
```
![[Pasted image 20220721174431.png]]

Or the tags only
```python
from bs4 import BeautifulSoup
import lxml

with open(file="something.html") as file:
	data = file.read()

reader = BeautifulSoup(data, "lxml")
print(reader.title.name)
```
![[Pasted image 20220721174533.png]]

Or the content only
```python
from bs4 import BeautifulSoup
import lxml

with open(file="something.html") as file:
	data = file.read()

reader = BeautifulSoup(data, "lxml")
print(reader.title.string)
```
![[Pasted image 20220721174612.png]]

