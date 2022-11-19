# Component Mount
Is called once when the page became live to the viewport. That is what mounting means, we called it once for ever start of the program, similar to [[useEffect]]

```jsx
componentDidMount(){

}
```

The most common use of this [[Lifecycle Methods]] is when we are fetching data from an [[API]]
To fetch data from them, in [[Javascript]] we use the `fetch` method
```jsx
componentDidMount(){
	fetch("https://jsonplaceholder.typicode.com/users")
}
```

This method is actually a promise, that when fulfilled, it will return an object. And we extract that object using a callback function after fetching it
```jsx
componentDidMount(){
	fetch("https://jsonplaceholder.typicode.com/users")
	.then((response) => {console.log(response.json)})
}
```

It might return 2 response
![[Pasted image 20220723172228.png]]

And that is because the app component is wrapped isnide the `React.StrictMode`. The most practical way of doing this is using 2 then methods
```jsx
  componentDidMount(){
    fetch("https://jsonplaceholder.typicode.com/users")
    .then((response) => response.json())
    .then((data) => console.log(data))
  }
```

This will reutrn an array of objects, not a promise
![[Pasted image 20220723172522.png]]

And opening it, we could see that each object have a property of name
![[Pasted image 20220723174115.png]]

So we could set it inside a `this.state`. Like what we have in [[Class Component Local State]]
```jsx
this.state = {
	monsters: []
}
```

Add those data to that state using `useState`
```jsx
  componentDidMount(){
    fetch("https://jsonplaceholder.typicode.com/users")
    .then((response) => response.json())
    .then((data) => {
	    this.setState(
		    () => {
			    return {monsters : data}
		    },
		    () => {
			    console.log(this.state)
		    }
		)
    })
  }

```


Then render it inside the return statement using [[Mapping in Class Component]]. To better understand when the render function [[Rerender Class Component]]s, search for the sequence of execution using it.
```jsx
  render() {
    return (
      <div className='App'>
	  { this.state.monsters.map((monster) => {
			return <h1>monster.name</h1>
		  })
	  }
      </div>
    );
  }
}
```

Don't forget the key
```jsx
  render() {
    return (
      <div className='App'>
	  { this.state.monsters.map((monster) => {
			return <h1 key={monster.id}>monster.name</h1>
		  })
	  }
      </div>
    );
  }
}
```

![[Pasted image 20220723175208.png]]
