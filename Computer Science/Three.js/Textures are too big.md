# textures
Have you ever experienced having too large [[Three.js Textures]] in your [[Three.js Mesh|mesh]]?
![[Pasted image 20220819104905.png]]

We could use [[Three.js Repeat Texture|texture.repeat()]] 
Just repeat the texture multiple times then use [[Three.js Repeat Texture|RepeatWrapping]]

```js
grassColor.repeat.set(8, 8)
grassAmbientOcclusion.repeat.set(8, 8)
grassNormal.repeat.set(8, 8)
grassRoughness.repeat.set(8, 8)

grassColor.wrapT = THREE.RepeatWrapping;
grassAmbientOcclusion.wrapT = THREE.RepeatWrapping;
grassNormal.wrapT = THREE.RepeatWrapping;
grassRoughness.wrapT = THREE.RepeatWrapping;

grassColor.wrapS = THREE.RepeatWrapping;
grassAmbientOcclusion.wrapS = THREE.RepeatWrapping;
grassNormal.wrapS = THREE.RepeatWrapping;
grassRoughness.wrapS = THREE.RepeatWrapping;
```

![[Pasted image 20220819105902.png]]

