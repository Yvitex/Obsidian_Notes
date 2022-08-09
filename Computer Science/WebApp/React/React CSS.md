# React CSS
This is how we use [[CSS]] inside a [[react]] file. 
![[Pasted image 20220724165857.png]]

This might be your prefered architecture of files. And this is plausible, 
![[Pasted image 20220724165929.png]]

This is how App is structured with its [[CSS]]
Inside the components, we import the file location of the css
```js
import "./card-list.styles.css"
```

Then we could now use it inside the `className`. 
```jsx
class CardList extends Component{
    render(){
        const { list } = this.props;
        return (
            <div className="card-list">
               {list.map((data) => {
                return <h1 key={data.id}>{data.name}</h1>
               })}
            </div>
        );
    }
}
```

where card-list is a class inside css with this styling
```css
.card-list {
    width: 85vw;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;
  }
```

```ad-Danger
title: Styling Spread Anywhere!!
collapse: open
Despite habing multiple css for each component, once we import it in any component file jsx, it will import to all, the styling will be applied everywhere. We just Split it for easier navigation

```



