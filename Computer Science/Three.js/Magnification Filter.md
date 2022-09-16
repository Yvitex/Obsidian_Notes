# Magnification Filter
Zooming into a certain texture may increase its blurriness because of [[Mipmapping]]. 
![[Pasted image 20220816092549.png]]

This is magnification filter, where the texture is too small for the surface it covers/
We could change it using the following
```js
colorTexture.magFilter = THREE.NearestFilter
```
![[Pasted image 20220816092700.png]]

Now it is more sharp than the former.
![[Pasted image 20220816092854.png]]

As we could see, if the texture is too small, it will be streched. ![[Pasted image 20220816094419.png]]

Other algorithm;
- NearestFilter
- LinearFilter (default)

```ad-Attention
title: NearestFilter best girl
collapse: open
Nearest Filter has better performance and higher framerate

```

When using nearest filter, we don't need mipmap so we could disable it
```js
colorTexture.generateMipmaps = false;
```