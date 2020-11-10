---
title: Python—NumPy的了解与准备工作
tags:
  - Python
  - NumPy
categories: Python
abbrlink: 46594
date: 2020-11-06 18:59:03
---





## 了解什么是NumPy



> ​	NumPy是Python中科学计算的基本软件包。它是一个Python库，提供多维数组对象，各种派生对象（例如蒙版数组和矩阵）以及各种[例程](https://baike.baidu.com/item/%E4%BE%8B%E7%A8%8B/2390628?fr=aladdin)，用于对数组进行快速操作，包括数学，逻辑，形状处理，排序，选择，   I / O ，离散傅立叶变换，基本线性代数，基本统计运算，随机模拟等等。



<!--more-->



更多信息请自行查询[官方文档](https://numpy.org/devdocs/user/whatisnumpy.html)或百度

<br>

---

<br>

## NumPy 安装



- ​	使用已有的发行版本

  - [Anaconda](https://www.anaconda.com/download/): 免费 Python 发行版，用于进行大规模数据处理、预测分析，和科学计算，致力于简化包的管理和部署。支持 Linux, Windows 和 Mac 系统。
  - [Enthought Canopy](https://www.enthought.com/products/canopy): 提供了免费和商业发行版。持 Linux, Windows 和 Mac 系统。
  - [Python(x,y)](https://python-xy.github.io/): 免费的 Python 发行版，包含了完整的 Python 语言开发包 及 [Spyder IDE](https://www.spyder-ide.org/)。支持 Windows，仅限 Python 2 版本。
  - [WinPython](https://winpython.github.io/): 另一个免费的 Python 发行版，包含科学计算包与 Spyder IDE。支持 Windows。
  - [Pyzo](http://www.pyzo.org/): 基于 Anaconda 的免费发行版本及 IEP 的交互开发环境，超轻量级。 支持 Linux, Windows 和 Mac 系统。

  

- 使用pip安装 &emsp;  (numpy常与scipy matplotlib搭配使用)

  - (国外线路，下载会较慢）

  ```
  pip install numpy scipy matplotlib
  ```

  - (清华源下载，速度较快)

  ```
  pip install numpy scipy matplotlib  -i https://pypi.tuna.tsinghua.edu.cn/simple
  ```

  ​    

- 使用conda安装

  ```
  conda install numpy scipy matplotlib
  ```

  (conda 命令使用清华源安装请自行百度)

- Linux下安装

  - Ubuntu & Debain

  ```
  sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose
  ```

  - CentOS/Fedora

  ```
  sudo dnf install numpy scipy python-matplotlib ipython python-pandas sympy python-nose atlas-devel
  ```

  - Mac系统

  ```
  pip install numpy scipy matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple
  ```

- 验证是否安装成功

```python
import numpy as np
np.eye(4)
```

<img src="https://cdn.jsdelivr.net/gh/zangwhe/Image@main/2020/11/06/660fcfbb056e265019b0c0b02620dd68.png" style="zoom: 80%;margin-left:10px;"/>



---

