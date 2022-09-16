# Shader Pattern 3

![[Pasted image 20220902042458.png]]

What we could do is to use the code from the precvious pattern at [[Shader Pattern 2]] then add it to the same pattern but using the x values
```glsl
varying vec2 vUv;
void main()
{
    float strength = step(0.5, mod(vUv.y * 10.0, 1.0));
    strength += step(0.5, mod(vUv.x * 10.0, 1.0));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

