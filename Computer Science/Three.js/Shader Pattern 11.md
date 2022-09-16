# Shader Pattern 11
![[Pasted image 20220902060320.png]]

Just copy paste a function from [BookofShader](https://thebookofshaders.com/10/). 
```glsl
float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}
```

Apply it to the uv
```glsl
varying vec2 vUv;

float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

void main()
{
    float strength =  random(vUv);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

