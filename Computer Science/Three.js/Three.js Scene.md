---
aliases: [scene]
---

# The Scene
This is the container of the things we will create such as the [[Three.js Objects]], [[Three.js Mesh|Mesh]], lights,  [[Three.js Camera|camera]], etc.


## Set up
To set up a Scene in three.js, we instantiate the Scene class
`const scene = new THREE.Scene()`

### Adding Objects
To add objects to the scene, we need to tell js to include that object `scene.add(camera)`

We include this scene object to the items that we will need to [[WebGL Renderer|render]]


#three