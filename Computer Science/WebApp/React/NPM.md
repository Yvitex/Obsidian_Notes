# NPM
Short for node package manager. A way to install modules written by other developers and implement it inside our website. 

## Installing
There are 2 ways to do this, one is
```shell
$ npm i cowsay
```

Where it will install the module only inside the folder we are currently working with
The second way is
```shell
$ npm i -g cowsay
```

Where it will be isntalled globally, inside many places. Or even to future projects we want to have

## Execution
To execute this, we basically say
```shell
$ cowsay hi
```
![[Pasted image 20220723055127.png]]

```ad-Upset
title: Awww
collapse: open
This only works for global installation

```

## Uninstall
Simply we say
```shell
$ npm uninstall -g cowsay
```

Without -g if local.


