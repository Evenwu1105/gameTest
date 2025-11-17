## 加载数据集并且指定编码

```python
import pandas as pd
data = pd.read_csv('medical_data.csv', encoding='gbk')
```

## 查看表结构基础信息

```python
print(data.info)
```


