# Firebase Authentication

![[Pasted image 20221118152729.png]]

The flow of authentication is we will send the user email to google, the google will responf with authentication token, the authentication token will then be sent to the firebase and firebase will send this token to google, google will return that this is a valid token by sending a verification token, then firebase will send an access token to the application. The application will return the access token everytime we want to make a CRUD request

## Creating Authentication

After you created a project, then we will press the web icon in the home base and we will see this
![[Pasted image 20221118160416.png]]

![[Pasted image 20221118160403.png]]

Register app and wait. We could see then this basecodes for us
![[Pasted image 20221118160512.png]]

What we are going to do is to copy this code to a utility file called `firebase.utils.js` located inside the utility folder and firebase folder

We will import then 3 methods for the rest, and they are `getAuth`, `signInWithPopup`, `signInWithRedirect`
```js
import { getAuth, GoogleAuthProvider, signInWithPopup, signInWithRedirect } from "firebase/auth"
```

We initialize our provider, for now, we use google provider
```js
const provider = new GoogleAuthProvider();
```

We set the provider to have a parameter in which we could choose which account should we use
```js
provider.setCustomParameters({
	prompt: "select_account"
});
```

We want to export the authentication
```js
export const auth = getAuth();
```

As well as the function to be executed when we want to authenticate with google, we use the method called `signInWithPopup` to pop out their accounts. This will take the auth and provider
```js
export const signInWithGoogle = () => signInWithPopup(auth, provider);
```

In the firebase console. go to authentication under build
![[Pasted image 20221118161926.png]]

Then enable the google auth

![[Pasted image 20221118161948.png]]

In the interface, we create a button and an [[Async and Await|async]] function that will do the fetching of google auth
```js
const googleSignIn = async() => {
	const response = await signInWithGoogle();
	console.log(response);
}
return (
	<button onClick={googleSignIn}>Sign In With Google</button>
)
```

It will respond along with the access token that we need
![[Pasted image 20221118162352.png]]

