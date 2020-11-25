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
#三个参数:
#第一个：插入的位置
#第二个：插入的列名
#第三个：插入的值
df.insert(1,'z',df['a'])
df
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/11/89ee07e147623f19650800693965612a.png" style="zoom:80%;margin-left:10px" />

---

### 必要的基本功能



#### 先创建一些示例对象

```python
import pandas as pd
import numpy as np
index = pd.date_range('1/1/2000',periods=8)
s = pd.Series(np.random.randn(5),index=['a','b','c','d','e'])
df = pd.DataFrame(np.random.randn(8,3),index = index)
print(index)
print(s)
print(df)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/ce892e66945574c9b7b0968f7cc8f6ff.png" style="zoom:80%;margin-left:10px" />

#### 查看head和tail

**默认显示的元素数量为5，但是可以传递自定义的数字**

```python
long_series = pd.Series(np.random.randn(1000))
print("long_series.head():")
print(long_series.head())
print("long_series.tail():")
print(long_series.tail(1))
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/f8cf1b21e282ff44e5e690338a34f8e0.png" style="zoom:80%;margin-left:10px" />

#### 加速操作

&emsp;pandas支持使用numexpr库和bottleneck库来加速某些类型的二进制数值和布尔运算。

这些库在处理大型数据集时特别有用，而且可以大大提高处理速度

**看一个示例（使用100列×100,000行的DataFrame对象）**

| 操作    | 优化后 | 优化前 |
| ------- | ------ | ------ |
| df1>df2 | 13.32  | 125.35 |
| df1*df2 | 21.71  | 36.63  |
| df1+df2 | 22.04  | 36.50  |

**这两个库是及其推荐安装的，可以使用pip或conda方式安装**

**安装后这两个都是默认启用的，可以通过设置以下选项来控制它们**

```python
pd.set_option('compute.use_bottleneck', False)
pd.set_option('compute.use_numexpr', False)
```

#### 迭代 

> &emsp;Pandas对象的基本迭代行为取决于类型。
>
> &emsp;对Series进行迭代时，它被看作是array-like,并且基本的迭代会产生值。
>
> &emsp;DataFrame遵循类似dict的约定，即在对象的“键”生进行迭代

&emsp;简而言之，基本的迭代（for i in object）产生:

- **Series**: 值
- **DataFrame**:列标签

> 例如：在DataFrame对象上进行基本迭代会返回列的名字

```python
df = pd.DataFrame({'col1': np.random.randn(3),
                    'col2': np.random.randn(3)}, index=['a', 'b', 'c'])

for col in df:
    print(col)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/a6b2f6ecaf98a6469c4e79d0a15deb38.png" style="zoom:80%;margin-left:10px" />

> Pandas对象也可以使用items()方法对dict-like对象来迭代(key,value)

```python
df = pd.DataFrame({'col1': np.random.randn(3),
                    'col2': np.random.randn(3)}, index=['a', 'b', 'c'])

for key_value in df.items():
    print(key_value)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/6f587123adc8281bd2d588a2a0ca89ed.png" style="zoom:80%;margin-left:10px" />

> 要遍历DataFrame的行，也可以使用以下方法：

- iterrows() : 以(index，Series)对的形式遍历DataFrame的行；这会将行转换为Series对象。
- itertuples() : 将DataFrame的行作为值命名元组从而进行迭代。这比iterrows()要快得多。

```python
for Series_row in df.iterrows():
    print(Series_row)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/df01f312399bf1c3b8530460c6f2e104.png" style="zoom:80%;margin-left:10px" />

```python
for tuples_row in df.itertuples():
    print(tuples_row)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/3269e9f36197bf211364ae932e518f96.png" style="zoom:80%;margin-left:10px" />

#### 排序

> Pandas支持三种排序方式：**按索引标签排序，按列值排序以及两者结合进行排序**

##### 按索引标签排序

[`Series.sort_index()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.sort_index.html#pandas.Series.sort_index) 和 [`DataFrame.sort_index()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_index.html#pandas.DataFrame.sort_index) 方法用于对pandas对象根据标签排序

```python
df = pd.DataFrame({
     'one': pd.Series(np.random.randn(3), index=['a', 'b', 'c']),
     'two': pd.Series(np.random.randn(4), index=['a', 'b', 'c', 'd']),
     'three': pd.Series(np.random.randn(3), index=['b', 'c', 'd'])})
#重新索引
unsorted_df = df.reindex(index=['a', 'd', 'c', 'b'],
                             columns=['three', 'two', 'one'])
print(unsorted_df)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/f3cea2d97d436198aabbde98bd8b58ba.png" style="zoom:80%;margin-left:10px" />

```python
unsorted_df.sort_index()
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/eeefd397e51072050a9ed586710f2ab6.png" style="zoom:80%;margin-left:10px" />

```python
unsorted_df.sort_index(ascending=False)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/12/61b7d952bda49336b26155d0234c7455.png" style="zoom:80%;margin-left:10px" />

```python
unsorted_df.sort_index(axis=1)   #axis=1表示跨操作，这里根据列名进行排序(根据字母排序)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/13/34073a692bc4e52799064d4cf2a36a35.png" style="zoom:80%;margin-left:10px" />

---

##### 按值排序

- [`Series.sort_values()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.sort_values.html#pandas.Series.sort_values)方法用于对Series对象根据值排序
- [`DataFrame.sort_values()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html#pandas.DataFrame.sort_values)方法用来对DataFrame对象根据列或行的值进行排序
  - [`DataFrame.sort_values()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html#pandas.DataFrame.sort_values)的参数**by**用来指定一个或多个列来确定排序顺序

```python
df1 = pd.DataFrame({'one': [2, 1, 1, 1],
                     'two': [1, 3, 2, 4],
                     'three': [5, 4, 3, 2]})
#根据列标签'two'对应的值从小到大排序
df1.sort_values(by='two')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/13/c9b64a6f93a8cb63f0ec6d281a7bbe34.png" style="zoom:80%;margin-left:10px" />

```python
df1.sort_values(by=['one','two'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/13/93e5ed81ba73e58e2c8e5c722a1988e7.png" style="zoom:80%;margin-left:10px" />

##### 按标签和值排序

**作为by参数传递给DataFrame.sort_values()的字符串可以引用列或索引级别的名称。**

```python
#MultiIndex.from_tuples()生成一个元组类型的多重索引
idx = pd.MultiIndex.from_tuples([('a',1),('a',2),('a',2),('b', 2), ('b', 1), ('b', 1)]);
idx.names=['first','second']
idx   #多重索引，第一重名字为first，第二重名字为second
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/76218d3801bb21dea219155c1be5e263.png" style="zoom:80%;margin-left:10px" />

```python
# np.arange(6,0,-1)  =>  array([6, 5, 4, 3, 2, 1])   
df_multi = pd.DataFrame({'A':np.arange(6,0,-1)},index=idx)
df_multi
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/d2c5799ebcb2b4e2628a66c7823143be.png" style="zoom:80%;margin-left:10px" />

```python
df_multi.sort_values(by=['second','A'])    #'second'和'A'的顺序决定了先根据谁排序
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/936962dc75c7571e64e958416742e168.png" style="zoom:80%;margin-left:10px" />

---

### IO工具（text,CSV,HDF5,...）

下面是一个包含可用读取器和写入器的表。

| Type   | Data Description                                             | Reader                                                       | Writer                                                       |
| :----- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| text   | [CSV](https://en.wikipedia.org/wiki/Comma-separated_values)  | [read_csv](https://pandas.pydata.org/docs/user_guide/io.html#io-read-csv-table) | [to_csv](https://pandas.pydata.org/docs/user_guide/io.html#io-store-in-csv) |
| text   | Fixed-Width Text File                                        | [read_fwf](https://pandas.pydata.org/docs/user_guide/io.html#io-fwf-reader) |                                                              |
| text   | [JSON](https://www.json.org/)                                | [read_json](https://pandas.pydata.org/docs/user_guide/io.html#io-json-reader) | [to_json](https://pandas.pydata.org/docs/user_guide/io.html#io-json-writer) |
| text   | [HTML](https://en.wikipedia.org/wiki/HTML)                   | [read_html](https://pandas.pydata.org/docs/user_guide/io.html#io-read-html) | [to_html](https://pandas.pydata.org/docs/user_guide/io.html#io-html) |
| text   | Local clipboard                                              | [read_clipboard](https://pandas.pydata.org/docs/user_guide/io.html#io-clipboard) | [to_clipboard](https://pandas.pydata.org/docs/user_guide/io.html#io-clipboard) |
|        | [MS Excel](https://en.wikipedia.org/wiki/Microsoft_Excel)    | [read_excel](https://pandas.pydata.org/docs/user_guide/io.html#io-excel-reader) | [to_excel](https://pandas.pydata.org/docs/user_guide/io.html#io-excel-writer) |
| binary | [OpenDocument](http://www.opendocumentformat.org/)           | [read_excel](https://pandas.pydata.org/docs/user_guide/io.html#io-ods) |                                                              |
| binary | [HDF5 Format](https://support.hdfgroup.org/HDF5/whatishdf5.html) | [read_hdf](https://pandas.pydata.org/docs/user_guide/io.html#io-hdf5) | [to_hdf](https://pandas.pydata.org/docs/user_guide/io.html#io-hdf5) |
| binary | [Feather Format](https://github.com/wesm/feather)            | [read_feather](https://pandas.pydata.org/docs/user_guide/io.html#io-feather) | [to_feather](https://pandas.pydata.org/docs/user_guide/io.html#io-feather) |
| binary | [Parquet Format](https://parquet.apache.org/)                | [read_parquet](https://pandas.pydata.org/docs/user_guide/io.html#io-parquet) | [to_parquet](https://pandas.pydata.org/docs/user_guide/io.html#io-parquet) |
| binary | [ORC Format](https://orc.apache.org/)                        | [read_orc](https://pandas.pydata.org/docs/user_guide/io.html#io-orc) |                                                              |
| binary | [Msgpack](https://msgpack.org/index.html)                    | [read_msgpack](https://pandas.pydata.org/docs/user_guide/io.html#io-msgpack) | [to_msgpack](https://pandas.pydata.org/docs/user_guide/io.html#io-msgpack) |
| binary | [Stata](https://en.wikipedia.org/wiki/Stata)                 | [read_stata](https://pandas.pydata.org/docs/user_guide/io.html#io-stata-reader) | [to_stata](https://pandas.pydata.org/docs/user_guide/io.html#io-stata-writer) |
| binary | [SAS](https://en.wikipedia.org/wiki/SAS_(software))          | [read_sas](https://pandas.pydata.org/docs/user_guide/io.html#io-sas-reader) |                                                              |
| binary | [SPSS](https://en.wikipedia.org/wiki/SPSS)                   | [read_spss](https://pandas.pydata.org/docs/user_guide/io.html#io-spss-reader) |                                                              |
| binary | [Python Pickle Format](https://docs.python.org/3/library/pickle.html) | [read_pickle](https://pandas.pydata.org/docs/user_guide/io.html#io-pickle) | [to_pickle](https://pandas.pydata.org/docs/user_guide/io.html#io-pickle) |
| SQL    | [SQL](https://en.wikipedia.org/wiki/SQL)                     | [read_sql](https://pandas.pydata.org/docs/user_guide/io.html#io-sql) | [to_sql](https://pandas.pydata.org/docs/user_guide/io.html#io-sql) |
| SQL    | [Google BigQuery](https://en.wikipedia.org/wiki/BigQuery)    | [read_gbq](https://pandas.pydata.org/docs/user_guide/io.html#io-bigquery) | [to_gbq](https://pandas.pydata.org/docs/user_guide/io.html#io-bigquery) |

> 更多关于IO详细解释与操作请到Pandas官网查阅
>
> [点此跳转](https://pandas.pydata.org/docs/user_guide/io.html)

---

### Merge, join, concatenate and compare

#### concatebate

> concat()函数完成沿轴执行连接操作的所有繁重工作，同时在其他轴上执行索引(如果有的话)的可选集合逻辑(并集或交集)。
>
> 注意，之所以说“如果有”，是因为Series的串联轴只有一个可能的轴。

先看一个关于concat()函数的简单应用：

```python
df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                        'B': ['B0', 'B1', 'B2', 'B3'],
                        'C': ['C0', 'C1', 'C2', 'C3'],
                        'D': ['D0', 'D1', 'D2', 'D3']},
                       index=[0, 1, 2, 3])
    
df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
                        'B': ['B4', 'B5', 'B6', 'B7'],
                        'C': ['C4', 'C5', 'C6', 'C7'],
                        'D': ['D4', 'D5', 'D6', 'D7']},
                       index=[4, 5, 6, 7])
    

df3 = pd.DataFrame({'A': ['A8', 'A9', 'A10', 'A11'],
                        'B': ['B8', 'B9', 'B10', 'B11'],
                        'C': ['C8', 'C9', 'C10', 'C11'],
                        'D': ['D8', 'D9', 'D10', 'D11']},
                       index=[8, 9, 10, 11])
    

frames = [df1, df2, df3]

result = pd.concat(frames)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/5d3e8e76d5a9462b40bf71ab80a83175.png" style="zoom:80%;margin-left:10px" />



> concat()函数的参数介绍

```python
pd.concat(objs,axis=0,join='outer',ignore_index=False,keys=None,levels=None,names=None,verify_integrity=False, copy=True)
```

- `objs`：Series或DataFrame对象的序列或映射。如果传递了dict ，则除非传递了已排序的键，否则它将用作keys参数，在这种情况下，将选择值（请参见下文）。任何None对象将被无声地删除，除非它们都是None，在这种情况下，ValueError将被抛出。
- `axis` ：{0，1，…}，默认值为0。要沿其连接的轴。
- `join`：{'inner'，'outer'}，默认为'outer'。如何处理其他轴上的索引。outer为联合，inner为交叉。
- `ignore_index`：布尔值，默认为False。如果为True，则不要在串联轴上使用索引值。结果轴将标记为0，…，n-1。如果要串联对象时，串联轴没有有意义的索引信息，这将很有用。请注意，联接中仍会考虑其他轴上的索引值。
- `keys`：序列，默认为无。使用传递的键作为最外层级别来构造层次结构索引。如果通过了多个级别，则应包含元组。
- `levels`：序列列表，默认为无。用于构造MultiIndex的特定级别（唯一值）。否则，将从按键推断出它们。
- `names`：列表，默认为无。生成的层次结构索引中的级别的名称。
- `verify_integrity`：布尔值，默认为False。检查新的连接轴是否包含重复项。相对于实际数据连接而言，这可能会非常昂贵。
- `copy`：布尔值，默认为True。如果为False，则不会不必要地复制数据。

**回顾一下上面对参数讲解时的keys参数，假设我们想将特定的键与分割后的DataFrame片段，我们可以使用keys参数实现这一点：**

```python
result = pd.concat(frames, keys=['x', 'y', 'z'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/e2bb6f84b878680ef0a97dfb82ee71d8.png" style="zoom:80%;margin-left:10px" />

> 关于对Pandas对象的连接请关注官方文档
>
> [点此跳转](https://pandas.pydata.org/docs/user_guide/merging.html#concatenating-objects)

---

#### Merge

> [`merge()`](https://pandas.pydata.org/docs/reference/api/pandas.merge.html#pandas.merge)作为`DataFrame`或命名为`Series`的对象之间所有标准数据库联接操作的入口点：

```python
pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None,
         left_index=False, right_index=False, sort=True,
         suffixes=('_x', '_y'), copy=True, indicator=False,
         validate=None)
```

**参数详情如下：**

- `left`：一个DataFrame或命名为Series的对象。

- `right`：另一个DataFrame或命名为Series的对象。

- `on`：要连接的列或索引级的名称。必须在left和right中的DataFrame和/或Series对象中找到。如果没有通过，`left_index`且 `right_index`是`False`，在DataFrames和/或Series列的交叉点会被推断为联接键。

- `left_on`：左侧DataFrame或Series中的列或索引级别用作键。可以是列名称，索引级别名称，也可以是长度等于DataFrame或Series长度的数组。

- `right_on`：右侧DataFrame或Series中的列或索引级别用作键。可以是列名称，索引级别名称，也可以是长度等于DataFrame或Series长度的数组。

- `left_index`：如果为`True`，则使用左侧DataFrame或Series中的索引（行标签）作为其连接键。对于具有MultiIndex（分层结构）的DataFrame或Series，级别数必须与正确的DataFrame或Series中的联接键数匹配。

- `right_index`：与`left_index`的DataFrame或Series的用法相同

- `how`：其一`'left'`，`'right'`，`'outer'`，`'inner'`。默认为`inner`。有关每种方法的详细说明，请参见下文。

- `sort`：按字典顺序按连接键对结果DataFrame进行排序。默认为`True`，设置为`False`可以在许多情况下显著提高性能。

- `suffixes`：适用于重叠列的字符串后缀元组。默认为。`('_x', '_y')`

- `copy`注意：始终`True`从传递的DataFrame或命名的Series对象复制数据（默认），即使不需要重新索引也是如此。在很多情况下都无法避免，但是可以提高性能/内存使用率。可以避免复制的情况有些病态，但是仍然提供了此选项。

- `indicator`：将一列添加到输出DataFrame中`_merge` ，并在每一行的源上提供信息。`_merge`是类别类型的，`left_only`对于其合并键仅出现在`'left'`DataFrame或Series中`right_only`的观察值，对于其合并键仅出现在`'right'`DataFrame或Series中`both`的观察值以及在两个视图中均找到观察值的合并键，则取值为。

- `validate`：字符串，默认为无。如果指定，则检查merge是否为指定的类型。

  - “ one_to_one”或“ 1：1”：检查合并键在左右数据集中是否唯一。

  - “ one_to_many”或“ 1：m”：检查合并键在左数据集中是否唯一。

  - “ many_to_one”或“ m：1”：检查合并键在右数据集中是否唯一。

  - “ many_to_many”或“ m：m”：允许，但不进行检查。

<br>

how选项中的合并方式

| 合并方式 | SQL连接名称        | 描述                       |
| :------- | :----------------- | :------------------------- |
| `left`   | `LEFT OUTER JOIN`  | 仅保留左边中的keys         |
| `right`  | `RIGHT OUTER JOIN` | 仅保留右边中的keys         |
| `outer`  | `FULL OUTER JOIN`  | 使用两个对象中的keys的并集 |
| `inner`  | `INNER JOIN`       | 使用两个对象中的keys的交集 |

```python
left = pd.DataFrame({'key1': ['K0', 'K0', 'K1', 'K2'],
                      'key2': ['K0', 'K1', 'K0', 'K1'],
                      'A': ['A0', 'A1', 'A2', 'A3'],
                      'B': ['B0', 'B1', 'B2', 'B3']})
 

right = pd.DataFrame({'key1': ['K0', 'K1', 'K1', 'K2'],
                      'key2': ['K0', 'K0', 'K0', 'K0'],
                       'C': ['C0', 'C1', 'C2', 'C3'],
                       'D': ['D0', 'D1', 'D2', 'D3']})
 

result = pd.merge(left, right, on=['key1', 'key2'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/5e7b61eec81bb6d32a6a5df67c3bc276.png" style="zoom:80%;margin-left:10px" />

```python
result = pd.merge(left, right, how='left', on=['key1', 'key2'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/bd621e62239896341c7c8153080b5ccf.png" style="zoom:80%;margin-left:10px" />

```python
result = pd.merge(left, right, how='right', on=['key1', 'key2'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/788728f63f70852ceafd9920b4614036.png" style="zoom:80%;margin-left:10px" />

```python
result = pd.merge(left, right, how='outer', on=['key1', 'key2'])

```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/6beb5baa7b731bcad4081b208e78fb7a.png" style="zoom:80%;margin-left:10px" />

```python
result = pd.merge(left, right, how='inner', on=['key1', 'key2'])
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/30af901305746869a00e4965e1873a67.png" style="zoom:80%;margin-left:10px" />

---

#### Join

> [`DataFrame.join()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.join.html#pandas.DataFrame.join)是将两个可能具有不同索引的数据文件的列组合成单个结果数据文件的一种方便方法。

这里有一个非常基本的例子:

```python
left = pd.DataFrame({'A': ['A0', 'A1', 'A2'],
                      'B': ['B0', 'B1', 'B2']},
                     index=['K0', 'K1', 'K2'])
 
right = pd.DataFrame({'C': ['C0', 'C2', 'C3'],
                       'D': ['D0', 'D2', 'D3']},
                      index=['K0', 'K2', 'K3'])
 

result = left.join(right)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/f2c31a9f5b9f9847351ee0a8d10db032.png" style="zoom:80%;margin-left:10px" />

```python
result = left.join(right, how='outer')  #并集
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/92f7497917a892826e8851a86041ad51.png" style="zoom:80%;margin-left:10px" />

```python
result = left.join(right, how='inner')  #交集
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/5217ec44ddf63aa36bdc1b5ffdc6702e.png" style="zoom:80%;margin-left:10px" />

> 在列上的Join

```python
left = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                      'B': ['B0', 'B1', 'B2', 'B3'],
                      'key': ['K0', 'K1', 'K0', 'K1']})


right = pd.DataFrame({'C': ['C0', 'C1'],
                       'D': ['D0', 'D1']},
                      index=['K0', 'K1'])
 

result = left.join(right, on='key')
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/1be2827ca29bb501329b2137d6b385a7.png" style="zoom:80%;margin-left:10px" />

---

#### Compare

> 使用[`compare()`](https://pandas.pydata.org/docs/reference/api/pandas.Series.compare.html#pandas.Series.compare)和[`compare()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.compare.html#pandas.DataFrame.compare)方法(两个compare()方法分别对应Series和DataFrame的compare方法)，您可以分别比较两个DataFrame或Series，并总结它们之间的差异。

**Pandas 的 V1.1.0版本中加入了此功能**

**如果显示AttributeError: 'DataFrame' object has no attribute 'compare'   ，大概率是版本不够的原因**

先定义一个DataFrame对象

```python
df = pd.DataFrame(
     {
         "col1": ["a", "a", "b", "b", "a"],
         "col2": [1.0, 2.0, 3.0, np.nan, 5.0],
         "col3": [1.0, 2.0, 3.0, 4.0, 5.0]
     },
     columns=["col1", "col2", "col3"],
 )
df
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/9c3d196d0eef3d76bc99c15dc019e3cd.png" style="zoom:80%;margin-left:10px" />

df2复制df，并修改两个值

```python
df2 = df.copy()
df2.loc[0,'col1'] = 'c'
df2.loc[2,'col3'] = 4.0
df2
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/a8c238bc148dc3b16452977ed6f7a262.png" style="zoom:80%;margin-left:10px" />

比较

```python
df.compare(df2)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/8ff76e9663c05e299a5e288940c18fc5.png" style="zoom:80%;margin-left:10px" />

如果需要，可选择差异在行上堆叠显示

```python
df.compare(df2, align_axis=0)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/14/b52952109bede8bfa30e711853fe818d.png" style="zoom:80%;margin-left:10px" />

<br>

---

<br>

如果你发现文章中出现的错误或者任何疑问欢迎在下方评论区评论





