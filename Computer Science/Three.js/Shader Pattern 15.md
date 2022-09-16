# Shader Pattern 15
![[Pasted image 20220902164642.png]]

We could just simply take the code from [[Shader Pattern 14]] then minus it by 1.0
```glsl
```glsl
varying vec2 vUv;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}


void main()
{
	// Reverse it
    float strength = 1.0 - distance(vUv, vec2(0.5, 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

