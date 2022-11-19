# Passports
Sadly, *passports* are very confusing indeed. Passports are used to authenticate a user along with [[Cookies]] to remember the user until they log out. 


## Initial Setup
Here, we need 3 modules
```
npm install passport passport-local passport-local-mongoose express-session passport-local
```

<hr>
- passport - for authentication
- passport-local-mongoose - integrate [[Mongoose Create Operations|mongoose]] module with passport
- express-session - create and control [[Cookies]]
- passport-local - also for authentication but specifically for username and password stored in [[Databases|database]]

<hr>

After this installations. We now should verufy its existence inside **package.json**. We now import this module to our source code as in

```js
const passport = require("passport");
const passportLocalMongoose = require("passport-local-mongoose");
const session = require("session"); 
const LocalStrategy = require("passport-local").Strategy;
```

We do not need to import `passport-local` as it is already inside the `passport-local-mongoose`

Now, we need to initialize all modules to be used. First is the `session` using [[Express]] method `.use()`
```js
app.use(session({
	secret: "Hello World",
	resave: false,
	saveUninitialized: false,
}))
```

- `secret` : used to sign id session cookie, should be a compelx string to avoid hijack
- `resave`: forces the session to be saved back to the store, recommended vlaue is false
- `saveUninitialized`: forces uninitialized session to be saved, unintialized means created but not modified

(Note: This should be placed before the [[Mongoose Create Operations|mongoose]] connection to [[Databases|database]]
 Note2: secret string should be an [[Environmental Variables]])

Next is to initialize the `passport`
```js
app.use(passport.initialize());
app.use(passport.session());
```

- `initialize()` : will initialize the passport
- `session()` : will enable passport to use sessions

Also, this is placed before database connection. 

To use the `passportLocalMongoose`, we will integrate it with the passport using `plugin()` method. Just before creating a schema... integrate the plugin with the Schema

```js
mongoose.connect("mongodb:\\0.0.0.0:27017/userDB");
const UserSchema = mongoose.Schema({
	email: String, 
	password: String,
})

UserSchema.plugin(passportLocalMongoose);
```

After we create a model for our schema, then we will now enable the creation and destruction of cookies into the web app.

```js
const User = mongoose.model("User", UserSchema);

passport.use(new LocalStrategy(User.authenticate()));

passport.serializeUser(function(user, cb) {
    process.nextTick(function() {
      cb(null, { id: user.id, username: user.username, name: user.displayName });
    });
  });

  passport.deserializeUser(function(user, cb) {
    process.nextTick(function() {
      return cb(null, user);
    });
  });
```

Or, the easiest shortcut way is
```js
passport.use(new LocalStrategy(User.authenticate()));
passport.serializeUser(model.serializeUser());
passport.deserializeUser(model.deserializeUser());
```


## Registration
Inside the [[Restful Api Architecture Post|post]] method. The way to use this is by using `passport-local-mongoose` method called `.register()` along with the mongoose model. This will accept an object, in which `username` is mandatory, next is the password and lastly a callback function. If the registration undergo without any error, therefore we will authenticate the `passport` in type `"local"` from` passport-local `module then redirect them to the `/secret` route. 

```js
app.post("/register", function(req, res){
	User.register({username: req.body.username}, req.body.password, function(err, result){
		if(err){
			console.log(err);
			res.redirect("/register");
		}
		else{
			passport.authenticate("local")(req, res, function(){
				res.redirect("/secret");	
			})
		}
	});	
})
```

Here is how we create a `/secret` route. 
```
app.get("/secret", function(req, res){
	if(req.isAuthenticated()){
		res.render("secret")
	}
	else{
		res.redirect("/login")
	}
})
```

This will render the secret html if and only if, the user passport is authenticated and redirect to login route ,
With this, whenever we login, the website will remember us. After registration, we could go to /secret route directly and voila, we accessed it without redoing the registration.

## Login
```
app.post("/login", passport.authenticate("local",{
    successRedirect: "/",
    failureRedirect: "/landing"
}), function(req, res){
});
```

The old way does not work so here is the update one. 

## Logout
```
app.get("logout", function(req, res){
	req.logout(function(err){
		if(err){
			console.log(err);
		}
	});
	res.redirect("/");
})
```

We onlt need to use `logout` method to do the thing, this will delete the cookies fromm the browser. 