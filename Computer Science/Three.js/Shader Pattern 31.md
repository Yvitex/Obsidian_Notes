# Shader Pattern 31
![[Pasted image 20220905050158.png]]

Take the code form [[Shader Pattern 29]] the apply absolute and inverse
```glsl
void main()
{
 float strength = 1.0 - abs(cnoise(vUv * 10.0));
 gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

