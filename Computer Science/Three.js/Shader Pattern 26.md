# Shader Pattern 26
![[Pasted image 20220903052810.png]]


We could use the [[Shader Pattern 25]]

```glsl
#define PI 3.141592653589793238

void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    angle /= PI * 2.0;
    float strength = angle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220903052854.png]]

Dividing by PI will cause darkness. Offset it by half
```glsl
#define PI 3.141592653589793238

void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    angle /= PI * 2.0;
    angle += 0.5;
    float strength = angle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220903052951.png]]

