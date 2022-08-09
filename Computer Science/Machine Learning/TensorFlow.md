# Tensor Flow
Is a library that contains pre built [[Machine Learning Algoritm|model]]s and works for numerical computation using [[GPU]]

To install tensorflow, rung hte following code
```python
import tensorflow as tf
```

Along this, we might also want to import [[Tensor Flow Hub]]
We also want to check whether we have an access to [[gpu]]
```python
print("Gpu Access: ", "Present 😎" if tf.config.list_physical_devices("GPU") else "Not Present 🔪")
```

![[Pasted image 20220806092706.png]]

If not available, do the following. Go to Runtime > Runtime Type > Select GPU

[[Tensor Flow Workflow]]
