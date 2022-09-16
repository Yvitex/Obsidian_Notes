# Fragment Shader
Fragment shaders are responsible for coloring and other stuff
Unlike [[Vertex Shader]], this don't have a [[Shader Attributes]] but instead we could pass:
- [[Shader Uniform]]
- [[Shader Varying]]

![[Pasted image 20220831050108.png]]

We could color the [[Fragments]] area using these type of data. And when we appy some [[Shader Varying]] codes, then we could have some interpolatng effects
![[Pasted image 20220831050450.png]]

This is executed after the [[Vertex Shader]]

Here is a sample code on how to use a [[Fragment Shader GLSL]]
