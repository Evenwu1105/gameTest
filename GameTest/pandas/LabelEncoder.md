## 归一化

```python
from sklearn.preprocessing import LabelEncoder  
  
# 归一化 'How do you describe your current level of fitness ?' 列  
label_encoder = LabelEncoder()  
data_cleaned['How do you describe your current level of fitness ?'] = label_encoder.fit_transform(data_cleaned['How do you describe your current level of fitness ?'])  
  
print(data_cleaned['How do you describe your current level of fitness ?'].unique())
```

# 图片归一化
- 对像素值进行归一化的处理