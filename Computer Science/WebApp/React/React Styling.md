# CSS Styling
## In File
With [[CSS]] file, we could do it normally like how we do with [[HTML]]. But inside [[React]], we can't specify the class name normally, but we use the camel case form of the attribute.
```js
ReactDOM.render(<h1 className=".header">My Favorite Foods</h1>)
```

```css
.header{
  color: "red";
}
```

![[Pasted image 20220627043944.png]]

There are other attributes mutateed through the use of [[Javascript]]. Here are the list of [attributes](https://www.w3schools.com/tags/ref_standardattributes.asp) that we could use with jsx. For example is the attr, `contenteditable`, which causes an error inside our jsx but changing the casing may fix the problem
```js
ReactDOM.render(<div>
					<h1>My Favorite Foods</h1>
				</div>)
```

![[Pasted image 20220627044303.png]]
The content is now editable![[Pasted image 20220627044332.png]]

## In Line 
To style a jsx file inside [[Javascript]] itself, the format should be in a json meaning it must be enclosed with a curly brace. And because we are embedding a [[CSS]] inside an [[HTML]] inside a [[Javascript]] file, we need to declare it using another pair of {} curly brace. 
```js
ReactDOM.render(<h1 style={{color: "red", fontSyle: "italic"}}>Hello World</h1>)
```
Also, to declare multiple styling, we separate them using a comma and some attributes in kebab casing turns insto camel case. 

![[Pasted image 20220627050706.png]]

Alternatively, we could do a [[Expression vs Statement]] embdedding
```js
const style = {
	color: "red",
	fontSyle: "italic"
}

ReactDOM.render(<h1 style={style}>Hello World</h1>)
```

Here are some of the [[CSS]] [attributes](https://www.w3schools.com/cssref/) we could use. 

