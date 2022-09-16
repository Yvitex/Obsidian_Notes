# Shader Pattern 9
![[Pasted image 20220902052545.png]]

At [[Shader Pattern 8]], we knew that it is the minimum value of the 2, but what if we want the maximum
```glsl
varying vec2 vUv;
void main()
{
    float strength = max(abs(vUv.x - 0.5), abs(vUv.y - 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

