---
aliases: []
---
# Network Throttling
We need to do this in every web development project that we have. We need to lower the [[Bandwidth]]  to see how the website react when there is a low network connection

![[Pasted image 20220915043237.png]]

We could do this network throttling using the chrome's > network > throttling feature. Add a new custom throttling with it
![[Pasted image 20220915043510.png]]

I added some 100 mbps data throttle. You could make it lower, like for instance, 1mbps per second.
Disable [[CPU Cache|cache]] so that the browser won't save your data and it will look like it is loaded for the first time. This is a good practice for development
![[Pasted image 20220915043818.png]]

I took roughly 5.5 seconds to load the site with 100 mbps throttle. This is so much slower when it is only 1mbps

# Metatags
---
###### Related: 
[[Network]], 
###### Tags:
#dev-tools 
