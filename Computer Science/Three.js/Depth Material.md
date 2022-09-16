# Depth Material
Produce a dark material that lightens if you go nearer, typically used in fogs or whotnot. 
To create this, just use the class `MeshDepthMaterial`

```js
const material = new THREE.MeshDepthMaterial();
```

![[chrome-capture-2022-7-16 (2).gif]]

Creating your own light does not work here, 