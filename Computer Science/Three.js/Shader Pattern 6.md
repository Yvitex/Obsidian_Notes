# Shader Pattern 6
![[Pasted image 20220902050057.png]]

What we could is just to offset slightly the code in [[Shader Pattern 5]]
```glsl
varying vec2 vUv;
void main()
{
    float shapeX = step(0.7, mod(vUv.y * 10.0, 1.0));
    
    // Offset the x coor
    shapeX *= step(0.3, mod(vUv.x * 10.0 - 0.2, 1.0

	// Offset the y coor	
    float shapeY = step(0.3, mod(vUv.y * 10.0 - 0.2, 1.0));
    shapeY *= step(0.7, mod(vUv.x * 10.0, 1.0));

    float strength = shapeY + shapeX;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```