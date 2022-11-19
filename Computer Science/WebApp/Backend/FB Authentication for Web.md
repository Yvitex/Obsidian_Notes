# FB Authentication
Here's a quick [Documentation](https://www.passportjs.org/packages/passport-facebook/)

## Steps
 -  First is to go to [Meta's Developer Site](https://developers.facebook.com/) click somewhere until you find this page
 
 ![[Pasted image 20220624044039.png]]
Or simply just click[ here](https://developers.facebook.com/apps/)

 -  Create an App, Do whatever. 
 
 ![[Pasted image 20220624044348.png]]
 
 - In setting, in basic. Create a new platform and create your callback url
 
 ![[Pasted image 20220624044519.png]]
 
 - Also create a url for privacy policy and deletion, i just provided a dummy url for the deletion. But the best provacy policy generator is [privacypolicy.com](https://www.freeprivacypolicy.com/) 

 ![[Pasted image 20220624044606.png]]
 
 - In code. Install the passport for facebook.

```
$ npm install passport-facebook
```

 - Import the module to the source code. 
 
```javascript
const FacebookStrategy = require('passport-facebook').Strategy;
```

 - Get the FB_id, FB_Secret and callback. Apply it tot he following code. Remember to hide the keys using [[Environmental Variables]]
 
```js
passport.use(new FacebookStrategy({
    clientID: process.env.FB_ID,
    clientSecret: process.env.FB_SECRET,
    callbackURL: "http://localhost:3000/auth/facebook/secret"
  },

  function(accessToken, refreshToken, profile, cb) {
    User.findOrCreate({ facebookId: profile.id }, function (err, user) {
        console.log(user)
      return cb(err, user);
    });
  }
));
```

 - Provide the authentication code along with the redirect routes

```js
app.get('/auth/facebook',
  passport.authenticate('facebook'));

app.get('/auth/facebook/secret',
  passport.authenticate('facebook', { failureRedirect: '/login' }),
  function(req, res) {
    // Successful authentication, redirect home.
    res.redirect('/secrets');

  });
```

 - Setup the button in [[HTML]]
 
```html
<div class="card">
        <div class="card-body">
          <a class="btn btn-block btn-social btn-facebook" href="/auth/facebook" role="button">
            <i class="fab fa-facebook"></i>
            Sign In with Facebook
          </a>
        </div>
      </div>
```

```ad-Notice
collapse: open
Notice that in the button, we provided the route /auth/facebook that when accessed, will authenticate the user with facebook confirmation and then will redirect to the callback that will redirect to the main secret page

```

Here, we also used [[Social Button CSS]] to design the buttons. 

![[Pasted image 20220624045709.png]]

```ad-Notice
collapse: open
When user is already logged inside the web. He or she don't need to login again as long as he does not change his facebook account already logged in at the browser. 

```


To get more additional data, we use this other property
```js
passport.use(new FacebookStrategy({
    clientID: process.env.FB_ID,
    clientSecret: process.env.FB_SECRET,
    callbackURL: "http://localhost:3000/auth/facebook/secret",
    profileFields: ['id', 'displayName', 'name', 'photos', 'emails']
  },
));
```

In this way, we could get the photos and email from the facebook profile. Also, we need to do this to the main,
```js
app.get('/auth/facebook', passport.authenticate('facebook', {scope: ['email']}));
```

To get the profile picture though is a different process, we need to use the Graph API of facebook. The syntax is this
```js
passport.use(new FacebookStrategy({
    clientID: process.env.FB_ID,
    clientSecret: process.env.FB_SECRET,
    callbackURL: "http://localhost:3000/auth/facebook/secret"
  },

  function(accessToken, refreshToken, profile, cb) {
    User.findOrCreate(
	    { 
		    facebookId: profile.id, 
		    profilePic:  "https://graph.facebook.com/" + profile.id + "/picture?width=200&height=200&access_token=" + process.env.FB_ACCESS_TOKEN
		}, function (err, user) {
        console.log(user)
      return cb(err, user);
    });
  }
));
```

The website to get the access token is [here](https://developers.facebook.com/tools/explorer/)
