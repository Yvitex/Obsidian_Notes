# Shader Pattern 4
![[Pasted image 20220902042742.png]]

What we could is just the same as the code from [[Shader Pattern 3]] but instead of adding the x and y together, we multiply them
```glsl
varying vec2 vUv;
void main()
{
    float strength = step(0.5, mod(vUv.y * 10.0, 1.0));
    strength *= step(0.5, mod(vUv.x * 10.0, 1.0));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902043116.png]]

This for instance is just a result of playing with the step value
```glsl
varying vec2 vUv;
void main()
{
    float strength = step(0.7, mod(vUv.y * 10.0, 1.0));
    strength *= step(0.4, mod(vUv.x * 10.0, 1.0));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Y have more step so it is cut later making it short, x has less step causing it to gave greater length.