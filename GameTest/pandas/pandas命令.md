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

## 对需要归一化的列进行处理

```python
scaler = MinMaxScaler()  
columns_to_normalize = ['年龄','体重','身高']  
data[columns_to_normalize] = scaler.fit_transform(data[columns_to_normalize])
```

>[!NOTE] 
>`plot` 是 pandas 中 DataFrame/Series 对象的**内置绘图方法**
>`bar` 是 `plot` 方法中 `kind` 参数的一个可选值，代表**柱状图（垂直柱状图）**，用于展示**分类数据的数值对比**（如不同类别的数量、平均值、总和等）。
当 `kind='bar'` 时，绘制的是**垂直柱状图**（柱子垂直向上，x 轴是类别，y 轴是数值）。
若用 `kind='barh'`，则绘制**水平柱状图**（柱子水平向右，y 轴是类别，x 轴是数值）。

```python
数据对象.plot(kind=图表类型, ...其他参数)
```

## 例:
```python
# 统计治疗结果分布  
treatment_outcome_distribution = data.groupby('疾病类型')['治疗结果'].value_counts().unstack()
# 绘制柱状图  
treatment_outcome_distribution.plot(kind='bar', stacked=True)
```

>[!NOTE] 
>`unstack()` 是 pandas 中用于**重塑数据结构**的重要方法，作用是将 DataFrame 中的**行索引（index）“旋转” 为列**，简单说就是 “把行上的层级信息展开到列上”，让数据从 “紧凑格式” 变为 “展开格式”。

```python
# 示例数据（先创建一个带多层行索引的 Series/DataFrame）
data = pd.Series(
    [15, 20, 10, 12],
    index=pd.MultiIndex.from_tuples(
        [('感冒', '男'), ('感冒', '女'), ('发烧', '男'), ('发烧', '女')],
        names=['疾病类型', '性别']  # 行索引的层级名称
    ),
    name='人数'
)

print("原始数据（堆叠状态）：")
print(data)
# 输出：
# 疾病类型  性别
# 感冒     男      15
#         女      20
# 发烧     男      10
#         女      12
# Name: 人数, dtype: int64

# 使用 unstack() 展开（默认将最后一层行索引转为列）
unstacked = data.unstack()
print("\nunstack() 后（展开状态）：")
print(unstacked)
# 输出：
# 性别      女   男
# 疾病类型
# 感冒     20  15
# 发烧     12  10
```
