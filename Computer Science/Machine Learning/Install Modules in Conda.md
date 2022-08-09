# Installation
Using [[Conda]] we could simply activate our environment then use the command
```shell
$ conda install seaborn
```

But an alternative way to do this is inside the [[Jupyter]] notebook using the [[Sytem Module]]
```python
import sys
```

To use the terminal inside the notebook, we use the bang method to do so like
```python
!dir
```

There fore we could use the terminal inside this [[Jupyter]] notebook
```python
import sys
!conda install --yes --prefix {sys.prefix} seaborn
```

What this will do is going t yes all selection and set the prefix to the environment path, in our code is the `sys.prefix`
```python
sys.prefix
```
![[Pasted image 20220801120021.png]]
