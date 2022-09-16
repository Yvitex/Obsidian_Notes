# Cannon Js Integrated with 3js
A [[Three.js (core)]] physics library. See the [documentation](http://schteppe.github.io/cannon.js/docs/classes/AABB.html)

The first thing that we need is a three,js world, composed of [[Three.js Mesh|mesh]]es
![[Pasted image 20220824083754.png]]

The next thing is to create a physics world. Install the cannon liobrary
```shell
$ npm i cannon
```

Import the library to the source code
```js
import CANNON, { Vec3 } from "cannon"
```

Next are these steps:
- [[Physics World]]
- [[Physics Material]]
- [[Physics Force]]
- [[Multiple Physics Object]]
- [[Broadphase Optimization]]
- [[Physics Sounds]]
- [[Physics Constraint]]

```ad-Danger
title: This library hasn't beed updated for years
collapse: open
But lucky for us that we have community that is working for cannon-es

```

We could use this instead. 
```shell
$ npm i cannon-es
```

Then to import
```js
import * as CANNON from "cannon-es"
```

Here is the [documentation](https://github.com/pmndrs/cannon-es)







