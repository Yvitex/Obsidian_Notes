# Galaxy Generator
Createe some basic parameters
```js
const parameters = {}
parameters.count = 100 // count of particle
parameters.size = 0.01 // size of particle
```

Create a function that will generate [[Three.js Particles]]
```js
const generateGalaxy = () => {
    console.time("generator")
    const coordinatesArray = new Float32Array(parameters.count * 3)
    const galaxyGeometry = new THREE.BufferGeometry()

    for (let i = 0; i < parameters.count; i++) {
        const i3 = i * 3;
        coordinatesArray[i3] = Math.random() // we are creating galazy so we need to be specific
        coordinatesArray[i3 + 1] = Math.random() // to each values in axes so we do this.
        coordinatesArray[i3 + 2] = Math.random()
    }
    
    galaxyGeometry.setAttribute(
        "position",
        new THREE.BufferAttribute(coordinatesArray, 3)
    )

    const galaxyMaterial = new THREE.PointsMaterial({
        size: parameters.size,
        sizeAttenuation: true,
        depthWrite: false,
        blending: THREE.AdditiveBlending
    })

    const galaxyMesh = new THREE.Points(galaxyGeometry, galaxyMaterial)
    scene.add(galaxyMesh)
    console.timeEnd("generator")
}
```

Next is to establish a [[Debug GUI]] to tweak our particles
```js
gui.add(parameters, "count").min(100).max(1000).step(10).onFinishChange(generateGalaxy)
gui.add(parameters, "size").min(0.01).max(0.2).step(0.01).onFinishChange(generateGalaxy)
```

![[Pasted image 20220822063135.png]]


But as what we could see, the old meshes dont delete, what we could do is to use the `dispose()` and `scene.remove()` method to delete this to the scene
Modify the function that will enable us to acces the mesh, geometry and material as a global variable. if the galaxy mesh is not null, dispose the material and geometry and remove the mes to the scene

```js

let coordinatesArray = null
let galaxyGeometry = null
let galaxyMaterial = null
let galaxyMesh = null

const generateGalaxy = () => {
    console.time("generator")

    if (galaxyMesh != null) { // detect of mesh is not null
        galaxyGeometry.dispose()
        galaxyMaterial.dispose()
        scene.remove(galaxyMesh)
    }

    const coordinatesArray = new Float32Array(parameters.count * 3)
    const galaxyGeometry = new THREE.BufferGeometry()

    for (let i = 0; i < parameters.count; i++) {
        const i3 = i * 3;
        coordinatesArray[i3] = Math.random() 
        coordinatesArray[i3 + 1] = Math.random() 
        coordinatesArray[i3 + 2] = Math.random()
    }
    
    galaxyGeometry.setAttribute(
        "position",
        new THREE.BufferAttribute(coordinatesArray, 3)
    )

    const galaxyMaterial = new THREE.PointsMaterial({
        size: parameters.size,
        sizeAttenuation: true,
        depthWrite: false,
        blending: THREE.AdditiveBlending
    })

    const galaxyMesh = new THREE.Points(galaxyGeometry, galaxyMaterial)
    scene.add(galaxyMesh)
    console.timeEnd("generator")
}
```

![[Pasted image 20220822083542.png]]

This is the look we are trying to recreate. 
The first thing we need to do is define the radius and the branch
```js
const parameters = {}
parameters.count = 100 // count of particle
parameters.size = 0.01 // size of particle
parameters.radius = 5
parameters.branches = 3
```

Inside the loop of the generator, we calculate the radius by multiplying a random number from 0 to 1 and the defined radius
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	coordinatesArray[i3] = radius
	coordinatesArray[i3 + 1] = Math.random()   
	coordinatesArray[i3 + 2] = Math.random()
	}
```

![[Pasted image 20220822091412.png]]

Next is to calculate and multipy thinssingle straigtline into multiple branches, we could do this by using the cos and sin [[Trigonometric functions]] combination to make a revolution using PI. But that is not enough, depending on the number of branches, we must comber them into nomalized repeating value and convert them into angle by multiplying it into 2 pi. 

For instance, if we have this count of poins \[1, 2, 3, 4, 5, 6, 7, 8, 9, 10], we shall convert it to \[0, 0.33, 0.66, 0, 0.33, 0.66, 0 ...] if the number of branch is 3 then multiply it by 2PI. We could do this using the modulo operator with the loop of counts. Modulo will not allow it to reach to 3 if the modulus is 3, 

```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2 // Convert to 0, 1, 2, 0, 1, 2, then normalize by dividing it to 3
	coordinatesArray[i3] = Math.random() 
	coordinatesArray[i3 + 1] = Math.random()   
	coordinatesArray[i3 + 2] = Math.random()
	}
```

Apply it through [[Trigonometric functions]] in the x and z axis
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2
	coordinatesArray[i3] = Math.sin(angleBranches) * radius 
	coordinatesArray[i3 + 1] = 0
	coordinatesArray[i3 + 2] = Math.cos(angleBranches) * radius 
	}

```

![[Pasted image 20220822092248.png]]

Add this to the gui.
The nexr step is to add an illusion of spin angle. To add this, we must notice that how we wil approach this is that when a point is near the origin, then it will have a slower rotation and the farther it is to the origin the faster it may go, or the higher the axis it must be, Therefore it is 
$$radius * spinAngle$$
Then add this to the the value that we use our [[Trigonometric functions]]
```js
const parameters = {}
parameters.count = 100 // count of particle
parameters.size = 0.01 // size of particle
parameters.radius = 5
parameters.branches = 3
parameters.spinAngle = 2
```

Inside the loop
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2

	const spinAngle = radius * parameters.spinAngle
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius 
	coordinatesArray[i3 + 1] =   0
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius 
	}
```
![[Pasted image 20220822101108.png]]


Next is to add randomness to the spin. We could simply do this by adding some random values
```js
const parameters = {}
parameters.count = 100 // count of particle
parameters.size = 0.01 // size of particle
parameters.radius = 5
parameters.branches = 3
parameters.spinAngle = 2
parameters.randomness = 0.01
```

Inside the loop
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2

	const spinAngle = radius * parameters.spinAngle

	const xRandomness = parameters.randomness * (Math.random() - 0.5)
	const yRandomness = parameters.randomness * (Math.random() - 0.5)
	const zRandomness = parameters.randomness * (Math.random() - 0.5)
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius + xRandomness
	coordinatesArray[i3 + 1] =  + yRandomness
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius + zRandomness
	}
```

![[Pasted image 20220822101440.png]]

What we want is that there are denser items in the center and less to the sides, in our case, the points appear constant wich makes it unrealistic, What we could do is to utilize the `Math.pow()` method. ![[Pasted image 20220822115557.png]]

What this will do is make our linear randomness to have a steepness.
If we use `Math.pow(0.2, 2) = 0.04`. But if we have `Math.pow(0.9, 2) = 0.81`. This difference makes the curvature. Set a parameter called randomnessPower
```js
const parameters = {}
parameters.count = 100 
parameters.size = 0.01 
parameters.radius = 5
parameters.branches = 3
parameters.spinAngle = 2
parameters.randomness = 0.01
parameters.randomnessPower = 1 //set to 1 as the initial power value
```

Inside the loop, we will add the randomness and not use the previous randomness parameter
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2

	const spinAngle = radius * parameters.spinAngle

	const xRandomness = Math.pow(Math.random(), parameters.randomnessPower) 
	const yRandomness = Math.pow(Math.random(), parameters.randomnessPower)  
	const zRandomness = Math.pow(Math.random(), parameters.randomnessPower) 
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius + xRandomness
	coordinatesArray[i3 + 1] = yRandomness
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius + zRandomness
	}
```

This will result for only the randomness tpo be in the positive side, we could multiply this to negative 1  randomly by using ternary expression
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius // spawn point in a straight line
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2

	const spinAngle = radius * parameters.spinAngle

	const xRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1) 
	const yRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)   
	const zRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)  
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius + xRandomness
	coordinatesArray[i3 + 1] = yRandomness
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius + zRandomness
	}
```

![[Pasted image 20220822120827.png]]

This is achieved by randomnessPower of 4. Now, to color it, we pass it to the parameter object to enable the tweaking
```js
const parameters = {}
parameters.count = 100 
parameters.size = 0.01 
parameters.radius = 5
parameters.branches = 3
parameters.spinAngle = 2
parameters.randomness = 0.01
parameters.innerColor = "#ff6030"
parameters.outerColor = "#1b3864"
```

Next is to pass it to the gui
```js
gui.addColor(parameters, "innerColor").onFinishChange(generateGalaxy)
gui.addColor(parameters, "outerColor").onFinishChange(generateGalaxy)
```

Inside the forloop, we create 2 instance of Three colors, 
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2
	const spinAngle = radius * parameters.spinAngle

	const innerColor = new THREE.Color(parameters.innerColor) // create instance of color
	const outerColor = new THREE.Color(parameters.outerColor)
	
	const xRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1) 
	const yRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)   
	const zRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)  
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius + xRandomness
	coordinatesArray[i3 + 1] = yRandomness
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius + zRandomness
	}
```

We could mix colors using [[Opening and Closing Door|lerp]] method in three,js. We can't do it to the original instance, instead we create a clone. Also, the second parameter will be the blending, which means we set it to the radius that is normalized so that the farther away it is from the origin, the more tint the outerColor is.
```js
for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2
	const spinAngle = radius * parameters.spinAngle

	const innerColor = new THREE.Color(parameters.innerColor) // create instance of color
	const outerColor = new THREE.Color(parameters.outerColor)
	const mixedColor = innerColor.lerp(outerColor, radius / parameters.radius)
	
	const xRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1) 
	const yRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)   
	const zRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)  
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius + xRandomness
	coordinatesArray[i3 + 1] = yRandomness
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius + zRandomness
	}
```

Set the color cy creating a new array and by modifying the attributes of the geometry
```js

const colorArray = new Float32Array(parameters.count * 3 )

for (let i = 0; i < parameters.count; i++) {
	const i3 = i * 3;
	const radius = Math.random() * parameters.radius
	const angleBranches = (i % paramaeters.branches) / paramaeters.branches * Math.PI * 2
	const spinAngle = radius * parameters.spinAngle

	const innerColor = new THREE.Color(parameters.innerColor) 
	const outerColor = new THREE.Color(parameters.outerColor)
	const mixedColor = innerColor.lerp(outerColor, radius / parameters.radius)
	
	const xRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1) 
	const yRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)   
	const zRandomness = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : -1)  
	
	coordinatesArray[i3] = Math.sin(angleBranches + spinAngle) * radius + xRandomness
	coordinatesArray[i3 + 1] = yRandomness
	coordinatesArray[i3 + 2] = Math.cos(angleBranches + spinAngle) * radius + zRandomness

	colorArray[i3] = mixedColor.r // set the color
	colorArray[i3 + 1] = mixedColor.g
	colorArray[i3 + 2] = mixedColor.b
	
	}
```

Then enable the vertexColor in the [[Points Material]]
```js
galaxyMaterial = new THREE.PointsMaterial({
	size: parameters.size,
	sizeAttenuation: true,
	depthWrite: false,
	blending: THREE.AdditiveBlending,
	vertexColors: true
})
```

