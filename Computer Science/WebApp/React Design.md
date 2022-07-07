# React Designing
One of the most famous icon provider library in [[React]] is [mui-material-icon](https://mui.com/material-ui/icons/)
Read the documentation for usage. To use this we need toinstall the following libraries
```sh
$ npm install @mui/material @emotion/react @emotion/styled @mui/icons-material
```

Also the updated version of react.
We could use the icons by importing this code to the source code, simply just choose the appropriate icon in their [search website](https://mui.com/material-ui/material-icons/)
![[Pasted image 20220707161618.png]]

Just copy the code and import it. For example
```js
import AddIcon from '@mui/icons-material/Add';
```

Then we could use it inside the html as
```js
<AddIcon />
```

We could also use their styled buttons along with the icons. Just import this. Here's the [documentation](https://mui.com/material-ui/react-floating-action-button/)
```jsx
import Fab from '@mui/material/Fab';
```

To use this. simply replace aby buttom [[HTML]] element with this
```js
<Fab color="primary" onClick={submitNote}><AddIcon /></Fab>
```

It will retain any properties you created. `color` property is a builtin properties from Fab that will definite its color.

![[Pasted image 20220707162127.png]]

To add aditional effect, we could make a transition effect using Zoom element
```jsx
import Zoom from '@mui/material/Zoom';
```

We could enable this effect by nesting it with other component
```js
<Zoom in={true}>
	<Fab color="primary" onClick={submitNote}><AddIcon /></Fab>
</Zoom>
```

`in` is important as it will indicate weather the button will show or not, We could enable it or disable using conditional rendering. 


![[anime-you-made-it.gif]]

The End, to be continued