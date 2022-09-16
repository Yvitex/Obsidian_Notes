---
aliases: [camera helper, light helper]
---
# Light Helpers
There are several kinds of helper for  each king of [[Three.js Light]]

- Hemisphere light
- Point Light
- Directional Light
- Rectangular Area Light
- Spot Light

We simply instantiate their own version of helper and pass the object light as its first paraeter then their size
```js
const pointLightHelper = new THREE.PointLightHelper(pointLight, 0.2);
scene.add(pointLightHelper);
```

That's all for any helper except [[Spot Light]]
To do this we do the following
```js
const spotLightHelper = new THREE.SpotLightHelper(flashLight, 0.2);
scene.add(spotLightHelper);
```

![[Pasted image 20220818113925.png]]

This is not allighed to the spot light, we need to update it in the next frame so we do this
```js
const spotLightHelper = new THREE.SpotLightHelper(flashLight, 0.2);
window.requestAnimationFrame(
	() => {
		spoitLightHelper.update()
	}
)
scene.add(spotLightHelper);
```

Rect area Light needs to be imported from the Example file

```js
import { RectAreaLightHelper }  from 'three/examples/jsm/helpers/RectAreaLightHelper.js'
```

Camera helper does not need size