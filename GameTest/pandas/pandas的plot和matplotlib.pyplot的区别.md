
>[!NOTE] 
>[[matplotlib.pyplot]] 是 Python 中最常用的**数据可视化库**，专门用于绘制各种图表（如折线图、柱状图、散点图、直方图等），让数据以直观的图形方式呈现，方便分析和展示。


>[!NOTE]
>- **[[pandas的plot]]（pandas）**：负责 “快速基于数据绘图”，简化数据与图表的绑定过程。
>- **[[matplotlib.pyplot]]（matplotlib）**：负责 “美化和控制图表细节”，是所有 matplotlib 系图表的通用调整工具。

```python
plt.scatter(data['年龄',data['疾病严重程度']])
```

>[!NOTE] 
>### 与 pandas 的 `plot(kind='scatter')` 区别：
>- `plt.scatter(x, y)` 是 matplotlib 原生函数，需要手动传入 x 和 y 轴的具体数据（如列表、数组）。
>- pandas 的 `df.plot(kind='scatter', x='列名', y='列名')` 是基于 `plt.scatter()` 的封装，更方便直接使用 DataFrame 中的列作为 x、y 轴数据（无需手动提取）。

两者最终效果一致，只是使用场景不同：原生函数更灵活，pandas 封装更简洁（适合直接基于表格数据绘图）。
