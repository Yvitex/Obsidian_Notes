# Shader Pattern 19
![[Pasted image 20220903040721.png]]

First of is to create this funciton in the fragment shader
```glsl
vec2 rotate(vec2 uv, float rotation, vec2 mid) {
    return vec2(
        cos(rotation) * (uv.x - mid.x) + sin(rotation) * (uv.y - mid.y) + mid.x,
        cos(rotation) * (uv.y - mid.y) - sin(rotation) * (uv.x - mid.x) + mid.y
    );
}
```

Define a pi value
```glsl
#define PI 3.141592653589793238
```

Using the pattern from [[Shader Pattern 18]], rotate the UV coordinates
```glsl
varying vec2 vUv;
float random (vec2 st) {
    return fract(sin(dot(st.xy, vec2(12.9898,78.233))) * 43758.5453123);
}

vec2 rotate(vec2 uv, float rotation, vec2 mid) {
    return vec2(
        cos(rotation) * (uv.x - mid.x) + sin(rotation) * (uv.y - mid.y) + mid.x,
        cos(rotation) * (uv.y - mid.y) - sin(rotation) * (uv.x - mid.x) + mid.y
    );
}

void main()
{
	// Rotate Uv
    vec2 rotUv = rotate(vUv, PI * 0.25, vec2(0.5));
    
    vec2 coorX = vec2(rotUv.x * 0.1  + 0.45, rotUv.y * 0.5 + 0.25);
    float dataX = 0.015 / distance(coorX, vec2(0.5, 0.5));
    
    vec2 coorY = vec2(rotUv.x * 0.4  + 0.3, rotUv.y * 0.1  + 0.45);
    float dataY = 0.015 / distance(coorY, vec2(0.5, 0.5));

    float strength = dataX * dataY;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```


