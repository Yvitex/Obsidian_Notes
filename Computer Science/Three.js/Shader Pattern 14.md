# Shader Pattern 14

![[Pasted image 20220902162148.png]]

We could simply use the [[Shader Pattern 13]] minus 0.5 to center it
```glsl
varying vec2 vUv;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main()
{
    float strength = length(vUv - 0.5);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

or else

```glsl
varying vec2 vUv;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}


void main()
{
    float strength = distance(vUv, vec2(0.5, 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

The later method have more control in which we could position the dark circle into any location. 

