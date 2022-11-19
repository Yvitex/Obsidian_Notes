---
aliases: []
---
We could apply the use of metmask  transaction on our [[Smart Contract]]s in our websites or application. After all, blockchain is simply a server. 

So we have this frontend
```js
import React, {useEffect} from "react";
import { ethers } from "ethers";
import './App.css';

export default function App() {

  const wave = () => {
    
  }

  return (
    <div className="mainContainer">

      <div className="dataContainer">
        <div className="header">
        👋 Hey there!
        </div>

        <div className="bio">
        I am farza and I worked on self-driving cars so that's pretty cool right? Connect your Ethereum wallet and wave at me!
        </div>

        <button className="waveButton" onClick={wave}>
          Wave at Me
        </button>
      </div>
    </div>
  );
}

```

![[Pasted image 20221107105110.png]]

The next part, we will have a code like this
```javascript
import React, { useEffect, useState } from "react";
import "./App.css";

const getEthereumObject = () => window.ethereum;

/*
 * This function returns the first linked account found.
 * If there is no account linked, it will return null.
 */
const findMetaMaskAccount = async () => {
  try {
    const ethereum = getEthereumObject();

    /*
     * First make sure we have access to the Ethereum object.
     */
    if (!ethereum) {
      console.error("Make sure you have Metamask!");
      return null;
    }

    console.log("We have the Ethereum object", ethereum);
    const accounts = await ethereum.request({ method: "eth_accounts" });

    if (accounts.length !== 0) {
      const account = accounts[0];
      console.log("Found an authorized account:", account);
      return account;
    } else {
      console.error("No authorized account found");
      return null;
    }
  } catch (error) {
    console.error(error);
    return null;
  }
};

const App = () => {
  const [currentAccount, setCurrentAccount] = useState("");

  const connectWallet = async () => {
    try {
      const ethereum = getEthereumObject();
      if (!ethereum) {
        alert("Get MetaMask!");
        return;
      }

      const accounts = await ethereum.request({
        method: "eth_requestAccounts",
      });

      console.log("Connected", accounts[0]);
      setCurrentAccount(accounts[0]);
    } catch (error) {
      console.error(error);
    }
  };

  /*
   * This runs our function when the page loads.
   * More technically, when the App component "mounts".
   */
  useEffect(async () => {
    const account = await findMetaMaskAccount();
    if (account !== null) {
      setCurrentAccount(account);
    }
  }, []);

  return (
    <div className="mainContainer">
      <div className="dataContainer">
        <div className="header">
          👋 Hey there!
        </div>

        <div className="bio">
          I am Farza and I worked on self-driving cars so that's pretty cool
          right? Connect your Ethereum wallet and wave at me!
        </div>

        <button className="waveButton" onClick={null}>
          Wave at Me
        </button>

        {/*
         * If there is no currentAccount render this button
         */}
        {!currentAccount && (
          <button className="waveButton" onClick={connectWallet}>
            Connect Wallet
          </button>
        )}
      </div>
    </div>
  );
};

export default App;
```

Dissecting each parts...
To check if we have some sort of [[Ethereum]] wallet, we could call window properties of ethereum
```js
const getEthereumObject = () => window.ethereum;
```

And because, it is about fetching data and we are using [[React]], we are going to use the [[useEffect]] function to get this data. If the object is null, then we don't have any kind of wallet. 
```js
useEffect(() => {
	const ethereum = getEthereumObject();
	if(!ethereum){
		console.log("Install Metamask");
	}
	else{
		console.log("Have Metamask");
	}
}, [])
```

No, we don't want something like this because we might crash into some error, use try and catch block plus async and await for better [[API]] response
```js
useEffect(async () => {
	const ethereum = await findMetaMaskAccount();
	if(ethereum !== null){
		return;
	}
})
```

The findMetaMaskAccount should also detect if there is a log in account from metamask. Here is the function
```js
const findMetaMaskAccount = async () => {
  try {
    const ethereum = getEthereumObject();

    if (!ethereum) {
      console.error("Make sure you have Metamask!");
      return null;
    }

    console.log("We have the Ethereum object", ethereum);
    const accounts = await ethereum.request({ method: "eth_accounts" });

    if (accounts.length !== 0) {
      const account = accounts[0];
      console.log("Found an authorized account:", account);
      return account;
    } else {
      console.error("No authorized account found");
      return null;
    }
  } catch (error) {
    console.error(error);
    return null;
  }
};
```

we enclosed it in a try catch block. In any error, we return null.
```js
const findMetaMaskAccount = async () => {
	try{
	}
	catch(error){
		console.log(error);
		return null;
	}
}
```

Wait for the ethereum object to be returned from arrow function
```js
const ethereum = getEthereumObject();
```

Check if ethereum is null, if yes, then return immediately outputing no metamask
```js
if (!ethereum) {
      console.error("Make sure you have Metamask!");
      return null;
}
```

If there is ethereum object, continue. Request from etheerum object the `eth_accounts`
```js
console.log("We have the Ethereum object", ethereum);
const accounts = await ethereum.request({ method: "eth_accounts" });
```

If account is 0, it means there is no account. If it is not, get the first account and return it
```js
if (accounts.length !== 0) {
	const account = accounts[0];
	console.log("Found an authorized account:", account);
	return account;
	} else {
	console.error("No authorized account found");
	return null;
}
```

We are going to use [[Hooks]] to store the account because it could change. Set the initial to empty string.
```js
const [currentAccount, setCurrentAccount] = useState("");
```

Now, If the account in our `useEffect` [[Lifecycle Methods]] is not null, we set the currentAccount to that account
```js
useEffect(async () => {
	const account = await findMetaMaskAccount();
	if (account !== null) {
	  setCurrentAccount(account);
	}
}, []);
```

![[Pasted image 20221107112456.png]]

There was no authorized account because we are not yet logged in. We will create a button for this. 
```js
<button className="waveButton" onClick={null}>
    Connect to Metamask
</button>
```

Next is the function. The function:
```js
const connectToMetamask = async () => {
    try {
		const ethereum = getEthereumObject();
		if(!ethereum){
		  alert("Install Metamask");
		  return;
		}
	    const accounts = await ethereum.request({method: "eth_requestAccounts"});
	    console.log("Account Connected: " +  accounts[0]);
	    setCurrentAccount(accounts[0]);
    }
    catch (error){
      console.log(error);
      return;
    }
  }
```

Enclose it again with try and catch
```js
const connectToMetamask = async () => {
    try {
    }
    catch (error){
      console.log(error);
      return;
    }
  }
```

Get the object ethereum, if there is none, alert them to install a wallet then exit
```js
const ethereum = getEthereumObject();
if(!ethereum){
  alert("Install Metamask");
  return;
}
```

To actuall request for the wallet to signup an account, we request the ethereum object with method `eth_requestAccounts`
```js
const accounts = await ethereum.request({method: "eth_requestAccounts"});
```

Then set the current account in the [[Hooks]].
```js
setCurrentAccount(accounts[0]);
```

![[Pasted image 20221107120503.png]]


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---