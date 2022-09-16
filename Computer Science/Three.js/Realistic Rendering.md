# Realistic Rendering
[[WebGL Renderer|Render]]ing the object in [[Three.js (core)]] is not very realistc
![[Pasted image 20220826044438.png]]

We coudl do the following step by step:
- [[Physically Correct Lights]]
- [[Environment Map Realistic Render]]
- [[sRGB Encoding]]
- [[Tone Mapping]]
- [[AntiAliasing]]
- [[Shadow Biasing]]


Bonus. To add shadow, we'll use the the function envMap to enable cast shadow and receive the shadow
```js
const envMapChild = () => {
  scene.traverse((child) => {
    if (
      child instanceof THREE.Mesh &&
      child.material instanceof THREE.MeshStandardMaterial
    ) {

      child.material.envMapIntensity = parameters.envIntensity;
      child.material.needsUpdate = true
      child.castShadow = true
      child.receiveShadow = true
    }
  });
};
```

