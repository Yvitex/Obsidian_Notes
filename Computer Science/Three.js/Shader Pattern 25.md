# Shader Pattern 25

![[Pasted image 20220903052359.png]]


Here, we knew that there is an angle coming from y to horitontal x. We could use `atan` for angles
of 2 coordinates.
```glsl
varying vec2 vUv;
uniform float trig;
void main()
{
    float angle = atan(vUv.x, vUv.y);
    float strength = angle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

We could also half it out
![[Pasted image 20220903052522.png]]
```glsl
varying vec2 vUv;
uniform float trig;
void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    float strength = angle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

