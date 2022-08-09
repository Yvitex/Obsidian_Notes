# Rerendering
```jsx
import { Component } from "react"

class App extends Component{
	constructor(){
		super();

		console.log(1);
	}

	componentDidMount(){
		console.log(3);
	}

	render(){
		console.log(2);
		return <div />
	}
}
```

The execution of methods inside a [[React Class Component]] happens from the [[Javascript Constructor]] -> Render Method -> [[Lifecycle Methods]]
![[Pasted image 20220724040110.png]]

Never mind the duplicates as a result of `React.StrictMode`, But notice that after the [[Lifecycle Methods]], the render method executes again. Why? Because we call `setState` inside it and `setState` updates the `state` variables that cause the [[React]] application to rerender

Also, [[React]] rerenders when [[React Properties]] are updated
For example, 
```jsx
return (
   <div className="App">
     <input
       className="search-box"
       type="search"
       placeholder="Search Monster"
       onChange={onSearch}
     />

     <CardList list={filtered} />  
    </div>
```

Filtered is an array component that implements a [[Javascript Scpecial Operations|filter]] method onChange, meaning it is a variable that changes content when we some changes happen, like when we tap in the keyboard. 

When we pass it to a new [[React Class Component]] and [[Javascript Scpecial Operations|map]] the arrays. We could simple extract it and assign some keys, it will automatically rerender when the `this.list.props` is changed. 
```jsx
render(){
   const { list } = this.props;
   return (
       <div>
          {list.map((data) => {
           return <h1 key={data.id}>{data.name}</h1>
          })}
       </div>
}
```




So there are 2 factors that determine the rerendering function, first is the `setState` metod and next is the updating  `props` 