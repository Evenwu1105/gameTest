## 归一化

```python
#对数据进行归一化处理  
from sklearn.preprocessing import MinMaxScaler  
  
scaler = MinMaxScaler()  
data_cleaned[numeric_cols] = scaler.fit_transform(data_cleaned[numeric_cols])  
  
# 设定目标变量  
target_variable = 函已OU如qin2yF