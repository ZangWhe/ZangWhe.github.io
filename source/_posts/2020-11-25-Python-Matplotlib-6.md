---
title: Python-Matplotlib-GridSpec等自定义图形布局
abbrlink: 59195
date: 2020-11-25 20:10:44
tags:
	- Python
	- Matplotlib
categories: Python
---

## 前言

&emsp;这篇文章主要学习如何根据GridSpec和一些其他的函数实现自定义图形布局

<!--more-->

## 使用GridSpec和其他函数自定义图形布局

&emsp; 以下函数或方法实现创建axes上的网格的组合

- [`subplots()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots) 

&emsp; 或许是创建figures和axes最主要的方式，与 [`matplotlib.pyplot.subplot()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html#matplotlib.pyplot.subplot) 类似，
但是同时创建并放置图形上的所有轴。更多详情请看[`matplotlib.figure.Figure.subplots`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.subplots).

- [`GridSpec`](https://matplotlib.org/api/_as_gen/matplotlib.gridspec.GridSpec.html#matplotlib.gridspec.GridSpec)

&emsp; 指定将放置子图的网格的几何形状。

&emsp; 需要设置网格的行数和列数。以及子图的布局参数可以调整

- [`SubplotSpec`](https://matplotlib.org/api/_as_gen/matplotlib.gridspec.SubplotSpec.html#matplotlib.gridspec.SubplotSpec)

&emsp; 在给定的GridSpec上指定子图的位置

- [`subplot2grid()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot2grid.html#matplotlib.pyplot.subplot2grid)

&emsp; 一个类似于[`subplot()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html#matplotlib.pyplot.subplot) 的辅助函数，但是使用基于0的索引并让subplot占用多个单元格。本文章没有介绍该函数。

---

### 导入

```python
import matplotlib
import matplotlib.pyplot as plt
import matplotlib.gridspec as gridspec
```

<br>

---

<br>

### 快速入门指南

> 使用[`subplots()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots)非常简单。它返回一个[`Figure`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure)实例和一个[`Axes`](https://matplotlib.org/api/axes_api.html#matplotlib.axes.Axes)对象数组 。

```python
fig1,f1_axes = plt.subplots(ncols=2,nrows=2,constrained_layout=True)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/a84efe42f06c675b465982ed43f3c331.png" style="zoom:80%;margin-left:10px" />

<br>

> 对于像上面这样的简单用例，[`gridspec`](https://matplotlib.org/api/gridspec_api.html#module-matplotlib.gridspec)可能过于冗长。
>
> 你必须分别创建图形和[`GridSpec`](https://matplotlib.org/api/_as_gen/matplotlib.gridspec.GridSpec.html#matplotlib.gridspec.GridSpec) 实例，然后将gridspec实例的元素传递给 [`add_subplot()`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_subplot) 函数来创建axes对象。
>
> gridspec元素的访问方式通常与numpy数组相同。

```python
fig2 = plt.figure(constrained_layout=True)
spec2 = gridspec.GridSpec(ncols=2,nrows=2,figure=fig2)
f2_ax1 = fig2.add_subplot(spec2[0,0])
f2_ax2 = fig2.add_subplot(spec2[0,1])
f2_ax3 = fig2.add_subplot(spec2[1,0])
f2_ax4 = fig2.add_subplot(spec2[1,1])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/c8cfe4f0d45137f5ed014a638a7a928f.png" style="zoom:80%;margin-left:10px" />

可以看出和subplots()方式结果相同

**gridspec的强大之处在于能够创建跨越行和列的子图**。注意，[NumPy slice Syntax](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html) 用于选择每个子图将占据的gridspec部分。

请注意，我们还使用了便捷方法[`Figure.add_gridspec`](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure.add_gridspec) 代替[`gridspec.GridSpec`](https://matplotlib.org/api/_as_gen/matplotlib.gridspec.GridSpec.html#matplotlib.gridspec.GridSpec)，有可能为用户节省了导入时间，并使名称空间更整洁。

```python
fig3 = plt.figure(constrained_layout=True)
gs = fig3.add_gridspec(3,3)

#关于切片可参考另一篇文章Numpy学习中的切片学习
f3_ax1 = fig3.add_subplot(gs[0,:])
f3_ax1.set_title('gs[0,:]')
f3_ax1 = fig3.add_subplot(gs[1,:-1])
f3_ax1.set_title('gs[1,:-1]')
f3_ax1 = fig3.add_subplot(gs[1:,-1])
f3_ax1.set_title('gs[1:,-1]')
f3_ax1 = fig3.add_subplot(gs[-1,0])
f3_ax1.set_title('gs[-1,0]')
f3_ax1 = fig3.add_subplot(gs[-1,-2])
f3_ax1.set_title('gs[-1,-2]')

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/1771e7f2c924222450b23f0d99d3d6de.png" style="zoom:80%;margin-left:10px" />

> 接下来展示的方法与上面的方法类似，
>
> 初始化统一的网格规范，然后使用numpy索引和切片为给定的子图分配多个“单元格”。

```python
fig4 = plt.figure(constrained_layout=True)
spec4 = fig4.add_gridspec(ncols=2,nrows=2)
anno_opts = dict(xy=(0.5,0.5),xycoords='axes fraction',va='center',ha='center')

f4_ax1 = fig4.add_subplot(spec4[0,0])
f4_ax1.annotate('GridSpec[0,0]',**anno_opts)
fig4.add_subplot(spec4[0, 1]).annotate('GridSpec[0, 1:]', **anno_opts)
fig4.add_subplot(spec4[1, 0]).annotate('GridSpec[1:, 0]', **anno_opts)
fig4.add_subplot(spec4[1, 1]).annotate('GridSpec[1:, 1:]', **anno_opts)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/03e448d6ea58673cb436c7f295203f59.png" style="zoom:80%;margin-left:10px" />



> &emsp; 另一个方式是使用width_ratios和height_ratios参数。这些关键字参数是数字列表。
>
> &emsp; 请注意，绝对值是没有意义的，只有它们的相对比率重要。这意味着width_ratio =[2, 4, 8]与width_ratio =[1, 2, 4]在同样宽的数字内相等。

```python
fig5 = plt.figure(constrained_layout=True)
widths = [2,3,1.5]
heights = [1,3,2]
spec5 = fig5.add_gridspec(ncols=3,nrows=3,width_ratios=widths,height_ratios=heights)

for row in range(3):
    for col in range(3):
        ax = fig5.add_subplot(spec5[row,col])
        label = 'Width: {}\nHeight: {}'.format(widths[col],heights[row])
        ax.annotate(label,(0.1,0.5),xycoords='axes fraction',va='center')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/41445b35cc1d0c8b71c98c482ba277cb.png" style="zoom:80%;margin-left:10px" />

> &emsp;学习使用width_ratio和height_ratio特别有用，因为函数[`subplots()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots)在gridspec_kw参数中接受它们。
>
> &emsp;为此，[`GridSpec`](https://matplotlib.org/api/_as_gen/matplotlib.gridspec.GridSpec.html#matplotlib.gridspec.GridSpec) 接受的任何参数都可以通过gridspec_kw参数传递给[`subplots()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html#matplotlib.pyplot.subplots) 。
>
> &emsp;此示例在不直接使用gridspec实例的情况下重新创建前面的图。

```python
gs_kw = dict(width_ratios=widths,height_ratios=heights)
fig6,f6_axes = plt.subplots(ncols=3,nrows=3,constrained_layout=True,gridspec_kw=gs_kw)

for r,row in enumerate(f6_axes):
    for c,ax in enumerate(row):
        label = 'Width:{}\nHeight:{}'.format(widths[c],heights[r])
        ax.annotate(label,(0.1,0.5),xycoords='axes fraction',va='center')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/b918ee705c15a77a63e27fdc6b63fc80.png" style="zoom:80%;margin-left:10px" />

> subplots和get_gridspec方法可以组合使用，因为有时使用subplots创建大多数子图，然后删除其中一些并组合它们更方便。
>
> 在这里，我们将最后一列中底部的两个轴组合起来创建一个布局。

```python
fig7,f7_axs = plt.subplots(ncols=3,nrows=3)
gs = f7_axs[1,2].get_gridspec()

#删除[1,-1],[2,-1]的axes
for ax in f7_axs[1:,-1]:
    ax.remove()
axbig = fig7.add_subplot(gs[1:,-1])    
axbig.annotate('Big Axes \nGridSpec[1:, -1]', (0.1, 0.5),
               xycoords='axes fraction', va='center')

#调整子图之间及其周围的填充。
fig7.tight_layout()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/25/fd722ff151b1ec23501358966706ccfa.png" style="zoom:80%;margin-left:10px" />