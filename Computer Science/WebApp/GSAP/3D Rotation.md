# 3d Animation
We could do a 3d rotation by simply applying the [[GSAP Programming|tweening]] property of rotationY/X/Z
Remember the [[Euler's Angle]]? It works similar to the likes of it. ![[chrome-capture-2022-6-16 (1).gif]]
```js
gsap.to(".box", {rotateY: 360, repeat: -1, duration: 10, ease: "none"})
```

The problem is, it doesn;t look 3d enough. We need to apply a perspective value in the [[CSS]] class of the parent container, not the box itself ok?
```css
.perspective {
	perspective:400px;
}
```

![[chrome-capture-2022-6-16 (2).gif]]

The lower the value of perspective, the closer it is to the item. We could also use the [[GSAP Programming|gsap]]'s `trasnformPerspective` to do the job while preventing the html object to have a similar vanishing point
```js
gsap.set(".box", {transformPerspecive: 400})
```

Using [[Transform Origin Gsap]] and other 3d rotation, we may create some crazy effects