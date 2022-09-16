# Vercel
Is like [[Heroku Deployment]] but for Next.js, but not exactly. We could also deploy [[Three.js (core)]] application

## With Email
Fist thing first. Build app
```shell
$ npm run build
```

This will run the build
![[Pasted image 20220817162401.png]]

And create a dist file![[Pasted image 20220817162419.png]]

Log in to Vercel using email. Download the vercel module
```shell
$ npm i vercel
```

Now add this script to the packahe.json file
```js
"deploy": "vercel --prod"
```

![[Pasted image 20220817162647.png]]

Run it and select continue with emai;
```shell
$ npm run deploy
```

![[Pasted image 20220817162737.png]]

After setting the email. Override the output directory setting and change it to dist
![[Pasted image 20220817163522.png]]


Then it is done after that. Easier. 
