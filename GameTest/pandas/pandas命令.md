## 加载数据集并且指定编码

```python
import pandas as pd
data = pd.read_csv('medical_data.csv', encoding='gbk')
```

## 查看表结构基础信息

```python
print(data.info)
```

## 重命名列名

```python
data.rename(columns={'病人ID': '患者ID'}, inplace=True)
```


## 只根据“患者ID”列去重（相同ID的行视为重复）

```python
data.drop_duplicates(subset=['患者ID'], inplace=True)
```

## 检测重复行

```python
duplicates = data.duplicated()
```

