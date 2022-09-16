# Shader Pattern 12
![[Pasted image 20220902161228.png]]

We could use the code from [[Shader Pattern 11]]. But instead of directly using the uv coordinates, we will use a rounded value instead 
```glsl
varying vec2 vUv;
float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main()
{
	// Create a vec2 coordinates with rounded values
    vec2 coords = vec2(round(vUv.x * 10.0) / 10.0, round(vUv.y * 10.0) / 10.0);
    float strength =  random(coords);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```



