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

Here is a simple diagram to understand this
![[Pasted image 20221117080011.png]]

We have 3 phase in our [[React]] application.

Construcor triggers a render, and at the first load, [[componentDidMount]] will execute. [[React Properties]] and setState in [[React Class Component]] will trigger also re render and then call componentDidUpdate to execute. forceUpdate should not be used as possible except for third party libraries. 

`componentWillUnmount` is triggered when component exits the application, this is often used to clean [[Javascript|Js event listener]]

[[React Functional Component]] does not have these 3 [[Lifecycle Methods]] but hey, they still have the 3 phases. 

## Virtual DOM
How exactly do we update or rerender the webpage? Through the virtual DOM
![[Pasted image 20221117122317.png]]

We copy the real dom an dmake a virtual dom, Virtual Dom is a javascript copy of the real dom, then we copy this DOM to another in which we will make changes, we remove 3 component, this will reflext to the snapshot all the way to the real dom.

This is better than getting the html, then inject codes to it. I think?