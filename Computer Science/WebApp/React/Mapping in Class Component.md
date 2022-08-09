# Mapping
[[Mapping Data]] in a [[React Class Component]] is very simple. For an instance, look at this example
```jsx
import './App.css';
import {Component} from "react"

class App extends Component {
  constructor() {
    super();

    this.state = {
      monster1: {
	      name: "Roberto"
      },
      monster2: {
	      name: "Miguel"
      },
      monster3: {
	      name: "Antonio"
      },
	  monster4: {
		  name: "Ricardo"
	  }
    }
  }

  render() {
    return (
      <div className='App'>
        
      </div>
    );
  }
}
```

We cannot simply [[Javascript Scpecial Operations|map]] this data as this function will only work for arrays. So we need to transform this datastructure to an array
```jsx
class App extends Component {
  constructor() {
    super();

    this.state = {
	    monsters: [
        {
          name: "Roberto"
        }, {
          name: "Miguel"
        }, {
          name: "Antonio"
        }, {
          name : "Ricardo"
        }
      ]
    }
  }

  render() {
    return (
      <div className='App'>
        
      </div>
    );
  }
}
```

The only thing left to do is to map the data. 
```jsx
class App extends Component {
  constructor() {
    super();

    this.state = {
	    monsters: [
        {
          name: "Roberto"
        }, {
          name: "Miguel"
        }, {
          name: "Antonio"
        }, {
          name : "Ricardo"
        }
      ]
    }
  }

  render() {
    return (
      <div className='App'> {
	      this.state.monsters.map((monster) => {
	        return <h1>monster.name</h1> }
	        )}
      </div>
    );
  }
}
```

 ![[Pasted image 20220723152155.png]]

Also, don't forget the keys
```jsx
class App extends Component {
  constructor() {
    super();

    this.state = {
	    monsters: [
        {
          name: "Roberto",
          id: "skdja2"
        }, {
          name: "Miguel",
          id: "deka;"
        }, {
          name: "Antonio",
          id: "sd3e2es"
        }, {
          name : "Ricardo",
          id: "sadj3ej20"
        }
      ]
    }
  }

  render() {
    return (
      <div className='App'> {
	      this.state.monsters.map((monster) => {
	        return <h1 key={monster.id}>monster.name</h1> }
	        )}
      </div>
    );
  }
}
```

This will help us to keep trach of each element in the iteration.