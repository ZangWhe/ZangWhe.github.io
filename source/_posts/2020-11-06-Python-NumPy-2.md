---
title: Python—NumPy学习—NumPy的快速入门
date: 2020-11-06 20:54:24
tags:
	- Python
	- NumPy
categories: Python
---

## 前导

### 准备

- Python学习，具体参阅[Python教程](https://www.runoob.com/python3/python3-tutorial.html)
- 为运行示例，需安装matplotlib库，具体看文章的[上一篇](http://localhost:4000/2020/11/06/2020-11-06-Python-Numpy-1)

<!--more-->

### 学习目标

- 了解NumPy中一维数组，二维数组和n维数组之间的区别
- 了解如何在不使用for循环的情况下将一些线性代数运算应用于n维数组
- 了解n维数组的轴和形状属性



<br>

---

<br>

## 基础

### 简单介绍

> ​	NumPy的主要对象是齐次多维数组。它是由非负整数的元组索引的所有类型相同的元素（通常为数字）表。在NumPy中，维度称为*轴*。
>
> ​	例如：3D空间上的点的坐标[1,2,1]只有一个轴。该轴上有3个元素，所以我们说它的长度为3.
>
> ​	在下图所示的中，数组有2个轴：第一个轴的长度为2，第二个轴的长度为3（可以理解为2行3列的向量）

```html
[[1.,0.,0.],
[0.,1.,2.]]
```

> NumPy的数组类别称为ndarray。也被称为别名array。

> ndarray对象的重要的属性如下：

---

- ndarray.ndim

&emsp;  数组的轴(维度)数

---

- ndarray.shape

&emsp;  数组的维度。这是一个整数元组，指示每个维度中数组的大小。对于具有*n*行和*m*列的矩阵，shape将为(n,m)。因此，shape元组的长度就是轴数，ndim

---

- ndarray.size

&emsp;  数组元素的总数。这等于shape元素的乘积

---

- ndarray.dtype

&emsp;  一个对象，描述数组中元素的类型。可以使用标准Python类型创建或指定dtype。另外，NumPy提供了自己的类型。numpy.int32，numpy.int16和numpy.float64是一些示例。

---

- ndarray.itemsize

&emsp;  数组中每个元素的大小（以字节为单位）。例如，类型为float64元素的数组具有itemsize 8（= 64/8），而其中类型为complex32中的元素具有itemsize 4（= 32/8）。等同于ndarray.dtype.itemsize。

---

- ndarray.data

&emsp;  包含数组实际元素的缓冲区。通常，我们不需要使用此属性，因为我们将使用索引工具访问数组中的元素。

---

<b>举个栗子</b>

```python
import numpy as np
a = np.arange(15).reshape(3,5)
a

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/a542edd1a2cdf03f20ecd10221403853.png" style="zoom:67%;margin-left:10px" />

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/558401f8295c1e629c1e594a95627737.png" style="zoom:67%;margin-left:10px" />

<br>

---

<br>

### 数组创建

- 使用array函数


```python
import numpy as np
a = np.array([2,3,4])
a
a.dtype
```

- 常见的出错在于，错误的使用多个参数调用数组，而不是使用单个序列作为参数。例如：

```python
a = np.array(1,2,3,4)       #错误的

a = np.array([1,2,3,4])		#正确的
```

- array将[序列,序列]转换为二维数组，将[序列,序列,序列]转换为三维数组，以此类推...

```python
b = np.array([(1,2,3),(4,5,6)])		#这是一个二维数组
b
```

- 数组类型可以在创建时明确的指出

```python
c = np.array([1,2],[3,4],dtype=complex)		#指定数组的类型为complex
c
```

- Numpy的一些内置函数

```python
#zeros()    将指定维度的数组全部置0，默认数据类型为float64,可以设置参数改变类型
a = np.zeros((3,4))
print(a)
print(a.dtype)

#ones()     将指定维度的数组全部置1，默认数据类型为float64,可以设置参数改变类型
b = np.ones((2,3,4),dtype = np.int16)
print(b)
print(b.dtype)

#empty()     将指定维度的数组初始化为没有特定意义的随机值（内容是随机的并取决于内存状态的数组），默认数据类型为float64,可以设置参数改变类型

c = np.empty((2,3))
print(c)

print(c.dtype)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/971911b538013d82473498d9c1879cf2.png" style="zoom:67%;margin-left:10px" />

- 更多内置函数

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/2343a83a0e291758abfde2fa45aa224b.png" style="zoom: 80%;margin-left:10px" />



### 输出数组

- 简单介绍下输出数组时的规则：
  - 最后一个轴从左到右打印，
  - 倒数第二个从上到下打印，
  - 其余的也从上到下打印，每个切片之间用空行隔开。

- 如果数组太大无法打印，那么Numpy会自动跳过数组的中心部分，仅输出边角点

```python
print(np.arange(10000))

print(np.arange(10000).reshape(100,100))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/b3ae52faedd5790ce7e094ee3887911e.png" style="zoom:67%;margin-left:10px" />

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/b2a2d70bdeda36579eab88eacaf75b0a.png" style="zoom:67%;margin-left:10px" />

- 要禁用此行为并强制NumPy打印整个数组，可以使用更改打印选项`set_printoptions`。

```python
import sys
np.set_printoptions(threshold=sys.maxsize)       # 需要导入sys库
print(np.arange(10000).reshape(100,100))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/cbc59855fe68040bb6606668480b0c75.png" style="zoom:80%;margin-left:10px" />

