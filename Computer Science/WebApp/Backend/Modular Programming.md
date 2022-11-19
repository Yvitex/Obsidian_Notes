---
aliases: []
---
# Modular Programming
A type of programmign where we separate codes into modules. HowI like to do it is sometimes, in [[OOP]] but probably, when doing [[Databases]] and [[Passport]] and stuff, I'll use functional way where I export modules like this:

```js
function createLocalStrategy(model, passport){
    passport.serializeUser(model.serializeUser());
    passport.deserializeUser(model.deserializeUser());
}

module.exports = {
	createLocalStrategy
}
```


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---