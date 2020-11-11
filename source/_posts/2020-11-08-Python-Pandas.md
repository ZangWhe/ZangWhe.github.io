---
title: Python-Pandas基础
tags:
  - Python
  - Pandas
categories: Python
abbrlink: 62063
date: 2020-11-08 15:48:40
---

## 概述

​	**Pandas**是一个[Python](https://www.python.org/)软件包，提供快速，灵活和富于表现力的数据结构。

​    **Pandas**建立在NumPy之上，旨在与许多其他第三方库在科学计算环境中很好地集成。

​    **Pandas** 的两个主要数据结构**Series**(一维)和**DataFrame**(二维)，处理了金融，统计，社会科学和许多工程领域的绝大多数典型用例。

<!--more-->

> **Pandas**对许多不同种类的数据都非常适合，例如：

- 具有不同类型列的制表数据，如SQL表或Excel电子表格中的数据

- 有序和无序(不一定是固定频率)时间序列数据。

- 具有行和列标签的任意矩阵数据(类型相同或异构)

- 任何其他形式的观测/统计数据集。实际上，数据根本不需要标记就可以放入到pandas数据结构中



>  以下是**Pandas**非常擅长做的事：

- 易于处理浮点数据和非浮点数据中的**缺失数据**（表示为NaN）
- 大小可变性：可以从DataFrame和更高维的对象中**插入和删除**列
- 自动和显式的**数据对齐**：可以将对象显式地对齐到一组标签，或者用户可以简单地忽略标签并让Series，DataFrame等自动为您对齐数据
- 强大，灵活的**分组**功能，可对数据集执行拆分应用合并操作，以汇总和转换数据
- 便于将其他Python和NumPy数据结构中的不规则、不同索引的数据转换为DataFrame对象
- 基于智能标签的**切片**，**花式索引**和 大数据集**子集**
- 直观的**合并**和**联接**数据集
- 灵活地**重塑**和旋转数据集
- 轴的**分层**标签（每个刻度可能有多个标签）
- 强大的IO工具，用于从**平面文件**（CSV和带分隔符），Excel文件，数据库中加载数据，以及从超快**HDF5格式**保存/加载数据
- 特定于**时间序列**的功能：日期范围生成和频率转换，移动窗口统计信息，日期移动和滞后。

<br>

---

<br>

## 安装

> 方式一：Anaconda

Anaconda作为一个跨平台（Linux,Mac OS X,Windows）的一个开源的Python发行版本

不仅包含了Pandas，还包含了其他诸如NumPy、Matplotlib等大量软件包

**下载方式**

（这里推荐清华大学开源软件镜像站下载，[点此跳转](https://mirrors.tuna.tsinghua.edu.cn/)）

1. 

![](https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/10/b80295990624279e201406d3908c048c.png)

2. ![](https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/10/7fffa959f6fd9eb15179b0dce7ecc432.png)
3. ![](https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/10/5ebf1c1d689bdc1b25206ef751ee40b8.png)

> 方式二：Miniconda

Anaconda有一个缺点就是大，因为他会预先安装上百个软件包，其中很多或许你用不到，这时候Miniconda就用到了

[Miniconda](https://conda.pydata.org/miniconda.html)允许您创建一个最小的自包含Python安装，然后使用 [Conda](https://conda.pydata.org/docs/)命令安装其他软件包。

**下载方式**

1. （由于本人使用的是Anaconda，所以也不详细介绍Miniconda）
2. 这里放一下[安装地址](https://docs.conda.io/en/latest/miniconda.html)

> 方式三： 从PyPI安装

打开cmd，使用命令行安装

命令：

```python
pip install pandas
```

(注：由于pip使用的是国外的源，所以下载可能会很慢，可以使用清华源进行下载)

```python
pip install pandas -i https://pypi.tuna.tsinghua.edu.cn/simple
```

<br>

---

<br>

## 进入主题，开始入门

> 这里推荐大家使用Jupyter练习Python，当然也可以使用其他方式

### 导入方式

```
import pandas as pd
import numpy as np             #接下来的样例中需要用到NumPy库
```

---

### 对象创建

>  更多信息请参阅官方文档关于[数据结构的简介](https://pandas.pydata.org/docs/user_guide/dsintro.html#dsintro)

#### Series



> [`Series`](https://pandas.pydata.org/docs/reference/api/pandas.Series.html#pandas.Series)是一维标记的数组，能够保存任何数据类型（整数，字符串，浮点数，Python对象等）。轴标签统称为**索引**。

创建Series的基本方法是调用：

```python
s = pd.Series(data,index=index)
```

**参数data可以是一个Python字典，一个ndarray对象，或是常量值**

**参数index指数组的索引，如果没有传递索引，则创建一个具有值的索引[0,1,……,len(data)-1]**

**(如果data是ndarray对象，则索引的长度必须与data的长度相同)**

> 举个栗子

```python
#data:字典
d = {'d':1,'a':0,'c':2}
print("data:字典")
print(pd.Series(d))

#data:ndarray
d = np.random.randn(5)
print("data:ndaary")
print(pd.Series(d,['A','B','C','D','E']))

#data:常量值，必须提供索引，该值将重复以匹配index的长度；如果不提供，则index只会等于0
d = 5
print("data:constant")
print(pd.Series(d,[0,1,2,3,4]))

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/ed247da54dd4162849732a08643d2fdb.png" style="zoom:80%;margin-left:10px" />

> Series是一个ndarray-like

&emsp;Series和ndarray的作用非常类似，并且在大多数NumPy函数中Series都是一个有效的参数。

但是，例如切片操作也会对标签进行切片

> 举个栗子

```python
s = pd.Series(np.random.randn(5))
#索引
print("索引")
print(s[0])
#切片
print("切片")
print(s[:3])
#布尔类型索引
print("布尔类型索引")
print(s[s>s.median()])
#索引数组建立建立索引
print("索引数组建立建立索引")
print(s[[1,4,3]])
#Series作为参数
print("Series作为参数")
print(np.exp(s))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/4cb6efd68c89a2745bd1533ef07612e7.png" style="zoom:80%;margin-left:10px" />

> 如果要用到数组，请使用[`Series.array`](https://pandas.pydata.org/docs/reference/api/pandas.Series.array.html#pandas.Series.array)

```python
s.array
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/9096faf5dea59d54e9224fe08b48eeff.png" style="zoom:80%;margin-left:10px" />

> 如果要用到ndarray.请使用[`Series.to_numpy()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.to_numpy.html#pandas.Series.to_numpy)

```python
s.to_numpy()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/7eee206ca699c89662162520f4f0cb15.png" style="zoom:80%;margin-left:10px" />

> 使用Series进行矢量化操作和标签对齐

在Pandas中对Series进行操作时和NumPy一样，通常不需要逐值循环。Series也可以作为参数传递给NumPy方法

```python
print("s+s:")
print(s+s)
print("s*2")
print(s*2)
print("np.exp(s)")
print(np.exp(s))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/6846f703a710484d25393570a5be0141.png" style="zoom:80%;margin-left:10px" />

#### DataFrame

> DataFrame是一个带有标签的二维数据结构，其中的列可能具有不同类型。它通常是最常用的pandas对象。

> DataFrame接受多种不同类型的输入：

- 一维ndarray,列表，字典或Series对象
- 二维numpy.ndarray对象
- [Structured数组或record数组](https://numpy.org/doc/stable/user/basics.rec.html)
- Series对象
- 另一个DataFrame对象

> 来自Series或dict的字典方式的DataFrame

```python
d = {'one': pd.Series([1., 2., 3.], index=['a', 'b', 'c']),
     'two': pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
df = pd.DataFrame(d)
df                    #空值使用NaN表示
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/005a62ba86af043bb2b68fa1f1f2ba8a.png" style="zoom:80%;margin-left:10px" />

```python
pd.DataFrame(d,index=['d','b','a'])   #根据指定标签输出
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/296880d0788e52d5faa439b83f1a905d.png" style="zoom:80%;margin-left:10px" />

```python
pd.DataFrame(d,columns=['two','three'])   #根据指定列输出，如果没有，则用空值NaN表示
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/acbb48d689649dabaca34c75c07bb521.png" style="zoom:80%;margin-left:10px" />

> 通过df.index和df.columns分别访问行标签和列表前

```python
print(df.index)          #行标签
print(df.columns)        #列标签
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/89b4eb61697406473fe18ea825049936.png" style="zoom:80%;margin-left:0px" />

> 来自ndrrays/list的字典

**ndarray的长度必须相同，如果传递了索引，那它的长度显然也必须与数组相同；如果未传递索引，则结果为range(n),其中n为数组长度**

```python
d = {'one':[1,2,3,4],'two':[4,3,2,1]}
pd.DataFrame(d)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/5d49e75010fde468a6f328588dc52f6f.png" style="zoom:80%;margin-left:10px" />

> 来自结构化或记录数组

```python
data = np.zeros((2, ), dtype=[('A', 'i4'), ('B', 'f4'), ('C', 'a10')])  #初始化结构化数组
data[:] = [(1,2.,'Hello'),(2,3.,'World')]
pd.DataFrame(data)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/c8d0f2e23d50edef05c76304f2145aca.png" style="zoom:80%;margin-left:10px" />

> 来自字典列表

```python
data2 = [{'a':1,'b':2},{'a':5,'b':10,'c':20}]
pd.DataFrame(data2)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/47787f597d16a4262c826872476f83a1.png" style="zoom:80%;margin-left:10px" />

> 来自元组的字典

```python
#这样排列纯粹为了方便看点
pd.DataFrame({
               ('一', 'b'): 
                            {('三', 'B'): 1, ('三', 'C'): 2},
               ('一', 'a'): 
                            {('三', 'C'): 3, ('三', 'B'): 4},
               ('一', 'c'): 
                            {('三', 'B'): 5, ('三', 'C'): 6},
               ('二', 'a'): 
                            {('三', 'C'): 7, ('三', 'B'): 8},
               ('二', 'b'): 
                            {('三', 'D'): 9, ('三', 'B'): 10}})

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/a6637bf52eae7015d4c8f78666bdecc1.png" style="zoom:80%;margin-left:10px" />

> 来自Series

```python
s1 = pd.Series(np.random.randn(5),index=['a','b','c','d','e'])
s2 = pd.Series(np.random.randn(5),index=['a','b','c','d','e'])
df = pd.DataFrame((s1,s2))

df
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/9cc4f898886e45ac0cc9cc59a77d49ac.png" style="zoom:80%;margin-left:10px" />

> 列的选择，添加，删除

```python
#选择
df['e']
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/bab1b522203b0ca9ab5200b695bc54e5.png" style="zoom:80%;margin-left:10px" />

```python
#添加
df['f']=df['a']+df['b']
df['flag'] = df['c'] > 0
df
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/8f1fc43a9cb8d42f75427640daf3cddf.png" style="zoom:80%;margin-left:10px" />

```python
#删除的两种方式
del df['d']
e = df.pop('e')
df
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/9406a517d721a2daef233975c7d69f80.png" style="zoom:80%;margin-left:10px" />

```python
#插入
df.insert(1,'z',df['a'])
df
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/89ee07e147623f19650800693965612a.png" style="zoom:80%;margin-left:10px" />