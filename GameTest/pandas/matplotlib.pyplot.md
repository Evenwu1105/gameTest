`matplotlib.pyplot` 是 Python 中最常用的绘图库 `matplotlib` 的核心模块，提供了一套类似 MATLAB 的绘图接口，方便用户快速创建各类可视化图表（如折线图、散点图、柱状图、饼图等）。

### 核心特点

- 语法简洁，贴近直觉，适合快速绘图和调试。
- 支持高度自定义（颜色、字体、标签、图例等）。
- 可与 NumPy、Pandas 等数据处理库无缝配合。

### 基本使用流程

1. **导入模块**（通常简写为 `plt`）：
    
    python
    
    运行
    
    ```python
    import matplotlib.pyplot as plt
    ```
    
2. **准备数据**（如 NumPy 数组或 Pandas 数据结构）：
    
    python
    
    运行
    
    ```python
    import numpy as np
    x = np.linspace(0, 10, 100)  # 0到10的100个均匀点
    y = np.sin(x)                # 正弦函数值
    ```
    
3. **绘制图表**（调用 `plt` 的绘图函数）：
    
    python
    
    运行
    
    ```python
    plt.plot(x, y)  # 绘制折线图
    ```
    
4. **添加标签和装饰**：
    
    python
    
    运行
    
    ```python
    plt.title("正弦函数曲线")  # 标题
    plt.xlabel("x轴")         # x轴标签
    plt.ylabel("y轴")         # y轴标签
    plt.grid(True)            # 显示网格
    ```
    
5. **显示或保存图表**：
    
    python
    
    运行
    
    ```python
    plt.show()  # 在窗口中显示图表
    # 或保存为图片
    # plt.savefig("sine.png", dpi=300)
    ```
    

### 常用绘图函数

| 函数              | 功能        |
| --------------- | --------- |
| `plt.plot()`    | 折线图 / 曲线  |
| `plt.scatter()` | 散点图       |
| `plt.bar()`     | 柱状图（垂直）   |
| `plt.barh()`    | 柱状图（水平）   |
| `plt.pie()`     | 饼图        |
| `plt.hist()`    | 直方图（数据分布） |
| `plt.boxplot()` | 箱线图（统计分布） |
| `plt.imshow()`  | 显示图像      |