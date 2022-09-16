# Shader Pattern 13
![[Pasted image 20220902161612.png]]

What we could do for this one is start off with a simple coordinate patterns of plane type
![[Pasted image 20220902161756.png]]

What we already know is that the length diagonally from 00 to 11 values could be used using the `length()`. 

```glsl
void main()
{
    float strength = length(vUv);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Or else, we could just add the x and y from the vUv
```glsl
void main()
{
    float strength = vUv.x + vUv.y;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

