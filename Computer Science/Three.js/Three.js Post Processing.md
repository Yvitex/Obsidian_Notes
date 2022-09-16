---
aliases: [render target]
---
# Three.js Post Processing
How this will work is that we first capture the [[Three.js Mesh|mesh]] to be rendered
![[Pasted image 20220912034432.png]]

Next is we put it inside what we call a Render Target
![[Pasted image 20220912034501.png]]

This render target will ready a [[Three.js Textures]] for later use, we could set that texture as a [[Shader]] to a plane then capture it with a [[Three.js Camera|camera]] in which we could apply some effects
![[Pasted image 20220912034656.png]]

Then we could render it to the [[HTML Canvas]]
![[Pasted image 20220912034800.png]]

If we need multiple effects. we need to create 2 render target
![[Pasted image 20220912034856.png]]

Effects are also called passes. Each passes we made, we need to add it to a render target, but it doesn't mean that if we want to apply 10 passes, we will need 10 render targets, we only need 2 and then we switch between these 2 per effect. We do it because we can't write over a render target while reading it.

![[Pasted image 20220912045604.png]]

To implement this in [[Three.js (core)]], we need to use the class called [[Three.js EffectComposer]]

