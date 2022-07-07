# Orbit Controls
We could control the [[Three.js Camera|camera]] using this [[Builtin Controls]]. Though this control cannot go beyond 180 degrees vertically. 

First is we need to import it by finding it inside the node_modiles > three > examples > jsm > controls > OrbitControls.js

```js
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls'
```

Next, just above the boilerplate for [[Three.js Animations]]. We instantiate the control to a constant variable.
```js
const orbitControls = new OrbitControls()
```

We do not need to write THREE as it is not belong to the scope of universal THREE
```js
import * as THREE from 'three';
```

We will pass, inside the class `OrbitControls()` 2 parameters, first is the [[Three.js Camera|camera]] and the second is the [[HTML Canvas]] element. 

```js
const canvas = document.querySelector('.webgl');

const orbitControls = new OrbitControls(camera, canvas);
```

![[chrome-capture-2022-6-6.gif]]

Fur a much better effect or smoothness, we could enable the damping by saying
```js
const canvas = document.querySelector('.webgl');

const orbitControls = new OrbitControls(camera, canvas);
orbitControls.enableDamping = true;
```

But this might output a weird result. 
![[chrome-capture-2022-6-6 (1).gif]]

To prevent this, we must update the controls each frames inside the [[Three.js Animations]] boiler plate
```js
const canvas = document.querySelector('.webgl');

const orbitControls = new OrbitControls(camera, canvas);
orbitControls.enableDamping = true;

const tick = () => {
	orbitControls.update();
	renderer.render(camera, scene);
	window.requestAnimationFrame(tick);
}

tick();
```
![[chrome-capture-2022-6-6 (2).gif]]

You can drag it also horizontally or vertically and can even zoom. 
![[chrome-capture-2022-6-6 (3).gif]]

update() is also used when positioning the camera in the start such as
```js
const orbitControls = new OrbitControls(camera, canvas);
orbitControls.target.y = 2;
orbitControls.update();
```