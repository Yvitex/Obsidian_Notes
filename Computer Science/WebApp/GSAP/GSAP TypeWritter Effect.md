# Gsap Type Writer Effect
## Documentation
Here is the documentation about [TextPlugin](https://greensock.com/docs/v3/Plugins/TextPlugin?_rid=62344)

## Setup
First things first, we need to import the cdn to the codepen we want, the link url is 
```link
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/TextPlugin.min.js
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/gsap.min.js
```

It could be found [here](https://greensock.com/docs/v3/Installation?checked=core,text#codepen)

Register the plugin using
```js
gsap.registerPlugin(TextPlugin);
```

Next is to animate the text. If we have an [[HTML]] element p
```html
<p>Start Animation</p>
```

We could apply animation using
```js
gsap.registerPlugin(TextPlugin);
gsap.to("p", {text: "Hello World", duration: 3, ease: "linear", repeat: 1, yoyo: true});
```

This will animate the text typewriter style from old text to new text and reverse![[chrome-capture-2022-6-12.gif]]
