# Light
There are several kinds of kight in [[Three.js (core)]], each have different cose, use at your own discretion and risk

## Low cost
- [[Ambient Light]]
-  [[Hemisphere Light]]

## Medium Cost
- [[Directional Light]]
- [[Point Light]]

## High Cost
- [[Rectangular Area Light]]
- [[Spot Light]]

```ad-Danger
title: Using Light Extensively Is a Dumb Idea
collapse: open
Light is indeed very expensive to the [[GPU]] usage so we must be careful when using those as it may effect our performance

```

There are also [[Three.js Ligh tHelpers]] that will aid us in positioning these lights

It is to be noted to do this is just to [[Bake the Light]] in the [[Three.js Textures]] imported model instead. 
![[Pasted image 20220818112346.png]]

