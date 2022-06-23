# EJS
## How to use with Express
First, import [[Express]] and create an app instance. Then set the view render to ejs using `.set()`
It is the same as setting a [[WebGL Renderer|render]]er with [[Three.js (core)|three.js]] 

```
app.set("view engine", 'ejs')
```

## How to render html
After setting view engine, then using the respond callback function, then we can say:
```
app.get('/', function(req, res){
    res.render('home')
});
```

All ejs files should be inside the *views* folder. Header and footer on the other hand could be inside the *partials* folder inside views folder. 