# Animated Shadow Bake
Animated shadow bake is [[Shadow Baking]] but with moving the [[Three.js Mesh|mesh]] with shadow. 
Here, we are gioing to use an [[Alpha Texture]]
![[simpleShadow.jpg]]

Black won't be seen and white will the the shadow.
Create a plane [[Three.js Geometry|geometry]] with a red material 
```js
const shadowPlane = new THREE.Mesh(
    new THREE.PlaneBufferGeometry(1.5, 1.5),
    new THREE.MeshBasicMaterial({color: "#f00"})
)
```

![[Pasted image 20220819051751.png]]


The next thing to do is to rotate it and make it say down to the ground
```js
shadowPlane.rotation.x = -Math.PI * 0.5
shadowPlane.position.y = plane.position.y
```


![[Pasted image 20220819052445.png]]


Here we only copy the position of the giant plane below making it have a disease called zed fighting.

What we could do is to add the y position of the shadow just above slightly
```js
shadowPlane.rotation.x = -Math.PI * 0.5;
shadowPlane.position.y = plane.position.y + 0.0001;
```

![[Pasted image 20220819054506.png]]

Next is to apply the [[Alpha Texture]] using [[Three.js Texture Loader]] and convert it to black
```js
const textureLoader = new THREE.TextureLoader();
const alphaShadow = textureLoader.load("/textures/simpleShadow.jpg")

const shadowPlane = new THREE.Mesh(
    new THREE.PlaneBufferGeometry(1.5, 1.5),
    new THREE.MeshBasicMaterial({color: "#000", transparent: true, alphaMap: alphaShadow})
)
```

![[Pasted image 20220819054725.png]]

So when we animate it, we just copy the position of the ball is x and z axes and fade if it is far away from the ball.

Use [[Trigonometric functions]] to animate this into circular and bouncing motion. To make it move in a circular motion
Cos + sin = circle
```js
sphere.position.x = Math.sin(elapsedTime) * 2;
sphere.position.z = Math.cos(elapsedTime) * 2;
```

![[Pasted image 20220819060125.png]]

The absolute value of sin or cosine is a bouncing material
```js
sphere.position.x = Math.sin(elapsedTime) * 2;
sphere.position.z = Math.cos(elapsedTime) * 2;
sphere.position.y = Math.abs(Math.sin(elapsedTime * 4))
```

![[Pasted image 20220819060224.png]]


Now copy the position of y and x
```js
shadowPlane.position.x = sphere.position.x;
shadowPlane.position.z = sphere.position.z;
```

![[Pasted image 20220819060305.png]]

Then access the `material.opacity` of the  shadow plane and copy the value of y poition substracted by 1. decrease the value by half if needed
```js
shadowPlane.material.opacity = (1 - sphere.position.y) * 0.5
```

![[chrome-capture-2022-7-19.gif]]

