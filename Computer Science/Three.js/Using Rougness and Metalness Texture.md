# Roughness and Metalness
[[Roughness]] and [[Metalness]] textures can be set in [[Standard Material]] or any [[Physical Based Rendering]] material. 

```js
material.roughnessMap =  roughnessTexture;
material.metalnessMap = metalnessTexture;
```

This image has [[Ambient Occlusion]] and [[Normal Texture]], etc included
![[Pasted image 20220817061059.png]]

when using customized roughness and metalness texture, we must set the roighness and metalness value into its default which is 
- metalness = 0
- roughness = 1
- 
```js
material.roughness = 1;
material.metalness = 0;
```

