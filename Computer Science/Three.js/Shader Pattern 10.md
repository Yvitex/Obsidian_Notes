# Shader Pattern 10

![[Pasted image 20220902054153.png]]

This comes from the basic uvpattern
![[Pasted image 20220902050833.png]]

```glsl
varying vec2 vUv;
void main()
{
    float strength =  vUv.x;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

We could round it down so that when it is 0.35, it will become 0.4 which causes the similarity of colors
```glsl
varying vec2 vUv;
void main()
{
    float strength =  round(vUv.x);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902054425.png]]

It became halved as instead of round 0.35 as 0.4, it became 0, what we could do is to multiply it by the number of division and use the floor method instead
```glsl
varying vec2 vUv;
void main()
{
    float strength =  floor(vUv.x * 10.0);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902055142.png]]

It won't work because it is nor normalized. divide the rounded value by the same number of division
```glsl
varying vec2 vUv;
void main()
{
    float strength =  floor(vUv.x * 10.0) / 10.0;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220902055308.png]]

We could also do this
![[Pasted image 20220902055438.png]]

By multiplying it with the y version
```glsl
varying vec2 vUv;
void main()
{
    float strength =  floor(vUv.x * 10.0) / 10.0;
    strength *= floor(vUv.y * 10.0) / 10.0;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

