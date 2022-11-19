---
aliases: []
---
The usual way to write this is through arrow functions
```js
const App = () => {
  return (
    <div className="App">
	    <h1 className="app-title">Monster Rolodex</h1>
    </div>
  )
}
```

One thing to note is that, in contrast to [[React Class Component]], this functional component do not have any [[Lifecycle Methods]] nor they mimic this methods. But this could be explained though [[Pure Functions]] and [[Impure Function]]

When you write funcitonal component, you are writing impure function emitting side effects

We mimic the [[React Class Component]] render ability using [[Hooks]] but instead of rendering only the return method, it will trigger to execute the whole function. In fact, the whole function will execute everytime you have new [[React Properties]] or you use [[Hooks]]

But take note, if you change your hook to a value similar tot he previous value, then it will not re render. For example
```js
const [findMonsters, setFindMonsters] = useState("a");

const getSearchedMonster = (event) => {
	setFindMonsters(event.target.value.toLowerCase())
}
```

If we press a, then it will not re-render, but if we press b, it will re render.

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---