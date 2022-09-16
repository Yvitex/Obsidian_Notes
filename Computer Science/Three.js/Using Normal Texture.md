# Normal Texture
This section will discuss how to use [[Normal Texture]]
![[Pasted image 20220811133547.png]]

This will add intricate detail to the object. 
![[Pasted image 20220817060112.png]]

This looks flat, but with normal texture
```js
material.normalMap = normalTexture;
```
![[Pasted image 20220817060648.png]]

We could change the instensity using `normalScale.set()`
```js
material.normalScale.set(0.5, 0.5)
```

![[Pasted image 20220817060814.png]]