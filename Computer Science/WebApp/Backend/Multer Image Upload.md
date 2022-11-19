---
aliases: [Multer]
---
# Multer
A library that could enable us to upload images from HTML Form. 

The first thing you need to do is to install multer
```shell
$ npm i multer
```

Import it
```js
const multer = require('multer');
```

Turn your HTML form into `enctype="multipart/form-data"` 
```html
<form action="/submitBook" class="form-container" method="post" enctype="multipart/form-data">
	<input name="photo" type="file" />
</form>
```

In our server we provide a `diskStorage` that will determine the destination of the uploaded file and the name of each file
```js
const storage = multer.diskStorage({})
```

This will have an object as a parameter, now we'll create the destination name
```js
const storage = multer.diskStorage({
	destination: function(request, file, callback){
		callback(null, './public/uploads/images')
	}
})
```

Next, we'll create the filname
```js
const storage = multer.diskStorage({
	destination: function(request, file, callback){
		callback(null, './public/uploads/images');
	},

	filename: function(request, file, callback){
		callback(null, Date.now() + file.originalname);
	}
})
```

Date.now() will generate a [[UNIX Time]] which is a unique calue concatenated by the original filename.
Now, we'll create an upload object
```js
const upload = multer({
	storage: storage
})
```

We could also specify the limit of the files
```js
const upload = multer({
	storage: storage,
	limits: {
		fileSize: 1024 * 1024 * 3
	}
})
```

The next thing we need to do is that in our [[HTTP Request Verbs|post request]], we would get the image by specifying the name of the input line
```js
app.post('/upload', upload.single('image'), function(req, res){
	
})
```

We could save the name of the uploaded file to [[Mongoose Create Operations|mongoose]] 

```js
app.post('/upload', upload.single('image'), function(req, res){
	let upload = new Upload({
		img: req.file.fileName
	})
})
```

# Metatags
###### Related: 
[[HTML]], [[Express]], [[Body Parser in Express]], [[Post in HTML Forms]], [[Restful Api Architecture Post]]
###### Tags:
#node
###### Source: 
[Documentation](https://www.npmjs.com/package/multer) [Youtube](https://www.youtube.com/watch?v=sUUgbcHm_3c&t=663s)

---