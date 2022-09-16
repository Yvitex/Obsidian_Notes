# GLTF
Means GL transmission format from the creators of things such as webgl etc. 
This supports [[Three.js Geometry|geometry]], [[Three.js Materials|material]], [[Three.js Camera|camera]], [[Three.js Scene|scene]], light, morphing, skeleton, animation, etc.

GLTF comes also in various formats 
- Default - glTF - have 3 files
- [[Binary]] - glTF-Binary - have 1 file, easier to load and light but unmodifiable
- [[Javascript Object]] Notation - glTF-Draco - have 4 files but lighter than default
- Embed Textures - have 1 file json but the [[Color Texture]] is included, heaviest

It is recommened to use default if you want items to modifiable or binary if not. We also must think about using Draco.

Here are some sample [models](https://github.com/KhronosGroup/glTF-Sample-Models/tree/master/2.0)
