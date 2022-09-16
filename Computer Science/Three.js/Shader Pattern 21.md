# Shader Pattern 21
![[Pasted image 20220903042205.png]]

What we could do is just to take the code from [[Shader Pattern 14]] then transform it to have a range of -0.5 to + 0.5

```glsl
varying vec2 vUv;
void main()
{
    float strength = abs(distance(vUv, vec2(0.5)) - 0.25);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

