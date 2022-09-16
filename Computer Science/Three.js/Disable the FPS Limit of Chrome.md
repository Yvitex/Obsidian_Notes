---
aliases: []
---
# Disable the FPS Limit of Chrome
We do this to test the maximum performance of three.js. If your software is running only a 80 fps at maximum, then there is a problem

- [ ] First step is to close the chrome browser

- [ ] Now, Input this command 

```shell
$ start chrome --args --disable-gpu-vsync --disable-frame-rate-limit
```

- [ ] Open chrome

If we look at the fps rate using [[Stats.js]]
![[Pasted image 20220914024804.png]]

It could rise up to thousands

---
###### Related: 
[[Three.js Performance Tips]], [[Stats.js]]
###### Tags:
#terminal #three #javascript 