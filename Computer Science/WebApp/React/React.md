# React
It is a framework made by facebook, this module  allows us to write inside the [[HTML]] without directly accessing the [[HTML]]

Here we need 2 modules to be imported and they are `react` and `react-dom`

```js
const React = require('react');
const ReactDOM = require('react-dom')
```

```ad-Attention
collapse: open
title: BUTTT!!!
In react, we could use the latest version of [[JavaScript]] called ES6 (ES2015). 

```
Here is the latest syntax, wait, can we also apply this in an ordinary node.js?

```js
import React from 'react';
import ReactDOM from 'react-dom';
```

In our [[HTML]] file, we include some div element with the id of `root` , this will be our target element from where we will render it.  [[WebGL Renderer|render]] it like what we do in [[Three.js (core)]]. Also, we initialize our [[Javascript]] script inside that we will use with react after our div element. 

```html
<body>
	<div id="root"></div>
	<script src="../src/index.js" type="text/javascript"></script>
</body>
```

Next is to render some some html from js to the html file using `ReactDOM.render()`, first pareter is what we want to render and the second is our target. 

```js
ReactDOM.render(<h1>Hello World</h1>, document.getElementById("root"));
```

![[Pasted image 20220624154620.png]]

The problem is, we could only render one [[HTML]] element at a time, so to create multiple... We cover them with a div element
```js
ReactDOM.render(
  <div>
    <h1>Hello World</h1>
    <p>But why was I born?</p>
  </div>,
  document.getElementById("root"));
```

![[Pasted image 20220624154845.png]]

```ad-Notice
title: You mean WHAT??
collapse: open
[[HTML]] inside [[JavaScript]], what kind of witchery is this??

```

Well, JSX allows us to write HTML inside Javascript. Can't you believe it?? Well... It's at least less complicated than embedding syntax like [[Embedded Javascript Templating]] 

Along with [[Babel]] that allows future js language to become compatible with older browser. 
So if we say
```js
ReactDOM.render(
  <div>
    <h1>Hello World</h1>
    <p>But why was I born?</p>
  </div>,
  document.getElementById("root"));
```

Therefore, with the help of [[Babel]], this is what it converts into.

```js
"use strict";
ReactDOM.render( /*#__PURE__*/
React.createElement("div", null, /*#__PURE__*/
React.createElement("h1", null, "Hello World"), /*#__PURE__*/
React.createElement("p", null, "But why was I born?")),
document.getElementById("root"));
```


Whoo, Oneshot best game I wanna play. I don't wanna study anymore.

![[Pasted image 20220624164450.png]]