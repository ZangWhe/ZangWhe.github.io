---
title: Python-NumPy基础
tags:
  - Python
  - NumPy
categories: Python
abbrlink: 38267
date: 2020-11-06 20:54:24
---





## 前导

### 准备

- NumPy的安装准备工作在上篇文章中，[点此跳转](https://zangwhe.cn/46594.html#more)

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

> NumPy的数组类别称为ndarray。
>
> ndarray 对象是用于存放同类型元素的多维数组。
>
> ndarray 中的每个元素在内存中都有相同存储大小的区域。

> 创建一个ndarray只需调用Numpy的array函数即可：
>
> ```python
> numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
> ```
>
> **参数说明：**
>
> | 名称   | 描述                                                      |
> | :----- | :-------------------------------------------------------- |
> | object | 数组或嵌套的数列                                          |
> | dtype  | 数组元素的数据类型，可选                                  |
> | copy   | 对象是否需要复制，可选                                    |
> | order  | 创建数组的样式，C为行方向，F为列方向，A为任意方向（默认） |
> | subok  | 默认返回一个与基类类型一致的数组                          |
> | ndmin  | 指定生成数组的最小维度                                    |

> ndarray对象的重要的属性如下：


- ndarray.ndim

&emsp;  数组的轴(维度)数


- ndarray.shape

&emsp;  数组的维度。这是一个整数元组，指示每个维度中数组的大小。对于具有*n*行和*m*列的矩阵，shape将为(n,m)。因此，shape元组的长度就是轴数，ndim


- ndarray.size

&emsp;  数组元素的总数。这等于shape元素的乘积


- ndarray.dtype

&emsp;  一个对象，描述数组中元素的类型。可以使用标准Python类型创建或指定dtype。另外，NumPy提供了自己的类型。numpy.int32，numpy.int16和numpy.float64是一些示例。


- ndarray.itemsize

&emsp;  数组中每个元素的大小（以字节为单位）。例如，类型为float64元素的数组具有itemsize 8（= 64/8），而其中类型为complex32中的元素具有itemsize 4（= 32/8）。等同于ndarray.dtype.itemsize。


- ndarray.data

&emsp;  包含数组实际元素的缓冲区。通常，我们不需要使用此属性，因为我们将使用索引工具访问数组中的元素。


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

[`array`](https://numpy.org/devdocs/reference/generated/numpy.array.html#numpy.array)， [`zeros`](https://numpy.org/devdocs/reference/generated/numpy.zeros.html#numpy.zeros)， [`zeros_like`](https://numpy.org/devdocs/reference/generated/numpy.zeros_like.html#numpy.zeros_like)， [`ones`](https://numpy.org/devdocs/reference/generated/numpy.ones.html#numpy.ones)， [`ones_like`](https://numpy.org/devdocs/reference/generated/numpy.ones_like.html#numpy.ones_like)， [`empty`](https://numpy.org/devdocs/reference/generated/numpy.empty.html#numpy.empty)， [`empty_like`](https://numpy.org/devdocs/reference/generated/numpy.empty_like.html#numpy.empty_like)， [`arange`](https://numpy.org/devdocs/reference/generated/numpy.arange.html#numpy.arange)， [`linspace`](https://numpy.org/devdocs/reference/generated/numpy.linspace.html#numpy.linspace)， [`numpy.random.Generator.rand`](https://docs.scipy.org/doc/numpy-1.15.1/reference/generated/numpy.random.rand.html)， [`numpy.random.Generator.randn`](https://docs.scipy.org/doc/numpy-1.15.1/reference/generated/numpy.random.randn.html)， [`fromfunction`](https://numpy.org/devdocs/reference/generated/numpy.fromfunction.html#numpy.fromfunction)， [`fromfile`](https://numpy.org/devdocs/reference/generated/numpy.fromfile.html#numpy.fromfile)

<br>

<hr>

<br>



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

<br>

---

<br>

### 基本运算

---

> 算术运算同样也适用于数组运算

```python
import numpy as np
a = np.array([20,30,40,50])

b = np.arange(4)
b
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/db3935a40f93455d6e2cd269f25c0f87.png" style="zoom: 80%;margin-left:10px" />

```python
c = a - b
c
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/4f8bbd06fabba5f25ce337035624c8b3.png" style="zoom:80%;margin-left:10px" />

```python
10*np.sin(a)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/585e9c7f57c3cdf04409277756f4fc27.png" style="zoom:80%;margin-left:10px" />

```python
a<35
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/91de52e58a9b1877c8eda6e6bc95d656.png" style="zoom:80%;margin-left:10px" />

---

> 与许多矩阵语言不同，乘积运算符*在NumPy中是按元素及进行操作。
>
> 在NumPy中可以使用@运算符（Python版本>=3.5）或用dot函数执行矩阵乘积

```python
A = np.array([[1,1],[0,1]])

B = np.array([[2,0],[3,4]])

```

```python
A*B
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/343061de563e938f62d9fcca8bffb351.png" style="zoom: 80%;margin-left:10px" />

```python
A@B
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/3971d4064549d5314abf173bafba4d83.png" style="zoom:80%;margin-left:10px" />

```python
A.dot(B)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/67a5858aae02ea9438a91887f6b8a009.png" style="zoom:80%;margin-left:10px" />

---

> 某些操作（如+=和*=）,是修改现有数组，而不是创建一个新数组

```python
rg = np.random.default_rng(1)     # 创建默认的随机数生成的示例
a = np.ones((2,3), dtype=int)     # Int类型的全1向量
b = rg.random((2,3))              #  默认为浮点数
a *= 3
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/516ff0af648025713ea836af2ad01c4a.png" style="zoom:80%;margin-left:10px" />

```python
b += a
b
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/b821f22eeac6db5334b69c0701fd6b9d.png" style="zoom:80%;margin-left:10px" />

```python
a += b        #浮点类型数组b不会自动转换为整型
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/78d0b526cce977042378983a39fce759.png" style="zoom:80%;" />

> 当使用不同类型的数组进行操作时，结果数组的类型对应于更通用或更精确的数组（一种称为向上转换的行为）。
>
> 类似于上述案例中int类型数组a可以向上转型为float类型
>
> 而float类型的数组b却不能转型为数组int类型a

---

> 许多一元运算（例如求和）都作为ndarray该类的方法实现

```python
a = rg.random((2,3))
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/8a6df5eb3fef72f08cde5d3b97a5c851.png" style="zoom:80%;margin-left:10px" />

```python
a.sum()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/efaeaf7840f47275e1e3abcc08177723.png" style="zoom:80%;margin-left:10px" />

```python
a.min()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/0562bd71b184abf88966277f227a4062.png" style="zoom:80%;margin-left:10px" />

```python
a.max()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/fd88d8a177dc2d643944647a171b0c14.png" style="zoom:80%;margin-left:10px" />

---

> 默认情况下，这些操作适用于数组，就好像它是数字列表一样，而不管其形状如何。但是，通过指定`axis` 参数，您可以沿数组的指定轴应用操作(通常axis=0表示指定列，axis=1指定行)

```python
b = np.arange(12).reshape(3,4)
b
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/65b63ee93d1e8dcd0409020b72628a1f.png" style="zoom:80%;margin-left:10px" />

```python
b.sum(axis=0)      #求每一列的和
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/755b37dab87ba9c4253472aade23a4cf.png" style="zoom:80%;margin-left:10px" />

```python
b.min(axis=1)      #求每一行的最小值
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/87eb1b5ba3305fd101cd6c82e44f33b8.png" style="zoom:80%;margin-left:10px" />

```python
b.cumsum(axis=1)      #每一行的累积和
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/8f0da952857e812f34fd53188cc7033b.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

### 通用函数

> ​	NumPy提供了熟悉的数学函数，例如sin，cos和exp。在NumPy中，这些被称为“通用函数”（`ufunc`）。在NumPy中，这些函数在数组上逐个元素操作，生成数组作为输出。

```python
B = np.arange(3)
B
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/803deb50a6102fa542033a3f28ef041a.png" style="zoom:80%;margin-left:10px" />

```python
np.exp(B)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/3aa764ff8c3a0ed75fdf1204def3c2ba.png" style="zoom:80%;margin-left:10px" />

```python
np.sqrt(B)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/907c3f34707eafa4f1487ca09be1d46f.png" style="zoom:80%;margin-left:10px" />

```python
C = np.array([2.,-1.,4.])
np.add(B,C)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/21703f05154f963ac7c3eaa9b80002b8.png" style="zoom:80%;margin-left:10px" />



> 更多函数

[`all`](https://numpy.org/devdocs/reference/generated/numpy.all.html#numpy.all)， [`any`](https://numpy.org/devdocs/reference/generated/numpy.any.html#numpy.any)， [`apply_along_axis`](https://numpy.org/devdocs/reference/generated/numpy.apply_along_axis.html#numpy.apply_along_axis)， [`argmax`](https://numpy.org/devdocs/reference/generated/numpy.argmax.html#numpy.argmax)， [`argmin`](https://numpy.org/devdocs/reference/generated/numpy.argmin.html#numpy.argmin)， [`argsort`](https://numpy.org/devdocs/reference/generated/numpy.argsort.html#numpy.argsort)， [`average`](https://numpy.org/devdocs/reference/generated/numpy.average.html#numpy.average)， [`bincount`](https://numpy.org/devdocs/reference/generated/numpy.bincount.html#numpy.bincount)， [`ceil`](https://numpy.org/devdocs/reference/generated/numpy.ceil.html#numpy.ceil)， [`clip`](https://numpy.org/devdocs/reference/generated/numpy.clip.html#numpy.clip)， [`conj`](https://numpy.org/devdocs/reference/generated/numpy.conj.html#numpy.conj)， [`corrcoef`](https://numpy.org/devdocs/reference/generated/numpy.corrcoef.html#numpy.corrcoef)， [`cov`](https://numpy.org/devdocs/reference/generated/numpy.cov.html#numpy.cov)， [`cross`](https://numpy.org/devdocs/reference/generated/numpy.cross.html#numpy.cross)， [`cumprod`](https://numpy.org/devdocs/reference/generated/numpy.cumprod.html#numpy.cumprod)， [`cumsum`](https://numpy.org/devdocs/reference/generated/numpy.cumsum.html#numpy.cumsum)， [`diff`](https://numpy.org/devdocs/reference/generated/numpy.diff.html#numpy.diff)， [`dot`](https://numpy.org/devdocs/reference/generated/numpy.dot.html#numpy.dot)， [`floor`](https://numpy.org/devdocs/reference/generated/numpy.floor.html#numpy.floor)， [`inner`](https://numpy.org/devdocs/reference/generated/numpy.inner.html#numpy.inner)， [`invert`](https://numpy.org/devdocs/reference/generated/numpy.invert.html#numpy.invert)， [`lexsort`](https://numpy.org/devdocs/reference/generated/numpy.lexsort.html#numpy.lexsort)， [`max`](https://docs.python.org/dev/library/functions.html#max)， [`maximum`](https://numpy.org/devdocs/reference/generated/numpy.maximum.html#numpy.maximum)， [`mean`](https://numpy.org/devdocs/reference/generated/numpy.mean.html#numpy.mean)， [`median`](https://numpy.org/devdocs/reference/generated/numpy.median.html#numpy.median)， [`min`](https://docs.python.org/dev/library/functions.html#min)， [`minimum`](https://numpy.org/devdocs/reference/generated/numpy.minimum.html#numpy.minimum)， [`nonzero`](https://numpy.org/devdocs/reference/generated/numpy.nonzero.html#numpy.nonzero)， [`outer`](https://numpy.org/devdocs/reference/generated/numpy.outer.html#numpy.outer)， [`prod`](https://numpy.org/devdocs/reference/generated/numpy.prod.html#numpy.prod)， [`re`](https://docs.python.org/dev/library/re.html#module-re)， [`round`](https://docs.python.org/dev/library/functions.html#round)， [`sort`](https://numpy.org/devdocs/reference/generated/numpy.sort.html#numpy.sort)， [`std`](https://numpy.org/devdocs/reference/generated/numpy.std.html#numpy.std)， [`sum`](https://numpy.org/devdocs/reference/generated/numpy.sum.html#numpy.sum)， [`trace`](https://numpy.org/devdocs/reference/generated/numpy.trace.html#numpy.trace)， [`transpose`](https://numpy.org/devdocs/reference/generated/numpy.transpose.html#numpy.transpose)， [`var`](https://numpy.org/devdocs/reference/generated/numpy.var.html#numpy.var)， [`vdot`](https://numpy.org/devdocs/reference/generated/numpy.vdot.html#numpy.vdot)， [`vectorize`](https://numpy.org/devdocs/reference/generated/numpy.vectorize.html#numpy.vectorize)， [`where`](https://numpy.org/devdocs/reference/generated/numpy.where.html#numpy.where)

<br>

---

<br>

### 索引，切片和迭代

> 一维数组可以被索引，切片和迭代，就像列表和其他Python序列一样

```python
#索引
a = np.arange(10)**3         #幂运算
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/6a09b37ce2cb47f175ce32bbb0b80a11.png" style="zoom:80%;margin-left:10px" />

```python
#切片
a[2:5]      #区间为[2,5)  ,  左闭右开
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/b730edb7ecf808a1408048323cc87855.png" style="zoom:80%;margin-left:10px" />

```python
#切片
#array[pos1:pos2:step] = val  指从pos1到pos2-1，没隔两个元素设置为val
#例如：
#  a
# array([  0,   1,   8,  27,  64, 125, 216, 343, 512, 729], dtype=int32)
a[:6:2] = 1000              #相当于a[0:6:2]    区间[0,6)     左闭右开
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/5bf4888a2666c55389dcddf6ebbd6ead.png" style="zoom:80%;margin-left:10px" />

```python
a[::-1]         #逆转数组
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/79dd38a84e95a9bf2f97c3b702a9845f.png" style="zoom:80%;margin-left:10px" />

```python
#遍历迭代
for i in a:
    print(i**2)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/444fd38b8965664143f1d043a318ddda.png" style="zoom:80%;margin-left:10px" />

> 多维数组每个轴可以有一个索引。这些索引以元组给出，并用逗号分割

```python
def f(x,y):
    return 10*x+y
b = np.fromfunction(f,(5,4),dtype=int)     #调用f函数，生成5行4列的数组，参数是数组的下标，类型为Int
b
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/4183eafbaa704890018f8f10e5b3a0d7.png" style="zoom:80%;margin-left:10px" />

```python
b[2,3]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/31c4199dc9b0883ece4363d75190fe12.png" style="zoom:80%;margin-left:10px" />

```python
b[0:5,1]        #每行的下标为1的值
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/061bb8da4750dabdf1b6e32a2993c4f4.png" style="zoom:80%;margin-left:10px" />

```python
b[:,1]          #等效与上面这个案例
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/197cd332025f9996743ffbb5f82a9c14.png" style="zoom:80%;margin-left:10px" />

```python
b[1:3,:]        #输出第2行和第三行的每一列
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/2381952b534226d5b6fcfcfbedbb81ac.png" style="zoom:80%;margin-left:10px" />

> 如果提供的索引数少于轴数，则丢失的索引数将视为完整切片`:`

```python
b[-1]            #未指明列的分片情况，则视为每一列，等效于b[-1,:]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/6ad08b5358d235027b36a911650a3a7b.png" style="zoom:80%;margin-left:10px" />

> 括号中的表达式b[i]被视为i 后跟:表示所需数量的剩余轴实例。
>
> NumPy还允许您使用**点**写为 b[i,...]。
>
> 点（...)表示为许多冒号，根据需要，以产生一个完整的索引元组。
>
> 例如，如果x是具有5个轴的数组，则
>
> - x[1,2,...]等于x[1,2,:,:,:]，
> - x[...,3]到x[:,:,:,:,3]和
> - x[4,...,5,:]到x[4,:,:,5,:]。

```python
c = np.array( [[[  0,  1,  2],               # 三维数组
                [ 10, 12, 13]],
                [[100,101,102],
                 [110,112,113]]])
c.shape
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/b0920364a02391f4632c46f6b4496a50.png" style="zoom:80%;margin-left:10px" />

```python
c[1,...]      
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/95cfd942c5bb0255e75ce8516e8c5219.png" style="zoom:80%;margin-left:10px" />

```python
c[...,2]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/5344d3fd679837641253593efee1137e.png" style="zoom:80%;margin-left:10px" />

> 迭代过多维数组相对于第一轴线完成

```python
# b
# array([[ 0,  1,  2,  3],
#        [10, 11, 12, 13],
#        [20, 21, 22, 23],
#        [30, 31, 32, 33],
#        [40, 41, 42, 43]])
for row in b:
    print(row)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/7c6edd2253bc5349d2b6114314927cd9.png" style="margin-left: 10px;" />

> 但是，如果要对数组中的每个元素执行操作，则可以使用`flat`属性，该属性是 数组中所有元素的 [迭代器](https://docs.python.org/tutorial/classes.html#iterators)：

```python
for element in b.flat:
    print(element)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/70099fd7f54d4e2c1ac3f7f26d6e07ba.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

## 操纵形状

### 改变数组的形状

>  数组的形状是由沿每个轴的元素数确定

```python
a = np.floor(10*rg.random((3,4)))       #np.floor 是将浮点数向下取整
print(a)
print(a.shape,a.dtype)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/6ffc8e3031d27030bb178049b71544e4.png" style="zoom:80%;margin-left:10px" />

> 数组的形状可以使用各种命令来更改。
>
> 请注意，以下三个命令均返回修改后的数组，但不更改原始数组：

```python
a.ravel()			#返回一个一维数组
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/262123547e78674f584763db174db621.png" style="zoom:80%;margin-left:10px" />

```python
a.reshape(6,2)        #改变数组a为6行2列
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/162ff7a441e98370639204e7dfd67580.png" style="zoom:80%;margin-left:10px" />

```python
a.T     #a的转置
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/44053a91c9f2710a848d3b779811b256.png" style="zoom:80%;margin-left:10px" />

>  [`ndarray.resize`](https://numpy.org/devdocs/reference/generated/numpy.ndarray.resize.html#numpy.ndarray.resize)方法修改了数组本身：

```python
#a修改前：
#array([[9., 7., 5., 2.],
#       [1., 9., 5., 1.],
#       [6., 7., 6., 9.]])
a.resize((2,6))
a
#a修改后：
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/1767ff1b687f12efc9145f56235c1922.png" style="zoom:80%;margin-left:10px" />

> 如果在改变形状时将维度改为-1，则会自动计算其他尺寸：

```python
a.reshape(3,-1)      #指定转换为3行，系统自动计算列数
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/739c516495e44d0b896f9ff7977ce347.png" style="zoom:80%;margin-left:10px" />

> 更多函数：

[`ndarray.shape`](https://numpy.org/devdocs/reference/generated/numpy.ndarray.shape.html#numpy.ndarray.shape)， [`reshape`](https://numpy.org/devdocs/reference/generated/numpy.reshape.html#numpy.reshape)， [`resize`](https://numpy.org/devdocs/reference/generated/numpy.resize.html#numpy.resize)， [`ravel`](https://numpy.org/devdocs/reference/generated/numpy.ravel.html#numpy.ravel)

---

### 堆叠在一起的不同数组

> 几个数组可以沿不同的轴堆叠在一起：

```python
a = np.floor(10*rg.random((2,2)))
print('a=','\n',a)
b = np.floor(10*rg.random((2,2)))
print('b=','\n',b)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/91cb0e1a10dfba3c60aeea349b26cdfc.png" style="zoom:80%;margin-left:10px" />

```python
np.vstack((a,b))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/769aad475ee9a5cc9d29b850d1902cb4.png" style="zoom:80%;margin-left:10px" />

```python
np.hstack((a,b))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/3993710b53facabb2878c2a7bfc90c98.png" style="zoom:80%;margin-left:10px" />

> 函数column_stack将1维数组作为列向量堆叠成2维数组
>
> 只有当作用与2维数组时是与hstack是等效的

```python
from numpy import newaxis
np.column_stack((a,b))			#结果等效于上个案例中np.hstack((a,b))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/5fd9d502b50bdcd24370dd50966872e2.png" style="zoom:80%;margin-left:10px" />

```python
a = np.array([4.,2.])
b = np.array([3.,8.])
print(np.column_stack((a,b)),'\n')
print(np.hstack((a,b)))               #两并不相同
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/6341dee82ba4c3e8b2e144b01e88bff1.png" style="zoom:80%;margin-left:10px" />

```python
a[:,newaxis]         #将a视为一个二维数组，newaxis字面意思就是新的轴
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/6cd334fc142debce12d23dbef11d29de.png" style="zoom:80%;margin-left:10px" />

```python
c = np.array([[1,2],[3,4]])
c[:,:,newaxis]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/7b3b95dd93885b8281aefc513ba6ed2f.png" style="zoom:80%;margin-left:10px" />

```python
np.column_stack((a[:,newaxis],b[:,newaxis]))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/900a99f3761a4d3352addebbd5f2d5f0.png" style="zoom:80%;margin-left:10px" />

```python
np.hstack((a[:,newaxis],b[:,newaxis]))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/214a034ca229213f661939af882a8b2d.png" style="zoom:80%;margin-left:10px" />



> 另外，无论输入数组是怎样的，函数row_stack都等效于函数vstack。
>
> 实际上，row_stack别名是vstack

```python
print(np.column_stack is np.hstack)
print(np.row_stack is np.vstack)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/df0c18e3ad87169f1e36a53ca4817932.png" style="zoom:80%;margin-left:10px" />

> 通常，对于二维以上（不包括二维）的数组，hstack沿着他们的第二个轴堆叠，vstack沿着他们的第一个轴堆叠

```python
a = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])
b = np.array([[[9,10],[11,12]],[[13,14],[15,16]]])
print(a.shape)
print(np.hstack((a,b)).shape)
np.hstack((a,b))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/25bcd2fe7ef7621b1f7ad8d63232af4b.png" style="zoom:80%;margin-left:10px" />

```python
a = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])
b = np.array([[[9,10],[11,12]],[[13,14],[15,16]]])
print(a.shape)
print(np.vstack((a,b)).shape)
np.vstack((a,b))

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/c4ad8e4fc784ab7a2640cae912c387d1.png" style="zoom:80%;margin-left:10px" />

> 注意
> 在复杂情况下，r_ 和 c_ 杜宇通过一个轴将数字叠加创建数组时很有用。
>
> 他们允许使用（“:”）

```python
np.r_[1:9,1,2,3]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/a8836a2ed1ff752d6205e153fda94d9f.png" style="zoom:80%;margin-left:10px" />

```python
np.c_[np.array([1,2,3]), np.array([4,5,6])]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/45621ae059174b4d8a0def016dd80212.png" style="zoom:80%;margin-left:10px" />

> ​	当使用数组作为参数时，r_和c_在默认行为上类似于vstack和hstack，但是允许一个可选参数给出要连接的轴的编号。

> More Information

[`hstack`](https://numpy.org/devdocs/reference/generated/numpy.hstack.html#numpy.hstack), [`vstack`](https://numpy.org/devdocs/reference/generated/numpy.vstack.html#numpy.vstack), [`column_stack`](https://numpy.org/devdocs/reference/generated/numpy.column_stack.html#numpy.column_stack), [`concatenate`](https://numpy.org/devdocs/reference/generated/numpy.concatenate.html#numpy.concatenate), [`c_`](https://numpy.org/devdocs/reference/generated/numpy.c_.html#numpy.c_), [`r_`](https://numpy.org/devdocs/reference/generated/numpy.r_.html#numpy.r_)

---

### 将一个数组拆分为几个较小的数组

> 使用[`hsplit`](https://numpy.org/devdocs/reference/generated/numpy.hsplit.html#numpy.hsplit)，您可以沿数组的水平轴拆分数组
>
> 方法是指定要返回的形状相同的数组的数量，或者指定要在其后进行划分的列

```python
a = np.floor(10*rg.random((2,12)))
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/2ceb31c38db0192e1fe45a8e1c32bde8.png" style="zoom:80%;margin-left:10px" />

```python
np.hsplit(a,3)        #一分为三
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/fcb1596c2ed0b48fbf0184c24f3df9c0.png" style="zoom:80%;margin-left:10px" />

```python
np.hsplit(a,(3,4))      #分别在第三列和第四列后分离
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/7292f59501c9dd0b7d7ad1c78b4a0361.png" style="zoom:80%;margin-left:10px" />

> vsplit沿着垂直的轴拆分分
>
> 并且array_split循序指定沿着哪个轴拆分

<br>

---

<br>

## 副本和视图

> ​	副本是一个数据的完整的拷贝，如果我们对副本进行修改，它不会影响到原始数据，物理内存不在同一位置。
>
> ​	视图是数据的一个别称或引用，通过该别称或引用亦便可访问、操作原有数据，但原有数据不会产生拷贝。如果我们对视图进行修改，它会影响到原始数据，物理内存在同一位置。



> 在操作数组时，有时会将其数据复制到新数组中，有时不复制。
>
> 对于初学者来说，这通常会引起混乱。
>
> 有以下三种情况:无复制、视图或浅复制、副本或深复制

### 无复制

> 简单分配不会复制对象或其数据

```python
a = np.array([[ 0,  1,  2,  3],
              [ 4,  5,  6,  7],
              [ 8,  9, 10, 11]])

b = a        #没有创建新的对象
b is a       #简单理解为a,b都指向了同一片区域，a、b只是ndarray对象的两个不同名字而已
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/36c66acb94653e78a2edecfb51037d2e.png" style="zoom:80%;margin-left:10px" />

> Python将可变对象作为引用传递，因此函数调用不会复制。

```python
def f(x):
    print(id(x))
id(a)               #id是一个对象的唯一的标识符
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/b09ac3e2993da9d38c8146ef52917d20.png" style="zoom:80%;margin-left:10px" />

```python
f(a)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/5a4c05fc972b618b984ddf5753facd44.png" style="zoom:80%;margin-left:10px" />

---

### 视图或浅复制

> 不同的数组对象可以共享相同的数据。`view`方法创建一个具有相同数据的新数组对象。

```python
# a
# a = np.array([[ 0,  1,  2,  3],
#               [ 4,  5,  6,  7],
#               [ 8,  9, 10, 11]])
c = a.view()
c
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/d0a6521ba9ce7318b9aa6eefd2285cbb.png" style="zoom:80%;margin-left:10px" />

```python
c is a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/0a301503c603565f81e2f1a9966171b9.png" style="zoom:80%;margin-left:10px" />

```python
c.base is a       #c与a具有相同的视图
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/fc5c11812e37a11eb34f665557cf59e9.png" style="zoom:80%;margin-left:10px" />

```python
c = c.reshape((2,6))
a.shape                      #修改c的形状并不能改变a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/c2fc87fd9e4a3b8dafa7cce924917dc8.png" style="zoom:80%;margin-left:10px" />

```python
c[0,4] = 1024
a                   #修改c中的某个值可以修改a   
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/8a399918bae41a6dd4cafa5a24d94d7e.png" style="zoom:80%;margin-left:10px" />

```python
s = a[ : ,1:3]      
s[:] = 10         #s[:]是s对象的view,s与s[:]有区别，请注意
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/1d0afd1dc2cd44f62d159468876d5251.png" style="zoom:80%;margin-left:10px" />

---

### 副本或深复制

> copy方法对数组及其数据进行完整复制

```python
d = a.copy()            #相当于新建了一个带有新数据的新数组
print(d is a)
print(d.base is a)      # d与a不共享任何事情 
d[0,0]=99999
print(a)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/992536b54cd59e1fb6950b2477fa4f0b.png" style="zoom:80%;margin-left:10px" />

> 如果不再需要原始数组，有时应该在切片后调用复制。
>
> 例如，假设a是一个巨大的中间结果，最终结果b只包含a的一小部分，那么在使用切片构造b时需要做一个深度复制:

```python
a = np.arange(int(1e8))
b = a[:100].copy()
del a  # a的内存可以被释放
```

> 如果使用b = a[:100]，则a被b引用，即使del a被执行，a也会存在内存中。



### 函数和方法概述

- 数组创建

  [`arange`](https://numpy.org/devdocs/reference/generated/numpy.arange.html#numpy.arange)， [`array`](https://numpy.org/devdocs/reference/generated/numpy.array.html#numpy.array)， [`copy`](https://numpy.org/devdocs/reference/generated/numpy.copy.html#numpy.copy)， [`empty`](https://numpy.org/devdocs/reference/generated/numpy.empty.html#numpy.empty)， [`empty_like`](https://numpy.org/devdocs/reference/generated/numpy.empty_like.html#numpy.empty_like)， [`eye`](https://numpy.org/devdocs/reference/generated/numpy.eye.html#numpy.eye)， [`fromfile`](https://numpy.org/devdocs/reference/generated/numpy.fromfile.html#numpy.fromfile)， [`fromfunction`](https://numpy.org/devdocs/reference/generated/numpy.fromfunction.html#numpy.fromfunction)， [`identity`](https://numpy.org/devdocs/reference/generated/numpy.identity.html#numpy.identity)， [`linspace`](https://numpy.org/devdocs/reference/generated/numpy.linspace.html#numpy.linspace)， [`logspace`](https://numpy.org/devdocs/reference/generated/numpy.logspace.html#numpy.logspace)， [`mgrid`](https://numpy.org/devdocs/reference/generated/numpy.mgrid.html#numpy.mgrid)， [`ogrid`](https://numpy.org/devdocs/reference/generated/numpy.ogrid.html#numpy.ogrid)， [`ones`](https://numpy.org/devdocs/reference/generated/numpy.ones.html#numpy.ones)， [`ones_like`](https://numpy.org/devdocs/reference/generated/numpy.ones_like.html#numpy.ones_like)， [`r_`](https://numpy.org/devdocs/reference/generated/numpy.r_.html#numpy.r_)， [`zeros`](https://numpy.org/devdocs/reference/generated/numpy.zeros.html#numpy.zeros)， [`zeros_like`](https://numpy.org/devdocs/reference/generated/numpy.zeros_like.html#numpy.zeros_like)

- 转换

  [`ndarray.astype`](https://numpy.org/devdocs/reference/generated/numpy.ndarray.astype.html#numpy.ndarray.astype)， [`atleast_1d`](https://numpy.org/devdocs/reference/generated/numpy.atleast_1d.html#numpy.atleast_1d)， [`atleast_2d`](https://numpy.org/devdocs/reference/generated/numpy.atleast_2d.html#numpy.atleast_2d)， [`atleast_3d`](https://numpy.org/devdocs/reference/generated/numpy.atleast_3d.html#numpy.atleast_3d)， [`mat`](https://numpy.org/devdocs/reference/generated/numpy.mat.html#numpy.mat)

- 操作方式

  [`array_split`](https://numpy.org/devdocs/reference/generated/numpy.array_split.html#numpy.array_split)， [`column_stack`](https://numpy.org/devdocs/reference/generated/numpy.column_stack.html#numpy.column_stack)， [`concatenate`](https://numpy.org/devdocs/reference/generated/numpy.concatenate.html#numpy.concatenate)， [`diagonal`](https://numpy.org/devdocs/reference/generated/numpy.diagonal.html#numpy.diagonal)， [`dsplit`](https://numpy.org/devdocs/reference/generated/numpy.dsplit.html#numpy.dsplit)， [`dstack`](https://numpy.org/devdocs/reference/generated/numpy.dstack.html#numpy.dstack)， [`hsplit`](https://numpy.org/devdocs/reference/generated/numpy.hsplit.html#numpy.hsplit)， [`hstack`](https://numpy.org/devdocs/reference/generated/numpy.hstack.html#numpy.hstack)， [`ndarray.item`](https://numpy.org/devdocs/reference/generated/numpy.ndarray.item.html#numpy.ndarray.item)， [`newaxis`](https://numpy.org/devdocs/reference/constants.html#numpy.newaxis)， [`ravel`](https://numpy.org/devdocs/reference/generated/numpy.ravel.html#numpy.ravel)， [`repeat`](https://numpy.org/devdocs/reference/generated/numpy.repeat.html#numpy.repeat)， [`reshape`](https://numpy.org/devdocs/reference/generated/numpy.reshape.html#numpy.reshape)， [`resize`](https://numpy.org/devdocs/reference/generated/numpy.resize.html#numpy.resize)， [`squeeze`](https://numpy.org/devdocs/reference/generated/numpy.squeeze.html#numpy.squeeze)， [`swapaxes`](https://numpy.org/devdocs/reference/generated/numpy.swapaxes.html#numpy.swapaxes)， [`take`](https://numpy.org/devdocs/reference/generated/numpy.take.html#numpy.take)， [`transpose`](https://numpy.org/devdocs/reference/generated/numpy.transpose.html#numpy.transpose)， [`vsplit`](https://numpy.org/devdocs/reference/generated/numpy.vsplit.html#numpy.vsplit)， [`vstack`](https://numpy.org/devdocs/reference/generated/numpy.vstack.html#numpy.vstack)

- 问题

  [`all`](https://numpy.org/devdocs/reference/generated/numpy.all.html#numpy.all)， [`any`](https://numpy.org/devdocs/reference/generated/numpy.any.html#numpy.any)， [`nonzero`](https://numpy.org/devdocs/reference/generated/numpy.nonzero.html#numpy.nonzero)， [`where`](https://numpy.org/devdocs/reference/generated/numpy.where.html#numpy.where)

- 组合排列排序

  [`argmax`](https://numpy.org/devdocs/reference/generated/numpy.argmax.html#numpy.argmax)， [`argmin`](https://numpy.org/devdocs/reference/generated/numpy.argmin.html#numpy.argmin)， [`argsort`](https://numpy.org/devdocs/reference/generated/numpy.argsort.html#numpy.argsort)， [`max`](https://docs.python.org/dev/library/functions.html#max)， [`min`](https://docs.python.org/dev/library/functions.html#min)， [`ptp`](https://numpy.org/devdocs/reference/generated/numpy.ptp.html#numpy.ptp)， [`searchsorted`](https://numpy.org/devdocs/reference/generated/numpy.searchsorted.html#numpy.searchsorted)， [`sort`](https://numpy.org/devdocs/reference/generated/numpy.sort.html#numpy.sort)

- 运作方式

  [`choose`](https://numpy.org/devdocs/reference/generated/numpy.choose.html#numpy.choose)， [`compress`](https://numpy.org/devdocs/reference/generated/numpy.compress.html#numpy.compress)， [`cumprod`](https://numpy.org/devdocs/reference/generated/numpy.cumprod.html#numpy.cumprod)， [`cumsum`](https://numpy.org/devdocs/reference/generated/numpy.cumsum.html#numpy.cumsum)， [`inner`](https://numpy.org/devdocs/reference/generated/numpy.inner.html#numpy.inner)， [`ndarray.fill`](https://numpy.org/devdocs/reference/generated/numpy.ndarray.fill.html#numpy.ndarray.fill)， [`imag`](https://numpy.org/devdocs/reference/generated/numpy.imag.html#numpy.imag)， [`prod`](https://numpy.org/devdocs/reference/generated/numpy.prod.html#numpy.prod)， [`put`](https://numpy.org/devdocs/reference/generated/numpy.put.html#numpy.put)， [`putmask`](https://numpy.org/devdocs/reference/generated/numpy.putmask.html#numpy.putmask)， [`real`](https://numpy.org/devdocs/reference/generated/numpy.real.html#numpy.real)， [`sum`](https://numpy.org/devdocs/reference/generated/numpy.sum.html#numpy.sum)

- 基本统计

  [`cov`](https://numpy.org/devdocs/reference/generated/numpy.cov.html#numpy.cov)， [`mean`](https://numpy.org/devdocs/reference/generated/numpy.mean.html#numpy.mean)， [`std`](https://numpy.org/devdocs/reference/generated/numpy.std.html#numpy.std)， [`var`](https://numpy.org/devdocs/reference/generated/numpy.var.html#numpy.var)

- 基本线性代数

  [`cross`](https://numpy.org/devdocs/reference/generated/numpy.cross.html#numpy.cross)， [`dot`](https://numpy.org/devdocs/reference/generated/numpy.dot.html#numpy.dot)， [`outer`](https://numpy.org/devdocs/reference/generated/numpy.outer.html#numpy.outer)， [`linalg.svd`](https://numpy.org/devdocs/reference/generated/numpy.linalg.svd.html#numpy.linalg.svd)， [`vdot`](https://numpy.org/devdocs/reference/generated/numpy.vdot.html#numpy.vdot)

<br>

---

<br>

## 不太基础

### 广播规则

> 广播允许通用函数以一种有意义的方式处理不具有完全相同形状的输入。
>
> 
>
> 广播的第一个规则是，如果所有输入数组的维数不相同，则会在较小阵列的形状前面重复加上一个“1”，直到所有阵列的维数相同。
>
> 
>
> 广播的第二个规则确保沿某一特定维度大小为1的数组表现得好像它们具有沿该维度形状最大的数组的大小。假设“广播”数组的数组元素沿该维度的值相同。
>
> 
>
> 在应用广播规则后，所有阵列的大小必须匹配。更多详情请参阅[广播](https://numpy.org/devdocs/user/basics.broadcasting.html#basics-broadcasting)。

<br>

---

<br>

## 高级索引和索引技巧



> NumPy提供了比常规Python序列更多的索引功能。
>
> 如前所述，除了通过整数和切片建立索引之外，还可以通过整数数组和布尔值数组对数组进行索引。

### 用索引数组建立索引

```python
a = np.arange(12)**2        
i = np.array([1,1,3,8,5])      #下标数组
a[i]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/2c3f44f71188e7bcb0351e26f82dda7c.png" style="zoom:80%;margin-left:10px" />

```python
j = np.array([[3,4],[7,9]])		#二维索引
a[j]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/3f656f52cd13bc2004a74e8a14be6233.png" style="zoom:80%;margin-left:10px" />



> 当索引数组a是多维的时，一个索引数组指的是a的第一个维。
>
> 下面的示例通过使用调色板将标签图像转换为彩色图像来显示这种行为。

```python
 palette = np.array([[0, 0, 0],         # black
                     [255, 0, 0],       # red
                     [0, 255, 0],       # green
                     [0, 0, 255],       # blue
                     [255, 255, 255]])  # white
 image = np.array([[0, 1, 2, 0],        # 每一个值都对应着palette中的一个颜色
                   [0, 3, 4, 0]])       
# 例如:0-black,1-red,2-green,3-blue,4-white
#image中的第一行[0, 1, 2,0],对应着palette中的四行
#        [  0,   0,   0],
#        [255,   0,   0],
#        [  0, 255,   0],
#        [  0,   0,   0]
 palette[image]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/641741110977fe6ea74486591098e52b.png" style="zoom:80%;margin-left:10px" />

> 我们还可以为多个维度提供索引。每个维度的索引数组必须具有相同的形状。

```python
a = np.arange(12).reshape(3,4)
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/f53e8c1bacc255d5d256f0c88f042d5f.png" style="zoom:80%;margin-left:10px" />

```python
i = np.array([[0,1],[1,2]])          #对应a数组的横下标
j = np.array([[2,1],[3,3]])          #对应a数组的纵下标
a[i,j]                               #i,j必须要有相同的形状，因为要一一对应
#对应结果a[0,2] = 2,a[1,1]=5......
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/69d81618bb477aa5301bf8324d181d3e.png" style="zoom:80%;margin-left:10px" />

```python
#2根据广播规则扩展为
#[2,2]
#[2,2]
a[i,2]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/00f8d05e318907d6a4bdb459124bb203.png" style="zoom:80%;margin-left:10px" />

```python
# :相当于
#[[0,0],[0,0]]
#[[1,1],[1,1]]
#[[2,2],[2,2]]
# j 根据广播规则扩展为
#[[2,1],[3,3]]
#[[2,1],[3,3]]
#[[2,1],[3,3]]
a[:,j]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/8e4d74c7a963666374a02922ee31db7f.png" style="zoom:80%;margin-left:10px" />

> 您还可以将索引与数组一起用作分配给以下对象的目标：

```ptyhon
a = np.arange(5)
print(a)
a[[1,3,4]]=0
print(a)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/d9d6fd3a198010dd9ab28dbd1e43d370.png" style="zoom:80%;margin-left:10px" />

> 但是，当索引列表包含重复项时，分配将完成几次，而留下最后一个值：

```python
a = np.arange(5)
a[[0,0,2]]=[1,2,3]    #执行两次对a[0]的赋值，最后一次a[0]=2
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/ce1959ff6b02130bac3b087b86fffd93.png" style="zoom:80%;margin-left:10px" />

---

### 用布尔数组建立索引

> 当我们使用（整数）索引数组对数组进行索引时，我们将提供要选择的索引列表。对于布尔索引，方法是不同的。
>
> 我们显式选择数组中需要哪些项，不需要哪些项。
>
> 对于布尔索引，可以想到的最自然的方法是使用形状与原始数组相同的布尔数组：

```python
a = np.arange(12).reshape(3,4)
b = a>4
b
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/7712f78e2de0f6b8e3185af43b575599.png" style="zoom:80%;margin-left:10px" />

```python
a[b]     #返回的是一维数组
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/978a156f7de40e0141b16c6a45acb088.png" style="zoom:80%;margin-left:10px" />

> 这个属性在分配时也同样有用

```python
a[b] = 0        所有大于4的都置为0
a
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/336b3ef682ce96979602bcb6bad2527d.png" style="zoom:80%;margin-left:10px" />

> 您可以看下面的示例，看看如何使用布尔索引来生成[Mandelbrot集](https://en.wikipedia.org/wiki/Mandelbrot_set)的图像：

```python
import numpy as np
import matplotlib.pyplot as plt
def mandelbrot( h,w, maxit=20 ):
    """返回大小(h,w)的曼德尔布罗特分形图像"""
    y,x = np.ogrid[ -1.4:1.4:h*1j, -2:0.8:w*1j ]   #横纵坐标,ogrid函数：取[-1.4,1.4),个数为h*1j
    #print(x.shape)   (1,400)
    #print(y.shape)   (400,1)
    c = x+y*1j
    z = c
    #print(c.shape)    (400,400)   c[i,j]=x[i,j]+y[i,j]
    divtime = maxit + np.zeros(z.shape, dtype=int)
    for i in range(maxit):
        z = z**2 + c
        diverge = z*np.conj(z) > 2**2            # 谁是发散的,（conj函数用于返回复数的共轭值）
        div_now = diverge & (divtime==maxit)  # 谁现在发散,（div_now是一个(400,400)的布尔值）
        #print(i,div_now)
        divtime[div_now] = i                  # note when
        z[diverge] = 2                        # 避免分散过多
    
    return divtime
plt.imshow(mandelbrot(400,400))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/61d7cb10e47fba71c27559a4282995b4.png" style="zoom:80%;margin-left:10px" />

> 使用布尔值建立索引的第二种方式与整数索引更相似；
>
> 对于数组的每个维度，我们提供一个一维布尔数组来选择所需的切片：

```python
a = np.arange(12).reshape(3,4)
print(a)
b1 = np.array([False,True,True])
b2 = np.array([True,False,True,False])
a[b1,:]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/3bebe1393fa412dc493251093ea3c046.png" style="zoom:80%;margin-left:10px" />

```python
a[:,b2]
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/d5d2891e7f8cef98757e34ec59615fa8.png" style="zoom:80%;margin-left:10px" />

```python
a[b1,b2]         #好奇怪，不大懂，候补
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/141fe25f7833cdab900e55fadb0942be.png" style="zoom:80%;margin-left:10px" />

> 注意，一维布尔数组的长度必须与要切片的维度(或轴)的长度一致。在前面的示例中，b1的长度为3 (a中的行数)，而b2(长度为4)适合于索引a的第二个轴(列)。

---

### ix_()函数

>ix_函数可用于组合不同的向量，得出多个向量的笛卡尔积的映射关系。
>
>例如，如果你想计算所有的a+b*c:

```python
a = np.array([2,3,4,5])
b = np.array([8,5,4])
c = np.array([5,4,6,8,3])
ax,bx,cx = np.ix_(a,b,c)
print(ax,ax.shape,'\n')
print(bx,bx.shape,'\n')
print(cx,cx.shape,'\n')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/8087c05d94b8c2d4d07d252386be1cb3.png" style="zoom:80%;margin-left:10px" />

```python
result = ax+bx*cx
print(result.shape)
result
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/a6e7c1d65148997871a59a9342801111.png" style="zoom:80%;margin-left:10px" />

```python
print(result[3,2,4])
print(a[3]+b[2]*c[4])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/dfb958fd84247d91e329f435aeb6e6da.png" style="zoom:80%;margin-left:10px" />

> 另一种方式
>
> 与普通的ufunc.reduce相比，这种reduce的优点在于它利用了[广播规则](https://numpy.org/devdocs/user/quickstart.html#broadcasting-rules) ，以避免创建一个参数数组，该参数数组的大小乘 以输出的数量乘以向量的数量。

```python
def ufunc_reduce(ufct, *vectors):
    vs = np.ix_(*vectors)
    r = ufct.identity
    for v in vs:
        r = ufct(r,v)
    return r
ufunc_reduce(np.add,a,b,c)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/bb55a653d14785eb11b65459bdf3c59c.png" style="zoom:80%;margin-left:10px" />

---

### 用字符串索引

> 结构化数组是ndarray，其数据类型是由一些更简单的数据类型组成的，这些简单数据类型被组织为一系列命名[字段](https://numpy.org/devdocs/glossary.html#term-field)

```python
x = np.array([('Rex', 9, 81.0), ('Fido', 3, 27.0)],
              dtype=[('name', 'U10'), ('age', 'i4'), ('weight', 'f4')])
x
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/c1afedab68e10bb41fb3d116a1dad8a2.png" style="zoom:80%;margin-left:10px" />

更多请参阅[结构化数组](https://numpy.org/devdocs/user/basics.rec.html#structured-arrays)

<br>

---

<br>

## 线性代数

### 简单的数组操作

> 有关更多信息，请参见numpy文件夹中的linalg.py

```python
import numpy as np
a = np.array([[1.0,2.0],[3.0,4.0]])
```

```python
a.transpose()         #转置
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/81873dbc2c4c9ebfe4ada546b165f175.png" style="zoom:80%;margin-left:10px" />

```python
np.linalg.inv(a)      #矩阵求逆
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/70767a4c3a9e6a34f45d8d0e0f1b1b52.png" style="zoom:80%;margin-left:10px" />

```python
np.linalg.det(a)      #求行列式
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/c5e234fa5d297b58cf65915f81bb43f0.png" style="zoom:80%;margin-left:10px" />

```python
u = np.eye(2)    #单位矩阵
u
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/f1d048ed112bfd7f309d15a8abf53464.png" style="zoom:80%;margin-left:10px" />

```python
j = np.array([[0.0, -1.0], [1.0, 0.0]])
j@j               #矩阵相乘
```

<img src="C:\Users\wangz\AppData\Roaming\Typora\typora-user-images\image-20201107222906525.png" alt="image-20201107222906525" style="zoom:80%;margin-left:10px" />

```python
np.trace(u)    #矩阵的迹
#在线性代数中，一个n×n矩阵A的主对角线（从左上方至右下方的对角线）上各个元素的总和被称为矩阵A的迹（或迹数），一般记作tr(A)。
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/d913a8f425f0ba22e643a39fca884366.png" style="zoom:80%;margin-left:10px" />

```python
y = np.array([[5.],[7,]])
np.linalg.solve(a,y)      # 调用solve函数求解线性方程
solve函数有两个参数a和b。a是一个N*N的二维数组，而b是一个长度为N的一维数组，solve函数找到一个长度为N的一维数组x，使得a和x的矩阵乘积正好等于b，数组x就是多元一次方程组的解

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/4b1cf7df575384f5046087567a9b9acc.png" style="zoom:80%;margin-left:10px" />

```python
np.linalg.eig(j)       #计算一个方阵的特征值和右特征向量。
#numpy.linalg.eig(a)[source]
#参数：
#a(…，M, M)数组
#为其计算特征值和正确特征向量的矩阵
#返回值
#w(…,M)数组
#特征值，每个根据它的多重性重复。特征值不一定是有序的。得到的数组将是复杂类型，除非虚部为零，在这种情况下，它将被转换为实类型。当a为实时，所得到的特征值将为实(0虚部)或以共轭对出现

#v(…，M, M)数组
#归一化(单位“length”)特征向量，使列v[:，i]为特征值w[i]对应的特征向量。
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/ad3da089c2d117603b5f8045bedf3487.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

## 技巧与窍门

### ”自动“重塑

```python
a = np.arange(30)
b = a.reshape((2,-1,3))   #-1指“Whatever is needed”
print(b,'\n',b.shape)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/a396e1ce29b883001a5739f599d5b3bd.png" style="zoom:80%;margin-left:10px" />

---

### 向量堆叠

> 我们如何根据一组等大小的行向量构造一个二维数组?
>
> 在MATLAB中这很简单:如果x和y是相同长度的两个向量，你只需要做m=[x;y]。
>
> 在NumPy中，它通过函数column_stack、dstack、hstack和vstack来工作，这取决于要进行堆叠的维度。例如:

```python
x = np.arange(0,10,2)
y = np.arange(5)
m = np.vstack([x,y])
print(m)
n = np.hstack([x,y])
print(n)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/1c62ebd370d8096df19c00f96977ba16.png" style="zoom: 80%;margin-left:10px" />

---

### 直方图

> 应用于数组的 NumPy  histogram函数返回一对向量:数组的直方图和bin edges的向量。
>
> 注意:matplotlib还有一个用于构建直方图的函数(在Matlab中称为hist)，它与NumPy中的函数不同。
>
> 主要的区别是pylab.hist自动绘制直方图，而numpy.histogram只生成数据。

```python
import numpy as np
rg = np.random.default_rng(1)       #设置随机种子
import matplotlib.pyplot as plt
#正态分布
mu,sigma = 2,0.5     #参数
v = rg.normal(mu,sigma,10000)#满足正态分布的10000个数
plt.hist(v,bins=50,density=1)   #bins：直方图的宽度，density:密度
(n,bins)=np.histogram(v,bins=50,density=True)
plt.plot(.5*(bins[1:]+bins[:-1]),n)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/07/5bf74fa2cba6d4bec9218260a854e58c.png" style="zoom:80%;margin-left:10px" />

---

如果发现问题或有疑问，欢迎下方留言