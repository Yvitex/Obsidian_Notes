# Minification Filter
![[Pasted image 20220816091903.png]]

THis box is blured because of a certain [[Mipmapping]] technique. If we go for far too far, it became more blurrier
![[Pasted image 20220816092138.png]]

This is what we call minification filter and we could modify this using different filter method.
This occurs when the texture is too big for the surface it covers.
We could change this into a different algorithm to make it more sharp and clear
```js
colorTexture.minFilter = THREE.NearestFilter
```

![[Pasted image 20220816092232.png]]

In a way, the burriness induced when far away is a good thins to prevent moire pattern
![[Pasted image 20220816093205.png]]

With nearest filter, it became like this mess
![[Pasted image 20220816093230.png]]


Here are other algorithm
- NearestFilter
- LinearFilter
- NearestMipmapLinearFilter
- NearestMipmapNearestFilter
- LinearMipmapLinearFilter
- LinearMipmapNearestfilter

```ad-Attention
title: NearestFilter best girl
collapse: open
Nearest Filter has better performance and higher framerate

```

When using nearest filter, we don't need mipmap so we could disable it
```js
colorTexture.generateMipmaps = false;
```