# Shader Pattern 23
![[Pasted image 20220903043924.png]]


Take the code from [[Shader Pattern 22]], apply a [[Trigonometric functions]] in the y using the x value
```glsl
varying vec2 vUv;
void main()
{
    vec2 modUv = vec2(
        vUv.x,
        vUv.y + sin(vUv.x * 30.0) * 0.1
    );
  
    float strength = 1.0 - step(0.01,abs(distance(modUv, vec2(0.5)) - 0.25));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

