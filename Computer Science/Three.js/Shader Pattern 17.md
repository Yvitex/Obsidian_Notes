# Shader patter 17
![[Pasted image 20220902165453.png]]

To do this, we must modify the vUv first before doing what we did in the [[Shader Pattern 16]]
```glsl
varying vec2 vUv;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main()
{
    vec2 coor = vec2(vUv.x * 0.1  + 0.45, vUv.y * 0.5 + 0.25);
    float strength = 0.015 / distance(coor, vec2(0.5, 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

Strech using multiplication and offset using addition or substraction

