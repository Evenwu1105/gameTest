Pandas 的 `plot` 是基于 Matplotlib 封装的绘图接口，直接集成在 Series 和 DataFrame 中，可快速将数据转换为可视化图表，无需手动处理数据格式，尤其适合与 Pandas 数据结构（Series、DataFrame）配合使用。

### 核心特点

- 语法极简：一行代码即可绘图（如 `df.plot()`）。
- 自动关联数据：索引自动作为 x 轴，列值作为 y 轴。
- 支持多种图表类型：折线图、柱状图、饼图、散点图等。
- 可无缝对接 Matplotlib 的 API 进行精细化调整（如添加标题、标签等）。

### 基本使用方法

Pandas 的绘图功能主要通过 `Series.plot()` 或 `DataFrame.plot()` 调用，语法如下：

python

运行

```python
# Series 绘图
s.plot(kind='图表类型', **kwargs)

# DataFrame 绘图（每列对应一条线/一个系列）
df.plot(kind='图表类型',** kwargs)
```

- `kind`：指定图表类型（默认是折线图），可选值包括 `'line'`（折线）、`'bar'`（柱状）、`'barh'`（水平柱状）、`'pie'`（饼图）、`'scatter'`（散点）、`'hist'`（直方图）等。
- `**kwargs`：传递额外参数（如标题、颜色、大小等）。

### 常用图表示例

#### 1. 折线图（默认类型）

适合展示数据随时间的变化趋势：

python

运行

```python
import pandas as pd
import matplotlib.pyplot as plt

# 示例数据：日期为索引，两列数值
data = {
    '产品A销量': [120, 150, 130, 180, 200],
    '产品B销量': [90, 110, 140, 160, 190]
}
df = pd.DataFrame(data, index=pd.date_range('2023-01-01', periods=5))

# 绘制折线图（默认kind='line'）
df.plot(figsize=(10, 6))  # figsize指定图表大小
plt.title('产品销量趋势', fontsize=14)
plt.xlabel('日期')
plt.ylabel('销量')
plt.grid(alpha=0.3)  # 网格透明度
plt.show()
```