# Shader Pattern 16
![[Pasted image 20220902164901.png]]

What we could do is to use the [[Shader Pattern 14]] and divide it by a very small number
```glsl
varying vec2 vUv;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}


void main()
{
	// Reverse it
    float strength =  0.012 / distance(vUv, vec2(0.5, 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}

```

