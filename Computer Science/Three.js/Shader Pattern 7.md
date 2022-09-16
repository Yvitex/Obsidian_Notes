# Shader Pattern 7
![[Pasted image 20220902050627.png]]

What we could do is to start just by a simple plane with simple gradient
![[Pasted image 20220902050833.png]]
```glsl
varying vec2 vUv;

void main()
{
    float strength = vUv.x;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Off set ut bt half
```glsl
varying vec2 vUv;

void main()
{
    float strength = vUv.x - 0.5;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902051501.png]]

Only half of it is not visible because the rest is in negative value, what we could do is to make negative a  positive integer by transforming it using `abs` or absolute vlaue
```glsl

varying vec2 vUv;

void main()
{
    float strength = abs(vUv.x - 0.5);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902051622.png]]

