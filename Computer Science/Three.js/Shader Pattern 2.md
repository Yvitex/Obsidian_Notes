# Shader Pattern 2
![[Pasted image 20220902041911.png]]

We could do this by using the [[Shader Pattern 1]] code and making a step value. We could use an if else state for this one but it is not good when it comes to performance in [[Shader]]. Lucky for use that we have a built in method called `step` that will aid us here
```glsl
varying vec2 vUv;

void main()
{
    float strength = mod(vUv.y * 10.0, 1.0);
    strength = step(0.5, strength);
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

What this basically means is that when it is less than 0.5, then transform it into 0 and if it is greater than 0.5, turn it into 1. 

