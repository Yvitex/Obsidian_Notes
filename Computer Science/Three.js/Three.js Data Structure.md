# Data Structuring for Large Projects
We separate the files to different folders like this, we add Experience and Utils folder
![[Pasted image 20220826153525.png]]

The startup code is
```js
import Experience from "./Experience/Experience";
const experience = new Experience(document.querySelector(".webgl"))
```
Where we get the [[HTML Canvas]] element

Create these classes on separate folders:
- [[Experience Class]] - where we store the canvas and the main class that will combine all class
- [[Sizes Class]] - will handle the width and height, triggers an event at resize
- [[Time Class]] - will handle the calculation of [[Delta Time]]
- [[Event Trigger Class]] - a class that will be used to create custom triggers
- [[Camera Class]] - a class that will create the camera
- [[Renderer Class]] - a class that will render the scene
- [[World Class]] - a class that will create [[Three.js Mesh|mesh]] items
- [[Environment Class]] - will handle the [[Three.js Light]]
- [[Resource Class]] - will handle the [[Three.js Texture Loader]]
- [[Floor Class]] - will handle the creation of floor mesh
- [[Model or Fox Class]] - will handle the mesh of the model fox
- [[Debug Class]]  - Will handle the [[Debug GUI]]
- [[Destroy Method]] - a method that will destroy all meshes, events and textures etc.