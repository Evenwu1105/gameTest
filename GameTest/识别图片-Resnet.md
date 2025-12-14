# 模型加载
```python
session = ort.InferenceSession('resnet.onnx')
```
inference 推理
```python
top5_idx = np.argsort(probabilities[0])[-5:][::-1] #由小到大排序，取倒数五个
```
去除首尾的空格
```python
name.strip()
```

