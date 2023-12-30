# **Matplotlib的使用**

```python
# 导入Matplotlib
import matplotlib.pyplot as plt
```

## 1. 添加画板

```python
fig = plt.figure()
```

## 2. 添加绘图的基准（轴）——画纸

```python
# 添加了axes，意思是在画板的第1行第1列生成一个Axes对象来作画，如有：fig.add_subplot(2, 2, 1),表示将画板分成2 × 2的方格，1代表在第一个方格中是生成画纸
ax = fig.add_subplot(1, 1, 1)
ax.set(xlim=[0.5, 4.5], ylim=[-2, 8], title='An Example Axes', ylabel='Y-Axis', xlabel='X-Axis')
plt.show()
```

```python
# 添加多个画纸
fig, axes = plt.subplots(nrows=2, ncols=2)
axes[0, 0].set(title = 'Upper Left')
axes[0, 1].set(title = 'Upper Right')
axes[1, 0].set(title = 'Lower Left')
axes[1, 1].set(title = 'Lower Right')
```

![多个画纸](Data\多个画纸.png)

## 3. 简单的绘图方式

```python
plt.plot([1, 2, 3, 4], [10, 20, 25, 30], color='lightblue', linewidth=3)
# 限制X轴的显示范围
plt.xlim(0.5, 4.5)
plt.show()
```

![简单的直线](..\Data\简单的直线.png)

## 4. 基本的2D绘图

```python
import numpy as np
```

```python
# 线(画点连线法)
x = np.linspace(0, np.pi)
y_sin = np.sin(x)
y_cos = np.cos(x)
fig, ax1 = plt.subplots()
ax1.plot(x, y_sin)
fig, ax2 = plt.subplots()
ax2.plot(x, y_sin, 'go--', linewidth=2, markersize=12)
fig, ax3 = plt.subplots()
ax3.plot(x, y_cos, color='red', marker='+', linestyle='dashed')
plt.show()
```

![sin_1](..\Data\sin_1.png)

![sin_2](..\Data\sin_2.png)

![cos](..\Data\cos.png)

```python
x = np.linspace(0, 10, 200)
data_obj = {
    'x':x,
    'y1':2*x+1,
    'y2':3*x+1.2,
    'mean':0.5*x*np.cos(2 * x) + 2.5 * x + 1.1
}
fig, ax = plt.subplots()
# 填充两条线之间的颜色
ax.fill_between('x', 'y1', 'y2', color='yellow', data=data_obj)
ax.plot('x', 'mean', color='black', data=data_obj)
plt.show()
```

![射线](..\Data\射线.png)

```python
# 散点图
x = np.arange(10)
y = np.random.randn(10)
plt.scatter(x, y, color='red', marker='+')
plt.show()
```

![散点图](..\Data\散点图.png)SS

```python
# 条形图
np.random.seed(1)
x = np.arange(5)
y = np.random.randn(5)
fig, axes = plt.subplots(ncols = 2, figsize=plt.figaspect(1. / 2))
vert_bars = axes[0].bar(x, y, color='lightblue', align='center')
horiz_bars=axes[1].barh(x, y, color='lightblue', align='center')

# 在水平或垂直方向上画线
axes[0].axhline(0, color='gray', linewidth=2)
axes[1].axvline(0, color='gray', linewidth=2)
plt.show()
```

![条形统计图](..\Data\条形统计图.png)
