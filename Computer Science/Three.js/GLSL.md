# GLSL
Means OpenGl Shading Language and it is a causin of C
It is also hardtyped language that needs to specify the datatype before using.
It does not have a console.logging method

It has the same datatype as in [[Java Variables]], it also support vector 2, 3 and 4
```GLSL
vec2 coor2 = vec2(1, 1); 
vec3 coor3 = vec3(1, 1, 1); 
vec4 coor4 = vec4(1, 1, 1, 1); 
```

This vec2, or 3 or 4 have a special functionality called `swizzle`
```glsl
vec4 coor4 = vec4(1, 1, 1, 1); 
vec2 coor2 = coor4.xy; // get the value of x and y
```

This is simply getting a value from a higher data type using a dot syntax sequence
The symbols available are as follow 
- x - r
- y - g
- z - b
- w - a

Creating a function here is as easy as follows
```glsl
float calcu() {
	return 0.1
}
```

We specify the type of return value like [[JAVA]]
