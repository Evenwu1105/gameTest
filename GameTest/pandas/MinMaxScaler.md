## 归一化


```python
#对数据进行归一化处理  
from sklearn.preprocessing import MinMaxScaler  
  
scaler = MinMaxScaler()  
data_cleaned[numeric_cols] = scaler.fit_transform(data_cleaned[numeric_cols])  
  
# 设定目标变量  
target_variable = 'SeriousD1qin2yrs'
```

## 对需要归一化的列进行处理

```python
scaler = MinMaxScaler()  
columns_to_normalize = ['年龄','体重','身高']  
data[columns_to_normalize] = scaler.fit_transform(data[columns_to_normalize])
```

