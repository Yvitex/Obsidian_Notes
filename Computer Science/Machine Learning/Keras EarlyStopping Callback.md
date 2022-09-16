---
aliases: [tf.keras.callbacks.EarlyStopping()]
---
# Early Stopping
To do this, we only need the return value of early stopping or instanc eof it. 

```python
early_stopper = tf.keras.callbacks.EarlyStopping(monitor="val_accuracy", 
												 patience=3)
```

## Params
- monitor : what metrics to monitor. the default is val_loss
- patience :