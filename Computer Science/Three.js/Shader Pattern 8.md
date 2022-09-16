# Shader Pattern 8
![[Pasted image 20220902052005.png]]

Here, we might tought we could just append the [[Shader Pattern 7]] and the y version but if we do that, we get something like this

```glsl
varying vec2 vUv;
void main()
{
    float strength = abs(vUv.x - 0.5) + abs(vUv.y - 0.5);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902052144.png]]

What we could do is to use the `min` method or the mnimum value of the 2 values
```glsl
varying vec2 vUv;
void main()
{
    float strength = min(abs(vUv.x - 0.5), abs(vUv.y - 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}

```

