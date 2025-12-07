- ## 来源：网易-免费
- ## 用途：各种软件测试
- ## 兼容性：支持各种操作系统
- ## 支持不同元素定位方式（图像定位，元素定位）
- ##  ==touch点击==![[Pasted image 20251118204501.png]]
- ## 隐式等待![[Pasted image 20251118204537.png]]
- ## 滑动Swipe![[Pasted image 20251118204631.png]]
- ## 是否存在页面元素![[Pasted image 20251118204705.png]]
- ## 填写文本![[Pasted image 20251118204813.png]]
- ## 手机固定按键点击事件 ![[Pasted image 20251118205049.png]]
- ## 截图![[Pasted image 20251118205206.png]]
- ## 显示等待 ![[Pasted image 20251118205245.png]]
- ## 断言![[Pasted image 20251118205343.png]]
- ## 断言图标是否存在 ![[Pasted image 20251118205502.png]]
- #### `Template()` 类（图像定位核心）

`Template()` 是 Airtest 图像识别定位的核心类，用于定义 “图像模板”，框架会通过该模板在屏幕上匹配对应的元素位置。

Airtest 核心 API（`from airtest.core.api import touch`），用于模拟设备的触摸操作（点击 / 长按）。

降低阈值（如 `threshold=0.6`）；