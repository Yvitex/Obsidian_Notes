
# Shader Pattern 30
![[Pasted image 20220905045858.png]]


We use the code from the [[Shader Pattern 29]] then apply a step
```glsl
void main()
{
 float strength = step(0.1, cnoise(vUv * 10.0));
 gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

