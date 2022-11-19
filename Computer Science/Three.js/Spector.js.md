---
aliases: []
---
# Spector.js
A tool for measuring the draw calls produced by a single frame. We could install it in this [page](https://chrome.google.com/webstore/detail/spectorjs/denbgaamihkadbghdceggmchnflmhpmk?hl=en) 

After installtion, reload the wepage and click the extension. We could click it again once it turns green and then record a scene

![[Pasted image 20220914031928.png]]


Next is to record a frame and see the info
![[Pasted image 20220914032016.png]]

We could see what the [[GPU]] draws inside here, one by one it is drawned and take note that such draw calls must be removed.

Our role is to lessen the command value![[Pasted image 20220914135836.png]]
And make it more efficient.
If this extension doesn't work, we could npm install the spector js module and call this code inside.
```js
const SPECTOR = require('Spector')
const spector = SPECTOR.Spector()
spector.displayUI()
```

---
###### Related: 
[[Three.js Performance Tips]]. [[Three.js Mesh]], [[GPU]]
###### Tags:
#extension 