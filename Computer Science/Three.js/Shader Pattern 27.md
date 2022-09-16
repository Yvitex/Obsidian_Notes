# Shader Pattern 27

![[Pasted image 20220903053124.png]]

We could take the code from [[Shader Pattern 26]], multiply it by 10 to icnrease its valeu from 0 to 1 to 0 to 10
```glsl
#define PI 3.141592653589793238
void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    angle /= PI * 2.0;
    angle += 0.5;
    angle *= 10.0;
    float strength = angle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220903053314.png]]

Get the modulo of 1
```glsl
#define PI 3.141592653589793238
void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    angle /= PI * 2.0;
    angle += 0.5;
    angle *= 10.0;
    angle = mod(angle, 1.0);
    float strength = angle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

We could make it look like this
![[Pasted image 20220903053550.png]]

Using some [[Trigonometric functions]] that

