# React Native
Native means it is optimized to run on mobile like java or kotlin which are built entirely for abdroid and like ios programming language such as objective c and swift.

React native could run in both android and ios application

## Advantage
- Higher community menaing much more resources and help
- Bic companies hire people
- Cross platorm available, we could use it sideby side with other programming language to increae optimal activity

The syntax is like [[React]]

## Main Parts
Programming in react native is just small rectanges inside rectangles combined together to create a program. It is composed of the *core components* and *native components* and also receives information using the device [[API]]
![[Pasted image 20220718041328.png]]


React native component, at compilation is converted into device specific views. Fron native vew, to viewgrouop then become UIView in ios. 
![[Pasted image 20220718041429.png]]


Core componennt on the other hand is react specific in which native components are inside of it,![[Pasted image 20220718041753.png]]
## How this works?
React native converts views into native views. It also sends the [[Javascript]] along with the [[javascript core]] that will enable the use of logic to the mobile devices as they do not understand javascript at all. [[javascript core]] is a virtual machien that runs javascript to make it functional. Because of this, performance must be slower than user native programming language such as [[JAVA]]. [[Javascript]] and the [[javascript core]] communicates with the mobile devices using what we call a React [[Native Bridge]] so that they could understand each other.

```ad-Danger
title: Shit!!! An update
collapse: open
Android could now utilize the use of Hermes

```

[[Android Architecture|android]] now implemented the use of a new [[Javascript]] virtual machine called [[Hermes]] 

```ad-Attention
title: Question!!!
collapse: open
Do we use [[CSS]] in this programming framework?

```

No. We use [[Javascript]] styling that mimics the [[CSS]]. We could plactice the use of react native in a web application called [[Expo]]


More information [here](https://reactnative.dev/docs/intro-react-native-components)
