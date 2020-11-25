---
title: Python-Matplotlib-Pyplot教程
abbrlink: 21604
date: 2020-11-25 16:54:00
tags:
---

### Pyplot教程

#### pyplot简介

[`matplotlib.pyplot`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html#module-matplotlib.pyplot)是使matplotlib像MATLAB一样工作的函数的集合。每个`pyplot`功能都会对图形进行一些更改：例如，创建图形，在图形中创建绘图区域，在绘图区域中绘制一些线条，用标签装饰绘图等。

> 使用pyplot生成可视化的效果非常快：

```python
plt.plot([1,2,3,4])
plt.ylabel('num')
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/7de3260fe8f8ea7e78c0e32906e6d4d5.png" style="zoom:80%;margin-left:10px" />

关于上面这个示例中，x轴范围0-3,y轴范围1-4,原因是如果你向Plot传递单个列表或数组，那么matplotlib假定它是y轴的序列，并自动为你生成从0开始的x值

---

#### plot的样式

> 对于每对x，y参数，都有一个可选的第三个参数，它是表示图的颜色和线型的格式字符串。格式字符串的字母和符号来自MATLAB，您将颜色字符串与线型字符串连接在一起。默认格式字符串是“ b-”，这是一条蓝色实线。

例如，要用红色圆圈绘制以上内容：

```python
plt.plot([1,2,3,4],[1,4,9,16],'ro') #'r':red,'o':点
plt.axis([0,6,0,20])                #确定坐标轴的范围，x轴0-6，y轴0-20
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/15/db2a3f7ecb19275e460762ead8cffa7d.png" style="zoom:80%;margin-left:10px" />

> 格式字符串由颜色，标记物和线条组成
>
> ```
> fmt = '[marker][line][color]'  #其他组合也是允许的，例如[color][marker][line]
> ```

> **每一个参数都是可选的。**

> Markers(标记物)

| 字符  | 描述               |
| ----- | ------------------ |
| `'.'` | 点标记             |
| `','` | 像素标记           |
| `'o'` | 圆圈标记           |
| `'v'` | triangle_down标记  |
| `'^'` | 三角形标记         |
| `'<'` | triangle_left标记  |
| `'>'` | triangle_right标记 |
| `'1'` | tri_down标记       |
| `'2'` | tri_up标记         |
| `'3'` | tri_left标记       |
| `'4'` | tri_right标记      |
| `'s'` | 方形标记           |
| `'p'` | 五边形标记         |
| `'*'` | 星标               |
| `'h'` | 六角形标记         |
| `'H'` | 六角标记           |
| `'+'` | 加号               |
| `'x'` | X标记              |
| `'D'` | 钻石笔             |
| `'d'` | thin_diamond标记   |
| `'|'` | vline标记          |
| `'_'` | 标记线             |

> line(线形)

| 字符   | 描述       |
| ------ | ---------- |
| `'-'`  | 实线样式   |
| `'--'` | 虚线样式   |
| `'-.'` | 点划线样式 |
| `':'`  | 虚线样式   |

> color(颜色)

| 字符  | 颜色 |
| ----- | ---- |
| `'b'` | 蓝色 |
| `'g'` | 绿色 |
| `'r'` | 红   |
| `'c'` | 青色 |
| `'m'` | 品红 |
| `'y'` | 黄色 |
| `'k'` | 黑色 |
| `'w'` | 白色 |

如何参数中只有颜色这一选择项，则可以使用任何[`matplotlib.colors`](https://matplotlib.org/api/colors_api.html#module-matplotlib.colors)规格，例如全名（‘green')或十六进制表示('#008000')

---

#### 处理多个图形和轴

在下面这个例子中一个figure下创建了两个子图：

```python
import matplotlib.pyplot as plt
import numpy as np


def f(t):
    return np.exp(-t) * np.cos(2*np.pi*t)

t1 = np.arange(0.0, 5.0, 0.1)
t2 = np.arange(0.0, 5.0, 0.02)

plt.figure()
plt.subplot(211)  #211:   2行1列的第一个子图
plt.plot(t1, f(t1), 'bo', t2, f(t2), 'k')   #在其一子图上绘制了两个图形

plt.subplot(212)   #212:   2行1列的第二个子图
plt.plot(t2, np.cos(2*np.pi*t2), 'r--')   
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/17/32e0260e251fb0ddf0e72d5ba651fd2b.png" style="zoom:80%;margin-left:10px" />

同样：可以创建多个figure

```python
plt.figure(1)                # 第一个图形
plt.subplot(211)             # 第一个图形中的第一个子图
plt.plot([1, 2, 3])
plt.subplot(212)             # 第一个图形中的第二个子图
plt.plot([4, 5, 6])


plt.figure(2)                # 第二个图形
plt.plot([4, 5, 6])          # 默认创建一个 subplot(111)

plt.figure(1)             # 此时figure(1)仍然存在，并且此时subplot(212)是figure(1)当前使用
plt.subplot(211)          # 使得subplot(211)是figure（1）当前使用
plt.title('Easy as 1, 2, 3') # 声明subplot(211)的标题

plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/17/74788e34b8c8f82e96ad774108a9e433.png" style="zoom:80%;margin-left:10px" />

---

#### 为图形添加文字说明

[`annotate`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.annotate.html#matplotlib.pyplot.annotate)方法提供了注释方式

**参数**：xy表示注释的位置，xytext是文本的位置。这两个参数都是(x,y)元组

```python
ax = plt.subplot(111)

t = np.arange(0.0, 5.0, 0.01)
s = np.cos(2*np.pi*t)
line, = plt.plot(t, s, lw=2)

plt.annotate('local max', xy=(2, 1), xytext=(3, 1.5),
             arrowprops=dict(facecolor='black', shrink=0.05),
             )

plt.ylim(-2, 2)		#规定y值范围(-2,2)
plt.show()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/19ab7b6707f8b7acd6dce6401fc2750c.png" style="zoom:80%;margin-left:10px" />

更多详细注释请参见官方文档[基本注释](https://matplotlib.org/tutorials/text/annotations.html#annotations-tutorial)和[高级注释](https://matplotlib.org/tutorials/text/annotations.html#plotting-guide-annotation)。

<br>

---

<br>

如果你发现文章中出现的错误或者任何疑问欢迎在下方评论区评论