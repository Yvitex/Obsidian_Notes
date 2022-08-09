# React Expression
From our previous lesson in [[React]]. We learned how JSX works, but did you know we could render a [[Javascript]] inside [[HTML]] inside [[Javascript]]?

![[anime-confused.gif]]

Say what again?

## Example
```js
import React from 'react';
import ReactDOM from 'react-dom';

let number = Math.round(Math.random() * 100)

ReactDOM.render(<h1>You will get married at age {number} Sir User</h1>, document.getElementById("root"))
```

![[Pasted image 20220624164209.png]]


I... uhh. Guess I'll die. ![[198167022000202.gif]]

## Using Link
One useful random pic generator is [Lorem Picsum](https://picsum.photos/), we could apply the link provided by them using a variable
```js
import React from 'react'
import ReactDOM from 'react-dom';

const image = "https://picsum.photos/200"

ReactDOM.render(<img src={image} alt="Random image"/>)
```

```ad-Attention
title: Expression is not Statement
collapse: open
See the difference [here](https://www.youtube.com/watch?v=WVyCrI1cHi8)

```

Basically, STatements do not return values, expression does. Statement control actions such as if statement, if-else statement, for loop etc.

```js
const a = if(x > 10){return 1}; //error
```

It does not make sense because we are assigning a variable a statement, not an expression. 

```ad-Attention
title: Objection your HONOR
collapse: open
Then why does ternary operator works?
For example: 
```js
const a = 10 > 1 ? 2 : 3; //prints 2
```

Well because, ternary operator is an expression. 
