# Shader Pattern 1
![[Pasted image 20220902041627.png]]

We could do this effect using modulo operator
```glsl
varying vec2 vUv;

void main()
{
    float strength = mod(vUv.y * 10.0, 1.0);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

We can't use % but rather we use a method called `mod` that accepts 2 values. In our case we limit the value by 1 which means that it returns to 0 if it is divisible by one

