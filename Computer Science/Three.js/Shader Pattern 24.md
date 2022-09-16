# Shader Pattern 24
![[Pasted image 20220903045731.png]]

We could use teh code from [[Shader Pattern 23]] and then apply another sin function now to the x
```glsl
varying vec2 vUv;

void main()
{
    vec2 modUv = vec2(
        vUv.x + sin(vUv.y * 30.0) * 0.1,
        vUv.y + sin(vUv.x * 30.0) * 0.1
    );

    float strength = 1.0 - step(0.01,abs(distance(modUv, vec2(0.5)) - 0.25));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220903052119.png]]

This happens when we use a higher value inside sin
```glsl
varying vec2 vUv;

void main()
{
    vec2 modUv = vec2(
        vUv.x + sin(vUv.y * 100.0) * 0.1,
        vUv.y + sin(vUv.x * 100.0) * 0.1
    );

    float strength = 1.0 - step(0.01,abs(distance(modUv, vec2(0.5)) - 0.25));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

