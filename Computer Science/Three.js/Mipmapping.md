# Mipmapping 
Is an act of producing smaller version of a texture repeatedly until it gets one by one resolusion. This cause the blurriness of a certain [[Three.js Textures]] and prevent some Moire patterns

![[Pasted image 20220816091516.png]]

![[Pasted image 20220816091544.png]]

As we could see on the above picture, the nearest part is clearer than the farther side. It is because, the farther side is using smaller pixel ratio

![[Pasted image 20220816091637.png]]


We have some different types of Mipmapping Filters to modify this effect such as
- [[Magnification Filter]]
- [[Minification Filter]]


We could disable it when using NearestFilter in [[Magnification Filter]] and [[Minification Filter]]
