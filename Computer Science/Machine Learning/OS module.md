---
aliases: [os]
---
# System Module
A way to access the internal system of the computer
```python
import os
```

It could do various things from outputing every item int he filepath
```python
print(os.listdir("/content/drive/MyDrive/dog_identification/train/"))
```

To Join a path file with additional string
```python
dir = os.path.file("/content/drive/MyDrive/dog_identification/model", datetime.now().strftime("%Y"))
```

