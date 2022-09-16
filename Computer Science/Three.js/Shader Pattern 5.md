
# Shader Pattern 5
![[Pasted image 20220902045529.png]]


What we could do is to separate the x and y drawing then later append it as individual drawings
```glsl
varying vec2 vUv;
void main()
{
	// Draw X
    float shapeX = step(0.7, mod(vUv.y * 10.0, 1.0));
    shapeX *= step(0.3, mod(vUv.x * 10.0, 1.0));

	// Draw Y
    float shapeY = step(0.3, mod(vUv.y * 10.0, 1.0));
    shapeY *= step(0.7, mod(vUv.x * 10.0, 1.0));

	// Combine
    float strength = shapeY + shapeX;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```