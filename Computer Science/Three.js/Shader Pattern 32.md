---
aliases: [mix(), clamp()]
---
# Shader Pattern 32
![[Pasted image 20220905052404.png]]

What we could do is to take the code from [[Shader Pattern 29]] then apply a [[Trigonometric functions]] for it
```glsl
void main()
{
 float strength = sin(cnoise(vUv * 10.0) * 20.0);
 gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Make it sharp using the step function
```glsl
void main()
{
 float strength = step(0.5, sin(cnoise(vUv * 10.0) * 20.0));
 gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220905053144.png]]

We could do this by mixing colors
```glsl
void main()
{
 float strength = step(0.5, sin(cnoise(vUv * 10.0) * 20.0));
 
 // Create the 2 colors 
 vec3 blackColor = vec3(0.0);
 vec3 uvColor = vec3(vUv, 1.0);
 gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Next is to create a mixed of color based on strength
```glsl
void main()
{
 float strength = step(0.5, sin(cnoise(vUv * 10.0) * 20.0));
 
 vec3 blackColor = vec3(0.0);
 vec3 uvColor = vec3(vUv, 1.0);

 // Mixed color
 vec3 mixedColor = mix(blackColor, uvColor, strength);
 gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

mix will return a vec3 which we could apply to `gl_FragColor`
```glsl
void main()
{
 float strength = step(0.5, sin(cnoise(vUv * 10.0) * 20.0));
 
 vec3 blackColor = vec3(0.0);
 vec3 uvColor = vec3(vUv, 1.0);

 // Mixed color
 vec3 mixedColor = mix(blackColor, uvColor, strength);
 gl_FragColor = vec4(mixedColor, 1.0);
}
```

To prevent interpolation of the colors, we must clamp the strength, so that it won't go beyong 1 or below 0
```glsl
void main()
{
 float strength = step(0.5, sin(cnoise(vUv * 10.0) * 20.0));
 // Clamp Color
 strength = clamp(strength, 0.0, 1.0);
 
 vec3 blackColor = vec3(0.0);
 vec3 uvColor = vec3(vUv, 1.0);

 vec3 mixedColor = mix(blackColor, uvColor, strength);
 gl_FragColor = vec4(mixedColor, 1.0);
}
```

