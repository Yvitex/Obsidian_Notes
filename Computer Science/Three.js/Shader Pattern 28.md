# Shader Pattern 28

![[Pasted image 20220903060527.png]]

We could combine the [[Shader Pattern 27]] and  [[Shader Pattern 22]]
USe 27 for the additional radius offset
```glsl
void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    angle /= PI * 2.0;
    angle *= 10.0;
    angle = sin(angle * 10.0);
}
```

Next os use the 22 t create a circle
```glsl
void main()
{
    float angle = atan(vUv.x - 0.5, vUv.y - 0.5);
    angle /= PI * 2.0;
    angle *= 10.0;
    angle = sin(angle * 10.0);
   
	// Use the angle as radius
    float radius = 0.2 + angle * 0.02;
    
    // Add radius to the circle
    float circle = 1.0 - step(0.01, abs(distance(vUv, vec2(0.5)) - radius));

    float strength = circle;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

