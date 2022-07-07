# React Local
Here are the steps to create a [[React]] app locally
- [ ] The recommended editor to use is [Visual Studio](https://visualstudio.microsoft.com/). Install it down. 

- [ ] Install [node](https://nodejs.org/en/) or update it

- [ ] Install some useful extension such as [babel javascript](https://marketplace.visualstudio.com/items?itemName=mgmcdermott.vscode-language-babel) or other suggested by [[Babel]] in their [documentation](https://babeljs.io/docs/en/editors), also install this [Doki theme](https://marketplace.visualstudio.com/items?itemName=unthrottled.doki-theme) because you are an anime addict who lives under your mom's basement. This [Vs Code icon](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons) is also useful.

- [ ] To start, create a react app as instructed in their [documentation](https://reactjs.org/docs/create-a-new-react-app.html)


## For Simple React App
```shell
$ npx create-react-app my-app
```

![[Pasted image 20220627131642.png]]

![[Pasted image 20220627131755.png]]

As suggested by the terminal we could start the development by typing command:
```shell
$ npm start
```

A webpage may load up, we could delete some unnecessary files as needed, and also, react already updated so there are some strange syntax everywhere. Instead of rendering this way like
```js
ReactDOM.render(<h1></h1>, document.getElementById("root"))
```

We use this;
first is we create a root object
```js
const root = ReactDOM.createRoot(document.getElementById("root"))
```

Then we use the attribute of root to render some  [[HTML]] element
```js
root.render(<h1>UWU</h1>)
```

![[Pasted image 20220627133233.png]]


May God forgive me for saying this word. 