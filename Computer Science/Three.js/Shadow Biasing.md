---
aliases: [shadow acne]
---
# Shadow Biasing
![[Pasted image 20220826104752.png]]

The hamburger export is heinous. It have some ripple effects that is namely called as shadow acne

Why does this occur?
When we are creating our [[Three,js Shadow]] using shadow mapping
![[Pasted image 20220826104917.png]]

We have this, some pixel that contains the [[Three.js Mesh|mesh]] will produce a shadow behind it but if the pixel is outside halfway between inside and outside the mesh, then it will produce a shadow in the surface creating this shadow acne

What we could do to solve this is to normalize it in the [[Three.js Light]] we have
```js
directionalLight.shadow.normalBias = 0.05;
```

![[Pasted image 20220826105230.png]]

Actually we have 2 solutions, we could either use:
- `directionalLight.shadow.normalBias`
- `directionalLight.shadow.bias`

Choose one and move on.


