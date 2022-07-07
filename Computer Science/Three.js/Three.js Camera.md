---
aliases: [camera]
---
# Camera
This servers as the point of view in a [[WebGL Renderer|render]]

## Example Camera
In this example, we will use a Perspective Camera

`const camera = new THREE.PerspectiveCamera(fov, aspect ratio)`

We need to provide the arguments such as [[Field of View]] or fov and the [[Aspect Ratio]]

```
const sizes = {
	width: 800,
	height: 600
}

const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes/height)

scene.add(camera);

```

After that, we need to add the camera to the [[Three.js Scene|scene]]
`scene.add(camera)`

We can also modify the [[Transform Object|Object's Position]] by using position syntax to make adjustments

`camera.position.z = 3`

## Types
1. [[Perspective Camera]]
2. [[Orthographic Camera]]
3. Array Camera
4. Cube Camera
5. Stereo Camera


#three