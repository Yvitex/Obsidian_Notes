# Twillio
Twillio is a multipurpose API. Using [[Python]], we could read the [documentation](https://www.twilio.com/docs/sms/quickstart/python) thatw ill enable you to send sms to your phone. 
```python
from twilio.rest import Client
import os
```

next is we will conenct to the client using our identification and token that are found after sining up into twillio website
```python
account_sid = os.environ['TWILIO_ACCOUNT_SID']
auth_token = os.environ['TWILIO_AUTH_TOKEN']
client = Client(account_sid, auth_token)
```

Now, we will send the message to the user using our number found isnide twillio
```python
message = client.messages.create(  
    body="Bro, it's goin to ☔ so you better bring an ☂ umbrella",  
    from_='+1732657889380',  
    to='+635443124909'  
)
```


Similar on how we could use *smtplib* to send an email. And also here we using [[Environmental Variables]]

```python
print("hello world")
```

