# Tone Mapping
Is how we compress the value of pixel colors that extends greater than 1, for example in an image of a bright light sun. We compress the values using tone mapping
![[Pasted image 20220826092046.png]]

We could have different types of tone mapping but use one however you like, in this example, it will be in a fomat using a [[Debug GUI]]
```js
gui.add(renderer, "toneMapping", {
	None: THREE.NoToneMapping,
	Linear: THREE.LinearToneMapping,
	Reinhard: THREE.ReinhardToneMapping,
	Cineon: THREE.CineonToneMapping,
	ACESFilmic: THREE.ACESFilmicToneMapping,
})
```

We have differnt kinds of tone mapping such as
- `None (default)`
- `Linear`
- `Reinhard`
- `Cineon`
- `ACESFilmic`

The problem in our current implementation is that, it just update the background but not the mesh itself. What we could do is to add an `onChangeFinish()` to make it work

Inside our function about traversing child in the scene and applying the envmap in it in the [[Environment Map Realistic Render]] section. 
```js
const envMapChild = () => {
  scene.traverse((child) => {
    if (
      child instanceof THREE.Mesh &&
      child.material instanceof THREE.MeshStandardMaterial
    ) {
      child.material.envMapIntensity = parameters.envIntensity;
      
      // Enable Update
      child.material.needsUpdate = true
    }
  });
};
```

Then what we could do in the gui is that we call the update after changing the values
```js
gui.add(renderer, "toneMapping", {
	None: THREE.NoToneMapping,
	Linear: THREE.LinearToneMapping,
	Reinhard: THREE.ReinhardToneMapping,
	Cineon: THREE.CineonToneMapping,
	ACESFilmic: THREE.ACESFilmicToneMapping,
})
.onFinishChange(() => {
	envMapChild()
})
```

We could also increase the exposure of tone mapping like this
```js
renderer.toneMappingExposure = 3 
```

![[chrome-capture-2022-7-26.gif]]

