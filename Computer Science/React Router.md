---
aliases: []
---
## Routes
THis is a module that allows us to have a routing mechanish to our [[React]] application. Depending on the url that go through, it will render certain components and save the other. 

The module we are using to do this is called [React Router](https://reactrouter.com/en/main)
To install this, follow the documentation and install for now, the V6
```shell
$npm i react-router-dom
```

```ad-Danger
title: React Libraries Upgrade Difficulties
collapse: open
React Libraries could break in upgrade, read the documentation on upgrade instruction because some libraries are not backward compatible

```

How do we use this? First of all, we need to enable the Browse Routing in the root component
Import the module and then surround the App component with the Browse Routing Component in the index js
```js
import { BrowserRouter } from 'react-router-dom';

root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

Create a path, a sibiling of component folder called `route`, inside we will create folders of a route. Example is home route and inside, like a component, we will create a route that s composed of component
![[Pasted image 20221118103207.png]]

```js
import CategoryContainer from "../../component/category-container/category-container.component";

const Home = () => {

  const categories = [
    {
      "id": 1,
      "title": "hats",
      "imageUrl": "https://i.ibb.co/cvpntL1/hats.png"
    },
    {
      "id": 2,
      "title": "jackets",
      "imageUrl": "https://i.ibb.co/px2tCc3/jackets.png"
    },
    {
      "id": 3,
      "title": "sneakers",
      "imageUrl": "https://i.ibb.co/0jqHpnp/sneakers.png"
    },
    {
      "id": 4,
      "title": "womens",
      "imageUrl": "https://i.ibb.co/GCCdy8t/womens.png"
    },
    {
      "id": 5,
      "title": "mens",
      "imageUrl": "https://i.ibb.co/R70vBrQ/men.png"
    }
  ]

  return (
    <CategoryContainer categories={categories} />
  )
}

export default Home;

```

We import it inside app js, this time, all component will be surrounded by routes from the react-router-dom
```js
import {Routes, Route} from 'react-router-dom';
const App = () => {
  return (
    <Routes>
      <Route path='/home' element={<Home />} />
    </Routes>
  )
}
```

Routes will specifiy that we want to use routing with these components, and Route will specify the specific component with path and what to render. 

BrowseRoute allows us to use this functionalities. Now, if we go to out `http://localhost:3000/home`, it is only then it will render the home page. 

## Outlet
There is also a trick for routing that requires nesting so that =other component will not dissapear when we go to other routes. 

We could do something like this
```js
const App = () => {

  const Shop = () => {
    return <h1>I am shop</h1>
  }

  return (
    <Routes>
      <Route path='/home' element={<Home />} />
      <Route path='/shop' element={<Shop />} />
    </Routes>
  )
}
```

OR nest it up like 
```js
return (
    <Routes>
      <Route path='/home' element={<Home />}> 
        <Route path='shop' element={<Shop />} />
      </Route>
      
    </Routes>
  )
```

Now we could go to route `http://localhost:3000/home/shop` but you may see that the h1 element does not appear, why? We havent specify there the component will go in the home component. In the home component, we will add an outlet like this
```js
import { Outlet } from "react-router-dom";

return (
    <div>
        <Outlet />
        <CategoryContainer categories={categories} />
    </div>
)
```

Now in this route `http://localhost:3000/home/shop`. 
![[Pasted image 20221118105114.png]]


Basically we could use this as a navigation bar like this
```js
const NavigationBar = () => {
    return (
      <div>
        <div>
          <h1>I am navigation</h1>
        </div>
        <Outlet />
      </div>
    )
  }

  const Shop = () => {
    return <h1>I am shop</h1>
  }

  return (
    <Routes>
      <Route path='/' element={<NavigationBar />}>
        <Route index element={<Home />} /> 
        <Route path='shop' element={<Shop />} />
      </Route>
    </Routes>
  )
```

You may notice this
```js
<Route index element={<Home />} /> 
```

index simply means that it will render in the parent path but not in its sibling or children. So our `/` route will render it but now in `/shop` 

More formally, we could do this.
```js
import { Outlet, Link } from "react-router-dom";
import { Fragment } from "react";

const NavigationBar = () => {
    return (
      <Fragment>
        <div className="navigation">
            <Link className="logo-container" to="/">
                <div>Logo</div>
            </Link>
            <div className="nav-links-container">
                <Link className="nav-link" to="/shop">
                    SHOP
                </Link>
            </div>
        </div>
        <Outlet />
      </Fragment>
    )
}
```

We have 2 additional components, `Fragment` is like a div container but it doesn;t register in the [[DOM]] so it is just a invisible container. `Link` is simply an anchor tag and functions like an anchor tag, it have to property that specify the link or destination. 


# Metatags
###### Related: 
###### Tags: #libraries 
###### Source: 

---