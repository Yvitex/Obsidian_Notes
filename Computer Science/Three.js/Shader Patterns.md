# Shader Patterns
Are [[Shader]] technique to create a certain drawing or [[WebGL Renderer|render]]. We could create patterns by messing with the [[UV Unwrapping|UV]]

Like what we are doing in the [[Fragment Shader GLSL]], because we can't access the uv from [[Shader Attributes]], then we will pass it as [[Shader Varying]]

```ad-Notice
title: ShaderMaterial()
collapse: open
Here we are using [[Create Shaders in Three.js|ShaderMaterial()]] which is just like rawshader material but with already written attributes and uniforms.

```
In the vertex glsl, we create the `vUv` variable of varying. And then pass the already written but hidden uv attributes. 
```glsl
varying vec2 vUv;
void main()

{
    gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
    vUv = uv;
}
```

We could have this kind of result
![[Pasted image 20220901171707.png]]

If the [[Fragment Shader GLSL]] is this
```glsl
varying vec2 vUv;
void main()
{
    gl_FragColor = vec4(1.0 , 1.0, 1.0, 1.0);
}
```

If we pass the y Uv values
```glsl
varying vec2 vUv;
void main()
{
    gl_FragColor = vec4(1.0 * vUv.y, 1.0 * vUv.y, 1.0, 1.0);
}
```

![[Pasted image 20220901171912.png]]

We;ll have this gradient effect from top to bottom. why? Uv values are like this
![[Pasted image 20220901172001.png]]

Uv are 2d coordinates with only have x and y, and like any [[Cartesian Coordinate System|cartesian]] plane, we have 0, 0 as the bottom left coordinate and 1 , 1 to the top right

- [[Shader Pattern 1]]
- [[Shader Pattern 2]]
- [[Shader Pattern 3]]
- [[Shader Pattern 4]]
- [[Shader Pattern 5]]
- [[Shader Pattern 6]]
- [[Shader Pattern 7]]
- [[Shader Pattern 8]]
- [[Shader Pattern 9]]
- [[Shader Pattern 10]]
- [[Shader Pattern 11]]
- [[Shader Pattern 12]]
- [[Shader Pattern 13]]
- [[Shader Pattern 14]]
- [[Shader Pattern 15]]
- [[Shader Pattern 16]]
- [[Shader Pattern 17]]
- [[Shader Pattern 18]]
- [[Shader Pattern 19]]
- [[Shader Pattern 20]]
- [[Shader Pattern 21]]
- [[Shader Pattern 22]]
- [[Shader Pattern 23]]
- [[Shader Pattern 24]]
- [[Shader Pattern 25]]
- [[Shader Pattern 26]]
- [[Shader Pattern 27]]
- [[Shader Pattern 28]]







