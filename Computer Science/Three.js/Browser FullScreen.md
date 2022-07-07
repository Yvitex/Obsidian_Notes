# Browser Fullscreen
Following our example in the [[Fullscreen Mode]]. We could set the fullscreen mode by a double click
```js
window.addEventListener('dblclick', () => {
})
```

We could detect if the browser already have a full screen turned on by using `document.fullscreenElement`
```js
window.addEventListener('dblclick', () => {
	if(!document.fullscreenElement){
		
	}
	else{
	
	}
})
```

If there is no full screen element turned on, then we will make the [[HTML Canvas]] element go full screen
```js
window.addEventListener('dblclick', () => {
	if(!document.fullscreenElement){
		canvas.requestFullscreen();
	}
	else{
	
	}
})
```

If there is already a fullscreen element turned on, then we will exit using `document.exitFullscreen()`
```js
window.addEventListener('dblclick', () => {
	if(!document.fullscreenElement){
		canvas.requestFullscreen();
	}
	else{
		document.exitFullscreen();
	}
})
```

![[chrome-capture-2022-6-6 (6).gif]]


But this won;t work in lower version of browser like safari. In order to do that, we will use webkit. 
```js
window.addEventListener('dblclick', () => {

	const fullscreen = document.fullscreenElement || document.webkitFullscreenElement;
	
	if(!fullscreen){
		if(cavas.requestFullscreen){
			canvas.requestFullscreen();
		}
		else if(canvas.webkitRequestFullscreen){
			canvas.webkitRequestFullscreen();
		}
	}
	else{
		if(document.exitFullscreen){
			document.exitFullscreen();
		}
		else if(document.webkitExitFullscreen){
			document.webkitExitFullscreen();
		}
		
	}
})
```

