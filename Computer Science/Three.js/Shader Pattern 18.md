
# Shader Pattern 18

![[Pasted image 20220902171035.png]]

What we could do is to create a y value from the [[Shader Pattern 17]] then combine the x and y using multiplixation
```glsl
varying vec2 vUv;
float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main()
{
    vec2 coorX = vec2(vUv.x * 0.1  + 0.45, vUv.y * 0.5 + 0.25);
    float dataX = 0.015 / distance(coorX, vec2(0.5, 0.5));
  
    vec2 coorY = vec2(vUv.x * 0.4  + 0.3, vUv.y * 0.1  + 0.45);
    float dataY = 0.015 / distance(coorY, vec2(0.5, 0.5));

    float strength = dataX * dataY;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

