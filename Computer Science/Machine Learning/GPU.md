# Graphical Processing Unit
Check whether we have an access to [[gpu]] using [[TensorFlow]]
```python
print("Gpu Access: ", "Present 😎" if tf.config.list_physical_devices("GPU") else "Not Present 🔪")
```

![[Pasted image 20220806092706.png]]

If not available, do the following. Go to Runtime > Runtime Type > Select GPU
