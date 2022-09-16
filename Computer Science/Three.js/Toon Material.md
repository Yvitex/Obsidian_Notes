# Toon Material
Is a Legend of Zelda breath of the wild like material, this produce a cartoonish effect
![[Pasted image 20220816165318.png]]

```js
const material = new THREE.MeshToonMaterial();
```

Using this gradient with [[Three.js Texture Loader]], note that this is actually a small pixel size and the image seems to be streched in the picture viewer appication. 
![[Pasted image 20220816165601.png]]

this is a very small picture. we could modify the texture
```js
material.gradientMap = gradientTexture;
```

The problem is we lost our catoonish effect
![[Pasted image 20220816165727.png]]

This is because of [[Mipmapping]]. We could prevent this using [[Magnification Filter]], and [[Minification Filter]] of NearestFilter

```js
gradientTexture.minFilter = THREE.NearestFilter;
gradientTexture.magFilter = THREE.NearestFilter;
gradientTexture.generateMipmaps = false;
material.gradientMap = gradientTexture;
```

![[Pasted image 20220816170036.png]]