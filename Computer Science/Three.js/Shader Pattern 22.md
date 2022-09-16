---
aliases: [circular fragment shader]
---
# Shader Pattern 22
![[Pasted image 20220903042546.png]]

```glsl
varying vec2 vUv;
void main()
{
    float strength = step(0.01,abs(distance(vUv, vec2(0.5)) - 0.25));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Reverse it by substracting 1
![[Pasted image 20220903042720.png]]

```glsl
varying vec2 vUv;
void main()
{
    float strength = 1.0 - step(0.01,abs(distance(vUv, vec2(0.5)) - 0.25));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```



