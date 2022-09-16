# Sounds
Inserting sounds is just as easy.
First is we need to create a new Sound instance with arguments being the route
```js
const hitSounds = new Audio("/sounds/hit.mp3")
```

We could play it with `play()` method but we will use it isnide a function
```js
const playHit = () => {
	hitSounds.play()
}
```

In the physics object, we could listen to event listener such as collide
```js
object.addEventListener("collide", playHit)
```

This will sounds static and non continuous, we must set the sounds to the beginnning so that it won;t be cut
```js
const playHit = () => {
	hitSounds.currentTime = 0 // reset to 0
	hitSounds.play()
}
```

What we want is that it won;t play when the impact of the collision is weak, we could call on a parameter that will output it using `contact.getImpactVelocityAlongNormal()`
```js
const playHit = (collision) => {
	const impactValue = collision.contact.getImpactVelocityAlongNormal()
	if (impactValue > 1.7) {
		hitSounds.currentTime = 0 // reset to 0
		hitSounds.play()
	}
}
```

We could also make the sounds more random
```js
const playHit = (collision) => {
	const impactValue = collision.contact.getImpactVelocityAlongNormal()
	if (impactValue > 1.7) {
		hitSounds.volume = Math.random()
		hitSounds.currentTime = 0 // reset to 0
		hitSounds.play()
	}
}
```