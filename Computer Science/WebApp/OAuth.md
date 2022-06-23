# Open Authentication
A token based authorization
Enables a webapplicaiton or other forms to use a third party website to authenticate the user and access some data. 

## Advantage
1. Granular Access Level - Could allow only specific parts to be fetched
2. Read and Write Access - Can allow us to write or get some information to the third party server
3. Revoke Access - User can revoke our webapplication using third party website giving much freedom to the user


After gaining access to the website using this form of authentication. We are able to receive an *authentication code* which then could be exchange for *Access Token* 

## How to Authenticate Using Googgle?
We first initialize our [[cookies]] or session as well as [[Passport]]. In [passport.js](https://www.passportjs.org/packages/) documentation we could see a lot of packages or strategies we could use to authentical the user.  In our case, we will use the latest version of google authentication called [ passport-google-oauth20](https://www.passportjs.org/packages/passport-google-oauth20/) , 

According to the documentation, we need to first set-up our [[Google Developer Console]] and save the google id and google secret into a [[Environmental Variables]]

We need to isntall the package first.

```
npm install passport-google-oauth20
```

Then import the module inside the source code
```
const GoogleStrategy = require('passport-google-oauth20').Strategy;
```


Next, is to cop- ehem, I mean, to import the code from the documentation and replace the `clientID`, `clientSecret`, `callbackURL` . In the callback URL, we supply the Autherized Redirect URL from the [[Google Developer Console]]. 
```
passport.use(new GoogleStrategy({

    clientID: process.env.CLIENT_ID,
    clientSecret: process.env.CLIENT_SECRET,
    callbackURL: "http://localhost:3000/auth/google/secret",

  },

  function(accessToken, refreshToken, profile, cb) {
    User.findOrCreate({ googleId: profile.id }, function (err, user) {
        console.log(user)
      return cb(err, user);
    });
  }
));
```
This is placed after deserialization stated in [[Passport]]

There are also few modifucation in our [[Mongoose Create Operations|mongoose]] schema. 
```
const UserSchema = mongoose.Schema({
	email: String,
	password: String,
	googleId: String,
})
```

Yep, we need to add `googleId` as a string. `email` and `password` are  when we are storing user data 'locally' directly to the database

Also, `findOrCreate` function doesn;t exist, we need to import it in npm, the module called [mongoose-findOrCreate](https://www.npmjs.com/package/mongoose-find-or-create)
```
npm i mongoose-findorcreate
```

This will enable the functionality that when mongoose, does not find [[Mongoose Read Operation|find]] anythin, it will create it as a new data input in oour database.

```
const findOrCreate = require('mongoose-find-or-create');
```

After that, we need to plug it in, as a plugin in a mongoose schema.
```
UserSchema.plugin(findOrCreate);
```
This is placed after creating a schema

Next is to add this copy pasted syntax. This will authenticate the user using their google account.  In our scope object, we only want the profile so,

```
app.get('/auth/google',
  passport.authenticate('google', { scope: ['profile'] }));
```

This will be applied along with the [[HTML]] button such as 
```
<div class="col-sm-4">
      <div class="card social-block">
        <div class="card-body">
          <a class="btn btn-block" href="/auth/google" role="button">
            <i class="fab fa-google"></i>
            Sign Up with Google
          </a>
        </div>
      </div>
    </div>
```

![[Pasted image 20220620171003.png]]

We could get this color by uting [[Social Button CSS]]. Then adding `btn-social` and `btn-google`
```
<div class="col-sm-4">
      <div class="card social-block">
        <div class="card-body">
          <a class="btn btn-block btn-social btn-google" href="/auth/google" role="button">
            <i class="fab fa-google"></i>
            Sign Up with Google
          </a>
        </div>
      </div>
    </div>
```

Now, pressing the button will now deliver us to the list of our account
![[Pasted image 20220620171310.png]]

Proceeding will cause an error as we haven't yet specified what will happen afterwards. What happen afterwards is that it will [[HTTP Request Verbs|get]] the route we specified on [[Google Developer Console]]'s Authorized Redirect. 
To fix this, we need to specify get method on what will happen if we enter the callback route. 

```
app.get('/auth/google/secret',
  passport.authenticate('google', { failureRedirect: '/login' }),
  function(req, res) {
    // Successful authentication, redirect home.
    res.redirect('/secrets');
  });
```

As we could see, our get method direct us to the callback route. After re-authentication, if it is successfull, it will redirect us to the `secrets` route and if  failed, will be directed to the `login`  route. 

```
app.get("/secrets", function(req, res){
    if(req.isAuthenticated()){
        res.render("secrets")
    }
    else{
        setHome = false;
        res.redirect("/")
    }
})
```

If it is authenticated, then we will render the html page of secrets. 



