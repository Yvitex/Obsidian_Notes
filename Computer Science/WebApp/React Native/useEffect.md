# useEffect
## Documentation
Here is the documentation regarding [useEffect](https://reactjs.org/docs/hooks-effect.html)

It is said that this method is like [[Lifecycle Methods ]]combined. It is used in any method that requires a side effect like data fetching, subscrition etc. 

Some useEffect method require clean ups using the `clearInterval` method if you are using the `setInterval` function because it exexcute everytime this variable of number change

This is similar to [[componentDidMount]] but for [[React Component|functional component]] only. In functional component, we could make our app more efficient by actually using this technique. As we know, [[React Functional Component]] executes the whole function everytime it triggers a render, but we could prevent a specific part of the code from being loaded using `useEffect`

```js
  useEffect(() => {
    const filteredMonster = monsters.filter((data) => {
      return data.name.toLowerCase().includes(findMonsters);
    })
    console.log("use effect")
    setFilteredMonster(filteredMonster);
  }, [findMonsters, monsters])
```

In this code, we will only trigger this function is findMonster or monsters change and not in other means thus preventing it from being loaded unnecessarily. Thus making it more efficient.