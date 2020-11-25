---
title: Python-Matplotlib-图片教程
abbrlink: 20301
date: 2020-11-25 16:54:13
tags:
---

### 图片教程

#### 导入

```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
```

---

#### 将图像数据导入到NumPy数组

这是我们要处理的图片：

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/eca78bc2a4cd3044e704e56767078adf.png" style="zoom:80%;margin-left:10px" />

让我们打开并输出它：

```python
img = mpimg.imread('C:\\Users\\wangz\\Desktop\\Pic.png') #图片路径
print(img)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/b92eba8f96442abb65015ae5862c0264.png" style="zoom:80%;margin-left:10px" />

---

#### 将NumPy数组绘制成图像

> [`imshow()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.imshow.html#matplotlib.pyplot.imshow)函数将numpy数组中的数据渲染成图像。

```python
imgplot = plt.imshow(img)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/d876abea0674df9600ae45f3e725bf76.png" style="zoom:80%;margin-left:10px" />

> 伪彩色应用于图像

伪彩色是增强对比度和更轻松地可视化数据的有用工具。

伪彩色仅与单通道，灰度，发光度图像有关。我们目前有一个RGB图像。由于R，G和B都是相似的（请参见上方或数据中的内容），我们可以选择一个数据通道：

```python
lum_img = img[:,:,0]   #数组切片，更多相关切片请看个人博客关于NumPy学习
plt.imshow(lum_img)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/f81bafc9654111311ebc0f39d0108936.png" style="zoom:80%;margin-left:10px" />

> 同样，对于亮度图像，将应用默认的颜色图（又名查找表：LUT）。默认名称为viridis,也有其他可供选择:

```python
plt.imshow(lum_img,cmap="hot")    #暖色调显示
```

![image-20201120212946492](C:\Users\wangz\AppData\Roaming\Typora\typora-user-images\image-20201120212946492.png)

> 您还可以使用[`set_cmap()`](https://matplotlib.org/api/cm_api.html#matplotlib.cm.ScalarMappable.set_cmap)方法更改现有打印对象上的颜色图

```python
imgplot = plt.imshow(lum_img)
imgplot.set_cmap('nipy_spectral')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/d14d93979e5c002dede7d045f745d30b.png" style="zoom:80%;margin-left:10px" />

> 可以通过添加颜色条来了解颜色代表什么价值，可通过matplotlib.pyplot.colorbar()函数实现

```python
imgplot = plt.imshow(lum_img)
plt.colorbar()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/dfdb2bb41d08ec8de061672881d7630f.png" style="zoom:80%;margin-left:10px" />

> 如果你想增强图像的对比度，或扩大特定区域的对比度，同时牺牲颜色变化不大或无关紧要的细节。直方图是个好工具。要创建图像数据的直方图，我们使用[`hist()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.hist.html#matplotlib.pyplot.hist)函数。

```python
plt.hist(lum_img.ravel(),bins=256,range=(0.0,1.0),fc='k',ec='k')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/add5f57e923c19a1ee1d71fafbfa2daa.png" style="zoom:80%;margin-left:10px" />

在获取图像的主要的区域[0.0，0.7]后 (如直方图所示)，

我们可以通过传递**clim参数**或者调用**set_clim()**方法修改图像对比度

```python
imgplot = plt.imshow(lum_img,clim=(0.0,0.7))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/20/d3cf83c9688e336ab13dd9ce35dd1d44.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

如果你发现文章中出现的错误或者任何疑问欢迎在下方评论区评论