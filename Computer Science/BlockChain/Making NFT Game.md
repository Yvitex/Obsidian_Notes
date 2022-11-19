---
aliases: []
---
## Setup
[[Solidity Smart Contract Setup]] first. Then to create an nft characters, we must think of its attributes. We could set the attributes as a [[Solidity Struct]] then store it to an array as a defaultCharacter that can be chosen by the player. We set the data using the constructor
```solidity
contract MyEpicGame{

	// Stats
    struct CharacterAttributes {
        uint256 characterIndex;
        string name;
        string imageUrl;
        uint256 hp;
        uint256 maxHp;
        uint256 attackDamage;
    }
    
	// Character storafe
    CharacterAttributes[] defaultCharacters;
    
	// set the values and add to defaultCharacter array
    constructor(string[] memory name, string[] memory imageUrl, uint256[] memory hp, uint256[] memory attackDamage){
        for(uint256 index = 0; index < name.length; index++){
            defaultCharacters.push(CharacterAttributes(index, name[index], imageUrl[index], hp[index], hp[index], attackDamage[index]));
            CharacterAttributes memory c = defaultCharacters[index];
            console.log("Name: %s, imageUrl: %s, Attack: %s", c.name, c.imageUrl, c.attackDamage);
        }
    }
}
```

We could test run it in the run.js
```js
const run = async () => {
    const contractFactory = await hre.ethers.getContractFactory("MyEpicGame");
    const gameContract = await contractFactory.deploy(
        ["Sylvie", "David Martinez", "Lelouch vi Britannia"],
        ["https://i.pinimg.com/564x/4a/30/89/4a3089bfeb92de031f85086ca83039d1.jpg", 
        "https://i.pinimg.com/564x/17/ba/cb/17bacb6db11c92783d1e94ed19673f0e.jpg", 
        "https://i.pinimg.com/564x/06/f0/d1/06f0d15018e98597b12a988bec6eaadc.jpg"],
        [100, 200, 300],
        [300, 200, 100],
    );
    await gameContract.deployed();
    console.log("Contract Address: " + gameContract.address);
}

const runMain = async () => {
    try{
        await run();
        process.exit(0);
    }
    catch (error){
        console.log(error);
        process.exit(1);
    }
}
// https://i.pinimg.com/564x/91/f0/51/91f05141d336932ee506366ec9ea7b0c.jpg
runMain();
```


## NFT using OpenZeppelin
We will make this an actuall nft now using the imports we do with zeppelin at [[ERC-20 Token Creation]]
```shell
$ npm install @openzeppelin/contracts
```

The full code is as follow
```solidity
// SPDX-License-Identifier: Unlicense

pragma solidity 0.8.17;

import "hardhat/console.sol";
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

import "@openzeppelin/contracts/utils/Counters.sol";
import "@openzeppelin/contracts/utils/Strings.sol";

contract MyEpicGame is ERC721{

    struct CharacterAttributes {
        uint256 characterIndex;
        string name;
        string imageUrl;
        uint256 hp;
        uint256 maxHp;
        uint256 attackDamage;
    }

    using Counters for Counters.Counter;
    Counters.Counter private _tokenIds;

    CharacterAttributes[] defaultCharacters;
    mapping(uint256 => CharacterAttributes) public NFTHolderAttributes;
    mapping(address => uint256) public NFTHolders;

    constructor(string[] memory name, string[] memory imageUrl, uint256[] memory hp, uint256[] memory attackDamage)ERC721("Heroes", "HERO"){
        
        for(uint256 index = 0; index < name.length; index++){
            defaultCharacters.push(CharacterAttributes(index, name[index], imageUrl[index], hp[index], hp[index], attackDamage[index]));
            CharacterAttributes memory c = defaultCharacters[index];
            console.log("Name: %s, imageUrl: %s, Attack: %s", c.name, c.imageUrl, c.attackDamage);
        }

        _tokenIds.increment();
    }

    function mintCharacterNFT(uint256 _characterIndex) external {
        uint256 newItemId = _tokenIds.current();

        _safeMint(msg.sender, newItemId);
        // NFTHolderAttributes[newItemId] = defaultCharacters[_characterIndex];
        NFTHolderAttributes[newItemId] = CharacterAttributes({
            characterIndex: defaultCharacters[_characterIndex].characterIndex,
            name:defaultCharacters[_characterIndex].name,
            imageUrl:defaultCharacters[_characterIndex].imageUrl,
            hp:defaultCharacters[_characterIndex].hp,
            maxHp:defaultCharacters[_characterIndex].maxHp,
            attackDamage:defaultCharacters[_characterIndex].attackDamage
        });
        console.log("Minted NFT w/ tokenId %s and characterIndex %s", newItemId, _characterIndex);
        NFTHolders[msg.sender] = newItemId;
        _tokenIds.increment();
    }
}
```

First thing is to get the ERC721 which is the standard contract for NFT
```solidity
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
```

Next is to import additioanal stuff that could help us in the future
```solidity
import "@openzeppelin/contracts/utils/Counters.sol";
import "@openzeppelin/contracts/utils/Strings.sol";
```

We will create a counter, this will track the IDS of our NFT so that we knew that they are unique. We set it to a Counter data type then as a token Id
```solidity
Counters for Counters.Counter;
Counters.Counter private _tokenIds;
```

We will create 2 trackers using [[Solidity Mapping]], this mapping will be a variable that will tell us the CharacterStats by their tokenIds and the second variable tells us what tokenIds does an address own. They are both public state
```solidity
mapping(uint256 => CharacterAttributes) public NFTHolderAttributes;
mapping(address => uint256) public NFTHolders;
```

Create a function that will mint the NFT, this is user choice, we will create a parameter that the user could control
```solidity
function mintCharacterNFT(uint256 _characterIndex) external {

}
```

Inside this function, we could get the current tokenId we have, we don't want 0, so we Increment the tokenId in the constructor like
```solidity
_tokenIds.increment(); // result 1
```

Then we could get the value like this
```solidity
uint256 newItemId = _tokenIds.current();
```

We will set some attributes based on a tokenId, and we will base this attributes to the array that we have. We want it to be unqque from each other tokenId so we do it like this. 
```solidity
NFTHolderAttributes[newItemId] = CharacterAttributes({
	characterIndex: defaultCharacters[_characterIndex].characterIndex,
	name:defaultCharacters[_characterIndex].name,
	imageUrl:defaultCharacters[_characterIndex].imageUrl,
	hp:defaultCharacters[_characterIndex].hp,
	maxHp:defaultCharacters[_characterIndex].maxHp,
	attackDamage:defaultCharacters[_characterIndex].attackDamage
});
```

Because we have a tokenId, we could map the current TokenId to the user who sent it
```soldity
NFTHolders[msg.sender] = newItemId;
```

Then at the end, we increment the tokenId so that from 1, it will became 2 the next time somebody else call this function

## TokenURI Encoding

To test things our in our current code, we do this
```js
const run = async () => {
    const contractFactory = await hre.ethers.getContractFactory("MyEpicGame");
    const gameContract = await contractFactory.deploy(
        ["Sylvie", "David Martinez", "Lelouch vi Britannia"],
        ["https://i.pinimg.com/564x/4a/30/89/4a3089bfeb92de031f85086ca83039d1.jpg", 
        "https://i.pinimg.com/564x/17/ba/cb/17bacb6db11c92783d1e94ed19673f0e.jpg", 
        "https://i.pinimg.com/564x/06/f0/d1/06f0d15018e98597b12a988bec6eaadc.jpg"],
        [100, 200, 300],
        [300, 200, 100],
    );
    await gameContract.deployed();
    console.log("Contract Address: " + gameContract.address);

    const newMint = await gameContract.mintCharacterNFT(0);
    await newMint.wait();

    let tokenUri = await gameContract.tokenURI(1);
    console.log("Token URI JSON: " + tokenUri);

    // console.log(await gameContract.NFTHolderAttributes(1));
}

const runMain = async () => {
    try{
        await run();
        process.exit(0);
    }
    catch (error){
        console.log(error);
        process.exit(1);
    }
}
// https://i.pinimg.com/564x/91/f0/51/91f05141d336932ee506366ec9ea7b0c.jpg
runMain();
```

What does this mean?
We deploy the contract with some characteristic or metadata for the default characters
```js
const gameContract = await contractFactory.deploy(
	["Sylvie", "David Martinez", "Lelouch vi Britannia"],
	["https://i.pinimg.com/564x/4a/30/89/4a3089bfeb92de031f85086ca83039d1.jpg", 
	"https://i.pinimg.com/564x/17/ba/cb/17bacb6db11c92783d1e94ed19673f0e.jpg", 
	"https://i.pinimg.com/564x/06/f0/d1/06f0d15018e98597b12a988bec6eaadc.jpg"],
	[100, 200, 300],
	[300, 200, 100],
);
```

We choose to mint the first selection which is my dear Sylvie and we wait till it is finished
```js
const newMint = await gameContract.mintCharacterNFT(0);
await newMint.wait();
```

Then we check the attributes in the tokenURI which will be the official characteristic of the specified tokenID. But where did this come from, from our ERC721 contract import of zeppelin.
```js
let tokenUri = await gameContract.tokenURI(1);
console.log("Token URI JSON: " + tokenUri);
```

![[Pasted image 20221110073815.png]]

When we run this, we get this. We see that the token Uri does not output anything. Why? Because we haven't assigned it!! We only store it inside a mapping but with this null, we can't view the stats or attribites inside OpenSea or NFT markets

What we do is to create  another folder called libraries under contract and inside here is to create a file called Base64.sol. Import this codes from [github](https://gist.github.com/farzaa/f13f5d9bda13af68cc96b54851345832?utm_source=buildspace.so&utm_medium=buildspace_project) and then copy paste it to the file or just get it in the [[Base64 Solidity]]

Import it into our contract sol
```solidity
import "./libraries/Base64.sol";
```

We will use this to convert strings into base64 strings... which is the proper encoding incase of nft used by nft markets. We encode it in [[JSON]] like format like this
```
'{
"name": "CharacterName" 
"--NFT#": 1,
"description": "token NFT",
"image": "url",
"attributes": [
	{
	"trait_type": "HP",
	"value": 100,
	"max_value": 100
	},
	{
	"trait_type": "Attack Damage",
	"value": 100
	}]
}'
```

The full code is this
```solidity
function tokenURI(uint256 _tokenId) public view override returns(string memory){
        CharacterAttributes memory charAttributes = NFTHolderAttributes[_tokenId];

        string memory strHp = Strings.toString(charAttributes.hp);
        string memory strMaxHp = Strings.toString(charAttributes.maxHp);
        string memory strAttackDamage = Strings.toString(charAttributes.attackDamage);
    
        string memory json = Base64.encode(
            abi.encodePacked(
                '{"name": "', charAttributes.name, '", ' 
                '"--NFT#": ', Strings.toString(_tokenId), ', '
                '"description": " NFT To be Minted", '
                '"image": "', charAttributes.imageUrl, '", '
                '"attributes": ['
                    '{'
                    '"trait_type": "HP", '
                    '"value": ', strHp, ', '
                    '"max_value": ', strMaxHp,
                    ' }, '
                    '{'
                    '"trait_type": "Attack Damage", '
                    '"value": ', strAttackDamage,
                    ' }]'
                '}'
            )
        );

        string memory output = string(
            abi.encodePacked("data:application/json;base64,", json)
        );
        
        return output;
    }
```

Create a function to do this. This function will be usable in public and will return something. This function is actually meant to override what we have on the ERC721 contract
```solidity
function tokenURI(uint256 _tokenId) public view override returns(string memory){
}
```

Get the character attributes and store it in memory because it is a [[Solidity Struct]]
```solidity
CharacterAttributes memory charAttributes = NFTHolderAttributes[_tokenId];
```

Numbers or integers will also be converted to strings. Use Strings method `toString`
```solidity
string memory strHp = Strings.toString(charAttributes.hp);
string memory strMaxHp = Strings.toString(charAttributes.maxHp);
string memory strAttackDamage = Strings.toString(charAttributes.attackDamage);
```

Use Base64 encode function, in which we will use inside an abi method `encodePackage` to transform strings to a a json encryption. Store it as a string in memory. Ok, so it means that if it is a state variable, we don't need to specify it as memory right?
```solidity
string memory json = Base64.encode(
	abi.encodePacked(
		'{"name": "', charAttributes.name, '", ' 
		'"--NFT#": ', Strings.toString(_tokenId), ', '
		'"description": " NFT To be Minted", '
		'"image": "', charAttributes.imageUrl, '", '
		'"attributes": ['
			'{'
			'"trait_type": "HP", '
			'"value": ', strHp, ', '
			'"max_value": ', strMaxHp,
			' }, '
			'{'
			'"trait_type": "Attack Damage", '
			'"value": ', strAttackDamage,
			' }]'
		'}'
	)
);
```

Next, combine this string "data:application/json;base64," with the resulting json string. This will use also the encodePacked method
```solidity
string memory output = string(abi.encodePacked("data:application/json;base64,", json));
```

return the resulting output. Now when we run,
![[Pasted image 20221110080629.png]]

If we copy this long text code and paste it to the browser, it will decode like this
![[Pasted image 20221110080714.png]]

## Deploying the NFT

Deploying this will be as easy as [[ERC-20 Deployment]]. Get your url from [QuickNode](https://www.quicknode.com)
Get your url and setup your hardhat config
```js
module.exports = {
  solidity: "0.8.17",
  networks: {
    goerli: {
      url: "urlendpoint",
      accounts: ["privatekey"]
    }
  }
};

```

Then set the deploy.js. We will try to mint our nft's to test it
```js
const run = async () => {
    const contractFactory = await hre.ethers.getContractFactory("MyEpicGame");
    const gameContract = await contractFactory.deploy(
        ["Sylvie", "David Martinez", "Lelouch vi Britannia"],
        ["https://i.pinimg.com/564x/4a/30/89/4a3089bfeb92de031f85086ca83039d1.jpg", 
        "https://i.pinimg.com/564x/17/ba/cb/17bacb6db11c92783d1e94ed19673f0e.jpg", 
        "https://i.pinimg.com/564x/06/f0/d1/06f0d15018e98597b12a988bec6eaadc.jpg"],
        [100, 200, 300],
        [300, 200, 100],
    );

    await gameContract.deployed();
    console.log("Contract Address: " + gameContract.address);

    let newMint = await gameContract.mintCharacterNFT(0);
    await newMint.wait();
    console.log("Minted #1");

    newMint = await gameContract.mintCharacterNFT(1);
    await newMint.wait();
    console.log("Minted #2");

    newMint = await gameContract.mintCharacterNFT(2);
    await newMint.wait();
    console.log("Minted #3");

    newMint = await gameContract.mintCharacterNFT(1);
    await newMint.wait();
    console.log("Minted #4");

    console.log("Done Minting");

}

const runMain = async () => {
    try{
        await run();
        process.exit(0);
    }
    catch (error){
        console.log(error);
        process.exit(1);
    }
}
// https://i.pinimg.com/564x/91/f0/51/91f05141d336932ee506366ec9ea7b0c.jpg
runMain();
```

Then we do run this and then once it is ready, we could now go to [Pixxiti](goerli.pixxiti.com) and see your nft.
We could do it like this
```
https://goerli.pixxiti.com/nfts/INSERT_DEPLOY_CONTRACT_ADDRESS_HERE/INSERT_TOKEN_ID_HERE
```

This is my open sea account and I could already see in my address these minted nfts, we have 4 of them, but this is not allowed in the logic of the game. 
![[Pasted image 20221110093053.png]]

In pixxity, our nft look as follows![[Pasted image 20221110093400.png]]

We have some HP attribute and Attack damage, cool right?

## Boss Data

We are now going to design the boss, but this will not be an nft but a data living inside the [[Smart Contract]]. We first construct using [[Solidity Struct]], then next is to initialize it in the constructor.

```solidity
struct BossAttribute {
	string name;
	string imageUrl;
	uint hp;
	uint maxHp;
	uint attackDamage;
}
```

In constructor
```solidity
constructor(string[] memory name, 
			string[] memory imageUrl, 
			uint256[] memory hp, 
			uint256[] memory attackDamage, 
			string memory bossName, 
			string memory bossImageUrl, 
			uint256 bossHp, 
			uint256 bossAttackDamage) ERC721("Heroes", "HERO"){
	
	bigBoss = BossAttribute(bossName, bossImageUrl, bossHp, bossHp, bossAttackDamage);
	console.log("Big Boss Created called %s with %s HP", bigBoss.name, bigBoss.hp);
}
```

That's it

## Attack On Boss

```solidity
function attackBoss() public {
	uint256 tokenIdOfPlayer = NFTHolders[msg.sender];
	CharacterAttributes storage player = NFTHolderAttributes[tokenIdOfPlayer];
	console.log("\n Player with %s will attack the boss. It has %s HP and %s AD", player.name, player.hp, player.attackDamage);
	console.log("\n Big Boss %s has %s HP and %s AD", bigBoss.name, bigBoss.hp, bigBoss.attackDamage);

	require(player.hp > 0, "Error: Player cannot attack with 0 HP");
	require(bigBoss.hp > 0, "Error: Player cannot attack Boss with 0 HP");

	if(player.attackDamage > bigBoss.hp){
		bigBoss.hp = 0;
	}
	else{
		bigBoss.hp = bigBoss.hp - player.attackDamage;
	}

	if(bigBoss.attackDamage > player.hp){
		player.hp = 0;
	}
	else{
		player.hp = player.hp - bigBoss.attackDamage;
	}

	console.log("Boss has been attacked, its HP was reduced to %s", bigBoss.hp);
	console.log("Player has been attacked, its HP was reduced to %s", player.hp);
}
```

We created a function that will reduce both the player character and the boss. This is a public function
```solidity
function attackBoss() public {

}
```

We get the tokenId possesed by the address... then get the attributes based on the tokenId
```solidity
uint256 tokenIdOfPlayer = NFTHolders[msg.sender];
CharacterAttributes storage player = NFTHolderAttributes[tokenIdOfPlayer];
```

We prevent the player from attacking if the boss hp is 0 or the player hp is 0
```solidity
require(player.hp > 0, "Error: Player cannot attack with 0 HP");
require(bigBoss.hp > 0, "Error: Player cannot attack Boss with 0 HP");
```

Then we prevent negatives because we are using uint, and using int is risky. What we could do is that when the attack is greater than the target's hp then make it automatically 0
```solidity
if(player.attackDamage > bigBoss.hp){
		bigBoss.hp = 0;
	}
else{
	bigBoss.hp = bigBoss.hp - player.attackDamage;
}

if(bigBoss.attackDamage > player.hp){
	player.hp = 0;
}
else{
	player.hp = player.hp - bigBoss.attackDamage;
}
```

Then output this info. And test it  by calling the attackBoss function 3 times with a character with 100 hp

![[Pasted image 20221110122421.png]]

It reverts as soon as the player have 0 hp. We could create a chance mechanism where there is a 50% chance that attacks might miss

So here we think of [[Randomness on Solidity]]
Create a state variable equal to 0
```solidity
uint256 randNum = 0;
```

Create a fucntion that will generat random number
```solidity
function randInt(uint _modulus) internal returns (uint){
}
```

We increment the randNum
```solidity
randNum++;
```

Then return a number that was hashed by keccak, those hashed came from abu encoder with the current time, the address and the random number, then limited by the modulo. 
```solidity
return uint(keccak256(abi.encodePacked(block.timestamp, msg.sender, randNum))) % _modulus;
```

```solidity
function randInt(uint _modulus) internal returns (uint){
	randNum++;
	return uint(keccak256(abi.encodePacked(block.timestamp, msg.sender, randNum))) % _modulus;
}
```

We will use this function to create a chance to miss mechanism. Like this
```solidity
uint256 random = randInt(10);
if(bigBoss.attackDamage > player.hp){
	player.hp = 0;
}
else{
	uint256 random = randInt(10);
	if(random > 4){
		console.log(random);
		player.hp = player.hp - bigBoss.attackDamage;
	}
	else{
		console.log(random);
		console.log("Missed");
	}
}
```

![[Pasted image 20221110125216.png]]




## Interface Functions

One thing to remememver is that when making a contract and integrating it to the front end we must prepare what functionalities do we need first hand

We want to check if the user has our nft, so
```solidity
function checkIfUserHasNFT() public view returns (CharacterAttributes memory){
	uint256 tokenId = NFTHolders[msg.sender];
	if(tokenId > 0){
		return NFTHolderAttributes[tokenId];
	}
	else{
		CharacterAttributes memory empty;
		return empty;
	}
}
```

A function that will get all default characters
```solidity
function getAllDefaultCharacter() public view returns (CharacterAttributes[] memory){
	return defaultCharacters;
}
```

Get boss data
```solidity
function getBigBoss() public view returns (BossAttribute memory){
	return bigBoss;
}
```

## FrontEnd Interface

### Connect to Wallet
We will first make the algorithm that will detect if we have some sort of wallet injected by metamask, if yes, do we have an authorized account active? Of course we will put it inside a [[useEffect]] lifecycle. 

```js
const checkIfWalletIsConnected = async () => {
	try {
	  const {ethereum} = window;
	  if(!ethereum){
		console.log("Get Metamask");
		return;
	  }
	  console.log("Ethereum Object Found");
	
	  const accounts = await ethereum.request({method: 'eth_accounts'});
	  if(accounts.length !== 0){
		const account = accounts[0];
		setCurrentAccount(account);
		console.log("Found authorized account: " + account);
	  }
	  else{
		console.log("No account found");
	  }
	}
	catch (error){
	  console.log(error);
	  return;
	}
  }

useEffect(() => {
	checkIfWalletIsConnected();
}, []);
```

We already did this on [[Metamask on FrontEnd]] and [[Smart Contract on Front End]]. 
We will proceed in creating the button for this.

```js
const connectWallet = async () => {
    try{
      const { ethereum } = window;
      if(!ethereum){
        alert("Install Metamask");
        return;
      }

      const accounts = await ethereum.request({method: "eth_requestAccounts"});
      console.log("Account: " + accounts[0]);
      setCurrentAccount(accounts[0]);
    }
    catch(error){
      console.log(error);
    }
  }
```

And of course the button itself
```js
<button
	className="cta-button connect-wallet-button"
	onClick={connectWallet}
>
	Connect Wallet To Get Started
</button>
```

### Character Selection
Then we creating something like conditional rendering, this new component will be under the folder component
```js
import React, { useEffect, useState } from 'react';
import './SelectCharacter.css';

/*
 * Don't worry about setCharacterNFT just yet, we will talk about it soon!
 */
const SelectCharacter = ({ setCharacterNFT }) => {
  return (
    <div className="select-character-container">
      <h2>Mint Your Hero. Choose wisely.</h2>
    </div>
  );
};

export default SelectCharacter;
```

Now import it to the appjs 
```js
import SelectCharacter from './Components/SelectCharacter';
```

We will create a [[Conditional Rendering]] function that if there is no connected account, we will show the button, if there is a metamask and connected account but no chosen nft, we will show them the nft selection
```js
const renderContent = () => {
    if(!currentAccount){
      return (
      <div className="connect-wallet-container">
        <img
          src="https://64.media.tumblr.com/tumblr_mbia5vdmRd1r1mkubo1_500.gifv"
          alt="Monty Python Gif"
        />
        <button
          className="cta-button connect-wallet-button"
          onClick={connectWallet}
        >
          Connect Wallet To Get Started
        </button>
      </div>
      )
    }
    else if (currentAccount && !characterNFT){
      return <SelectCharacter setCharacterNFT={setCharacterNFT} />;
    }
  }
```

Then activate it to the main return like this
```js
{renderContent()}
```

### Fetch Character
This will be called at the start of the application if a wallet is connected. USe a [[useEffect]]
```js
  useEffect(() => {
    const fetchNFTMetaData = async() => {
      console.log("Cheking for NFT in address: " + currentAccount);
      const provider = new ethers.providers.Web3Provider(window.ethereum);
	    const signer = provider.getSigner();
	    const gameContract = new ethers.Contract(CONTRACT_ADDRESS, myEpicGame.abi, signer);
	
	    const txn = await gameContract.checkIfUserHasNFT();
	    if(txn.name){
	      console.log("Has character nft");
	      setCharacterNFT(txn);
	    }
	    else{
	      console.log("No character nft");
	    }
	    }
	
	    if(currentAccount){
	      console.log("Account: " + currentAccount);
	      fetchNFTMetaData();
	    }
	  }, [currentAccount])
```

Breaking this down, we initialize the contract
```js
const provider = new ethers.providers.Web3Provider(window.ethereum);
const signer = provider.getSigner();
const gameContract = new ethers.Contract(CONTRACT_ADDRESS, myEpicGame.abi, signer);
```

Get character data, if a character exist, log Has chaacter, if not , no character
```js
const txn = await gameContract.checkIfUserHasNFT();
if(txn.name){
  console.log("Has character nft");
  setCharacterNFT(txn);
}
else{
  console.log("No character nft");
}
```

Only execute the function if the account exist
```js
if(currentAccount){
	  console.log("Account: " + currentAccount);
	  fetchNFTMetaData();
}
```

Execute this function everytime this variable change set on the second parameter
```js
[currentAccount]
```

### Minting 
We update the useEffect like thi
```js
  useEffect(() => {
    const getCharacter = async() => {
      try {
        console.log("Getting characters to mint");

        const characterTxn = await gameContract.getAllDefaultCharacter();
        // console.log("Characters: " + characterTxn);

        const characters = characterTxn.map((characterData) => {
          return transformCharacterData(characterData);
        })

        console.log("Characters: " + characters[0].imageUrl)

        setCharacters(characters);
        
      } catch (error) {
        console.log(error);
      }
    }

    const onCharacterMint = async(sender, tokenId, characterIndex) => {
      console.log(
      `CharacterNFTMinted - sender: ${sender} tokenId: ${tokenId.toNumber()} characterIndex: ${characterIndex.toNumber()}`
    );
      if(gameContract){
        const characterNFT = await gameContract.checkIfUserHasNFT();
        console.log("CharacterNFT: " + characterNFT);
        setCharacterNFT(transformCharacterData(characterNFT));
      }
    }

    if(gameContract){
      getCharacter();
      gameContract.on("CharacterMinted", onCharacterMint);
    }

    return () => {
      if(gameContract){
        gameContract.off("CharacterMinted", onCharacterMint);
      }
    }
    
  }, [gameContract]);
```

What we add here is a method that will detect ane vent to the contract
```js
gameContract.on("CharacterMinted", onCharacterMint);
```

This have 2 arguments, the event name and then the function to execute, this will automatically get the arguments inside the event 
We do it like this. The function will have 3 arguments as indicated to the created event. Output this out.
```js
const onCharacterMint = async(sender, tokenId, characterIndex) => {
  console.log(
  `CharacterNFTMinted - sender: ${sender} tokenId: ${tokenId.toNumber()} characterIndex: ${characterIndex.toNumber()}`
);
  if(gameContract){
	const characterNFT = await gameContract.checkIfUserHasNFT();
	console.log("CharacterNFT: " + characterNFT);
	setCharacterNFT(transformCharacterData(characterNFT));
  }
}
```

We could check if the user not has an nft, then outputit, and use the function;s setCharacterNFT to store this, this is a hook function located at the app.js. 

```js
if(gameContract){
	const characterNFT = await gameContract.checkIfUserHasNFT();
	console.log("CharacterNFT: " + characterNFT);
	setCharacterNFT(transformCharacterData(characterNFT));
}
```

Turn off the listener at the end
```js
return () => {
	if(gameContract){
		gameContract.off("CharacterMinted", onCharacterMint);
	}
}
```

### Get Boss
```js
import React, {useState, useEffect} from "react";
import { ethers } from 'ethers';
import { CONTRACT_ADDRESS, transformCharacterData } from '../../constant.js';
import myEpicGame from '../../utils/MyEpicGames.json';
import './Arena.css';

const Arena = ({characterNFT, setCharacterNFT, currentAccount}) => {
  const [gameContract, setGameContract] = useState(null);
  const [boss, setBoss] = useState(null);
  const [attackState, setAttackState] = useState('');
  
  useEffect(() => {
    const { ethereum } = window;

    if(ethereum){
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      const gameContract = new ethers.Contract(CONTRACT_ADDRESS, myEpicGame.abi, signer);

      setGameContract(gameContract);
    }
    else{
      console.log("No ethereum wallet found");
    }

  }, [])

  useEffect(() => {
    const fetchBoss = async() => {
      const bossTxn = await gameContract.getBigBoss();
      console.log("Boss: " + transformCharacterData(bossTxn));
      setBoss(transformCharacterData(bossTxn));
    }


    if(gameContract){
      fetchBoss();
    }
    
  }, [gameContract])

  return (
    <div className="arena-container">
      {boss && (
        <div className="boss-container">
        <div className={`boss-content ${attackState}`}>
          <h1>{boss.name}</h1>
          <div className="image-content">
            <img src={boss.imageUrl} alt={`Boss ${boss.name}`} />
            <div className="health-bar">
              <progress value={boss.hp} max={boss.maxHp} />
              <p>{`${boss.hp} / ${boss.maxHp} HP`}</p>
            </div>
          </div>
        </div>
        <div className="attack-container">
          <button className="cta-button" onClick={runAttackAction}>
            {`💥 Attack ${boss.name}`}
          </button>
        </div>
        </div>  
      )}

      {characterNFT && (
        <div className="player-container">
          <div className="player-container">
            <h2>Your Character</h2>
            <div className="player">
              <div className="image-content">
                <h2>{characterNFT.name}</h2>
                <img src={characterNFT.imageUrl} alt={`Image of ${characterNFT.name}`} />
                <div className="health-bar">
                  <progress value={characterNFT.hp} max={characterNFT.maxHp} />
                  <p>{`${characterNFT.hp} / ${characterNFT.maxHp} HP`}</p>
                </div>
              </div>  
              <div className="stats">
              <h4>{`⚔️ Attack Damage: ${characterNFT.attackDamage}`}</h4>
            </div>
            </div>
          </div>
        </div>
      )} 
    </div>
  )
}

export default Arena;
```

The thing that is important here is that we are passing the character nft from the app.js to the function as well as its hook function and currentAccount. 
```js
const Arena = ({characterNFT, setCharacterNFT, currentAccount}) => {}
```

We create 3 state variables for gamecontract, the boss and the attack state for later use
```js
const [gameContract, setGameContract] = useState(null);
const [boss, setBoss] = useState(null);
const [attackState, setAttackState] = useState('');
```

We fetch the boss at the start of our application and update it when the game contract change. Keep in mind to transform the boss
```js
  useEffect(() => {
    const fetchBoss = async() => {
      const bossTxn = await gameContract.getBigBoss();
      console.log("Boss: " + transformCharacterData(bossTxn));
      setBoss(transformCharacterData(bossTxn));
    }
    
    if(gameContract){
      fetchBoss();
    }
    
  }, [gameContract])
```

Then we pass it as an interface if the boss state variable is ready
```js
{boss && (<div></div>)}
```

Player's nft is inside the passed parameter, so we could just do this as normal
```js
{characterNFT && (<div></div>)}
```

### Attack function
```js
import React, {useState, useEffect} from "react";
import { ethers } from 'ethers';
import { CONTRACT_ADDRESS, transformCharacterData } from '../../constant.js';
import myEpicGame from '../../utils/MyEpicGames.json';
import './Arena.css';

const Arena = ({characterNFT, setCharacterNFT, currentAccount}) => {
  const [gameContract, setGameContract] = useState(null);
  const [boss, setBoss] = useState(null);
  const [attackState, setAttackState] = useState('');
  
  useEffect(() => {
    const { ethereum } = window;

    if(ethereum){
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      const gameContract = new ethers.Contract(CONTRACT_ADDRESS, myEpicGame.abi, signer);

      setGameContract(gameContract);
    }
    else{
      console.log("No ethereum wallet found");
    }

  }, [])

  useEffect(() => {
    const fetchBoss = async() => {
      const bossTxn = await gameContract.getBigBoss();
      console.log("Boss: " + transformCharacterData(bossTxn));
      setBoss(transformCharacterData(bossTxn));
    }

    const onAttackComplete = (from, newBossHp, newPlayerHp) => {
      const bossHp = newBossHp.toNumber();
      const playerHp = newPlayerHp.toNumber();
      const sender = from.toString();
      console.log(`AttackComplete: Boss Hp: ${bossHp} Player Hp: ${playerHp}`);

      if(currentAccount === sender.toLowerCase()){
        setBoss((prevState) => {
          return {...prevState, hp: bossHp};
        });
        
        setCharacterNFT((prevState) => {
          return { ...prevState, hp: playerHp };
        });
      } 
    else {
        setBoss((prevState) => {
            return { ...prevState, hp: bossHp };
        });
    }
    }

    if(gameContract){
      fetchBoss();
      gameContract.on('AttackComplete', onAttackComplete);
    }

    return () => {
      if(gameContract){
        gameContract.off('AttackComplete', onAttackComplete);
      }
    }
  }, [gameContract])

  const runAttackAction = async () =>{
    try {
      if(gameContract){
        setAttackState("attacking");
        console.log("Attacking boss...");
        const attackTxn = await gameContract.attackBoss({gasLimit: 300000});
        await attackTxn.wait();
        console.log('attackTxn:', attackTxn);
        setAttackState('hit');
      }
    } catch (error) {
      console.error('Error attacking boss:', error);
      setAttackState('');
    }
  }

  return (
    <div className="arena-container">
      {boss && (
        <div className="boss-container">
        <div className={`boss-content ${attackState}`}>
          <h1>{boss.name}</h1>
          <div className="image-content">
            <img src={boss.imageUrl} alt={`Boss ${boss.name}`} />
            <div className="health-bar">
              <progress value={boss.hp} max={boss.maxHp} />
              <p>{`${boss.hp} / ${boss.maxHp} HP`}</p>
            </div>
          </div>
        </div>
        <div className="attack-container">
          <button className="cta-button" onClick={runAttackAction}>
            {`💥 Attack ${boss.name}`}
          </button>
        </div>
        </div>  
      )}

      {characterNFT && (
        <div className="player-container">
          <div className="player-container">
            <h2>Your Character</h2>
            <div className="player">
              <div className="image-content">
                <h2>{characterNFT.name}</h2>
                <img src={characterNFT.imageUrl} alt={`Image of ${characterNFT.name}`} />
                <div className="health-bar">
                  <progress value={characterNFT.hp} max={characterNFT.maxHp} />
                  <p>{`${characterNFT.hp} / ${characterNFT.maxHp} HP`}</p>
                </div>
              </div>  
              <div className="stats">
              <h4>{`⚔️ Attack Damage: ${characterNFT.attackDamage}`}</h4>
            </div>
            </div>
          </div>
        </div>
      )}
    </div>
  )
}

export default Arena;
```

Create a function that wil call the attack on a button. We will change the attack state that will be used a a class 
```js
const runAttackAction = async () =>{
	try {
		if(gameContract){
			setAttackState("attacking");
			console.log("Attacking boss...");
			const attackTxn = await gameContract.attackBoss({gasLimit: 300000});
			await attackTxn.wait();
			console.log('attackTxn:', attackTxn);
			setAttackState('hit');
		}
	}
	} catch (error) {
		  console.error('Error attacking boss:', error);
		  setAttackState('');
	}
}
```

```js
<div className={`boss-content ${attackState}`}>
```

How do we update the attack on the interface. Use event listeners
```js
gameContract.on('AttackComplete', onAttackComplete);
```

The attack function is isnde a usestate so that we could clear it in the end
```js
const onAttackComplete = (from, newBossHp, newPlayerHp) => {
  const bossHp = newBossHp.toNumber();
  const playerHp = newPlayerHp.toNumber();
  const sender = from.toString();
  console.log(`AttackComplete: Boss Hp: ${bossHp} Player Hp: ${playerHp}`);

  if(currentAccount === sender.toLowerCase()){
	setBoss((prevState) => {
	  return {...prevState, hp: bossHp};
	});
	
	setCharacterNFT((prevState) => {
	  return { ...prevState, hp: playerHp };
	});
  } 
}
```

We have some additional conditioning here. If the sender damage the boss, we will update the bossHp and the playerHp
```js
  if(currentAccount === sender.toLowerCase()){
	setBoss((prevState) => {
	  return {...prevState, hp: bossHp};
	});
	
	setCharacterNFT((prevState) => {
	  return { ...prevState, hp: playerHp };
	});
  } 
```

Else, we will update on ly the boss
```js
else {
	setBoss((prevState) => {
		return { ...prevState, hp: bossHp };
	});
}
```

Clean the listener
```js
return () => {
  if(gameContract){
	gameContract.off('AttackComplete', onAttackComplete);
  }
}
```

### Loading Component
It is fairly quite simple,We just need to use a state variable to switch between true and false if we are suppossed to show load or turn off

```
const [isLoading, setIsLoading] = useState(false);
```

Note that if you have different components, we use different name variables just for the sake of readability and also prevent collisions. 

## Images

Actually, do not just get links from somewhere, upload it into an ipfs like [Pinata](https://www.pinata.cloud/?utm_source=buildspace&utm_medium=buildspace_project)





# Metatags
###### Related: [[Solidity Language]], [[React]], [[NPX]]
###### Tags: 
###### Source: 

---