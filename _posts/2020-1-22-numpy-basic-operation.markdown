---
layout:     post
title:      "Numpy 基本操作"
subtitle:   " \" numpy basic operation\""
date:       2020-1-22 13:01:00
author:     "张凡"
header-img: "https://aerozf.oss-cn-beijing.aliyuncs.com/images/frp_network.jpg"
catalog: true
tags:
    - 服务器
    - frp
---

## Numpy 基本操作

- 基本概念

  - array.ndim     数组轴的个数
  - array.shape    数组的维度
  - array.size         数组元素的总个数
  - array.dtype     数组元素的类型
  - array.itemsize 数组中每个元素的字节大小
  - array.data        包含实际数组元素的缓冲区（地址位置）

  ```python
  In [1]: import numpy as np
  In [2]: a=np.random.randn(3,4)
  In [3]: a
  Out[3]: 
  array([[ 0.07730844, -0.67299791,  0.51333217, -0.48144071],
         [ 1.12056794, -1.11480193,  0.36176565,  0.84209968],
         [ 0.19255922,  0.58232696, -0.58533054,  0.30037351]])
  In [4]: a.ndim
  Out[4]: 2
  In [5]: a.shape
  Out[5]: (3, 4)
  In [6]: a.size
  Out[6]: 12
  In [7]: a.dtype
  Out[7]: dtype('float64')
  In [8]: a.itemsize
  Out[8]: 8
  In [9]: a.data
  Out[9]: <memory at 0x000001574C23B3A8>
  ```

- 创建数组

  - numpy.array(list)     通过数组创建array对象
  - numpy.zeros(tuple)   创建全0array对象
  - numpy.ones(tuple)   创建全1array对象
  - numpy.arange(start,end,step)    创建连续序列
  - numpy.linspace(start,end,num)  创建连续序列
  - numpy.random.randn(m,n)   创建随机数组

  ```python
  In [10]: a=np.array([1,2,3,4,5])
  In [11]: a
  Out[11]: array([1, 2, 3, 4, 5])
  In [12]: b=np.zeros((3,4))
  In [13]: b
  Out[13]: 
  array([[0., 0., 0., 0.],
         [0., 0., 0., 0.],
         [0., 0., 0., 0.]])
  In [14]: c=np.ones((3,4))
  In [15]: c
  Out[15]: 
  array([[1., 1., 1., 1.],
         [1., 1., 1., 1.],
         [1., 1., 1., 1.]])
  In [16]: d=np.arange(0,10,1)
  In [17]: d
  Out[17]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
  In [18]: e=np.linspace(0,10,20)
  In [19]: e
  Out[19]: 
  array([ 0.        ,  0.52631579,  1.05263158,  1.57894737,  2.10526316,
          2.63157895,  3.15789474,  3.68421053,  4.21052632,  4.73684211,
          5.26315789,  5.78947368,  6.31578947,  6.84210526,  7.36842105,
          7.89473684,  8.42105263,  8.94736842,  9.47368421, 10.        ])
  In [20]: f=np.random.randn(3,4)
  In [21]: f
  Out[21]: 
  array([[-0.47241529,  0.82223497, -0.56418561, -1.83797943],
         [-2.40210165, -1.06299785, -0.15278713,  1.05393034],
         [ 0.726491  , -0.12466184, -0.321895  ,  1.17075301]])
  ```

- 基本运算

  - 加、减、乘、除    直接相加减
  - 矩阵点乘   np.dot(A,B) 或 A.dot(B)
  - 矩阵求逆   np.linalg.inv(A)
  - 内置函数运算  例如sin(),cos()
  - 统计类运算，求最大值、最小值、求和等(可通过axis来指定对应的轴)

  ```python
  In [22]: a=np.array([1,2,3,4])
  In [23]: b=np.array([4,3,2,1])
  In [24]: a+b
  Out[24]: array([5, 5, 5, 5])
  In [25]: a*b
  Out[25]: array([4, 6, 6, 4])
  In [26]: a/b
  Out[26]: array([0.25      , 0.66666667, 1.5       , 4.        ])
  In [27]: a-b
  Out[27]: array([-3, -1,  1,  3])
  In [28]: A=np.array([[1,2],[3,4]])
  In [29]: B=np.array([[1,2],[3,4]])
      ...: 
  In [30]: A.dot(B)
  Out[30]: 
  array([[ 7, 10],
         [15, 22]])
  In [31]: np.dot(A,B)
  Out[31]: 
  array([[ 7, 10],
         [15, 22]])
  In [32]: np.linalg.inv(A)
  Out[32]: 
  array([[-2. ,  1. ],
         [ 1.5, -0.5]])
  In [33]: np.sin(A)
  Out[33]: 
  array([[ 0.84147098,  0.90929743],
         [ 0.14112001, -0.7568025 ]])
  In [34]: np.exp(A)
  Out[34]: 
  array([[ 2.71828183,  7.3890561 ],
         [20.08553692, 54.59815003]])
  In [35]: np.sum(A)
  Out[35]: 10
  In [36]: np.sum(A,axis=0)
  Out[36]: array([4, 6])
  In [37]: np.min(A)
  Out[37]: 1
  In [38]: np.min(A,axis=0)
  Out[38]: array([1, 2])
  In [39]: np.max(A)
  Out[39]: 4
  In [40]: np.max(A,axis=0)
  Out[40]: array([3, 4])
  ```

- 索引、切片

  - 一维数组索引，用:+数字来索引
  - 多维数组索引方式和一维数组类似，若取某个坐标轴全部的值，则用：来取
  - 使用多为数组flat属性来迭代获取多位数组元素

  ```python
  In [41]: a=np.arange(0,10,1)
  In [42]: a
  Out[42]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
  In [43]: a[2:6]
  Out[43]: array([2, 3, 4, 5])
  In [44]: a[:4]
  Out[44]: array([0, 1, 2, 3])
  In [45]: a[2:]
  Out[45]: array([2, 3, 4, 5, 6, 7, 8, 9])
  In [46]: a[:]
  Out[46]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
  In [47]: a[2:-2]
  Out[47]: array([2, 3, 4, 5, 6, 7])
  In [48]: b=np.ones((5,5))
  In [49]: b
  Out[49]: 
  array([[1., 1., 1., 1., 1.],
         [1., 1., 1., 1., 1.],
         [1., 1., 1., 1., 1.],
         [1., 1., 1., 1., 1.],
         [1., 1., 1., 1., 1.]])
  In [51]: b[1:3,:]
  Out[51]: 
  array([[1., 1., 1., 1., 1.],
         [1., 1., 1., 1., 1.]])
  In [52]: b[1:3,2:4]
  Out[52]: 
  array([[1., 1.],
         [1., 1.]])
  In [53]: b[:,2]
  Out[53]: array([1., 1., 1., 1., 1.])
  In [54]: for i in b.flat:
      ...:     print(i)    
  1.0
  1.0
  1.0
  ....
  ```

- 改变数组形状

  - 使用array.reshape(A)    进行该操作时会生成一个新的数组
  - 使用array.resize(A)         进行该操作时不会生成一个新的数组
  - array.ravel()             返回扁平化的数组（一维数组）

  ```python
  In [55]: c=np.floor(10*np.random.randn(3,4))   #floor函数取不大于x的最大整数
  In [56]: c
  Out[56]: 
  array([[-18.,   6.,  -3.,   2.],
         [ -9.,  19.,  11., -11.],
         [ -1.,  -5.,   1.,  -3.]])
  In [57]: c.reshape(2,6)
  Out[57]: 
  array([[-18.,   6.,  -3.,   2.,  -9.,  19.],
         [ 11., -11.,  -1.,  -5.,   1.,  -3.]])
  In [58]: c.reshape(2,2,3)
  Out[58]: 
  array([[[-18.,   6.,  -3.],
          [  2.,  -9.,  19.]],
  
         [[ 11., -11.,  -1.],
          [ -5.,   1.,  -3.]]])
  In [59]: c.reshape(-1)   #-1表示对应轴的长度未知，自适应长度
  Out[59]: 
  array([-18.,   6.,  -3.,   2.,  -9.,  19.,  11., -11.,  -1.,  -5.,   1.,
          -3.])
  In [60]: c
  Out[60]: 
  array([[-18.,   6.,  -3.,   2.],
         [ -9.,  19.,  11., -11.],
         [ -1.,  -5.,   1.,  -3.]])
  In [61]: c.resize((2,6))
  In [62]: c
  Out[62]: 
  array([[-18.,   6.,  -3.,   2.,  -9.,  19.],
         [ 11., -11.,  -1.,  -5.,   1.,  -3.]])
  In [63]: c.T    #数组转置
  Out[63]: 
  array([[-18.,  11.],
         [  6., -11.],
         [ -3.,  -1.],
         [  2.,  -5.],
         [ -9.,   1.],
         [ 19.,  -3.]])
  In [64]: c.ravel()
  Out[64]: 
  array([-18.,   6.,  -3.,   2.,  -9.,  19.,  11., -11.,  -1.,  -5.,   1.,
          -3.])
  In [65]: c
  Out[65]: 
  array([[-18.,   6.,  -3.,   2.,  -9.,  19.],
         [ 11., -11.,  -1.,  -5.,   1.,  -3.]])
  In [66]: c.reshape(4,-1)  #-1表示对应轴的长度未知，自适应长度
  Out[66]: 
  array([[-18.,   6.,  -3.],
         [  2.,  -9.,  19.],
         [ 11., -11.,  -1.],
         [ -5.,   1.,  -3.]])
  ```

- 组合、拆分数组 

  -  组合使用np.vstack()函数和np,hstack()函数，前者沿第一个轴组合，后者沿第二个轴组合
  -   np.column_stack()和np.row_stack()函数支持将一维数组组合成一个二维数组
  -  拆分使用np.vsplit()和np.hsplit()函数，前者沿第一个轴拆分，后者沿第二个轴拆分
  - 可以使用np.split()更加自由的拆分

  ```python
  In [1]: import numpy as np
  In [2]: a=np.floor(10*np.random.randn(2,2))
  In [3]: b=np.floor(10*np.random.randn(2,2))
  In [4]: a
  Out[4]: 
  array([[21., -4.],
         [ 0., -4.]])
  In [5]: b
  Out[5]: 
  array([[ -1., -10.],
         [ 10., -12.]])
  In [7]: 
  In [7]: np.vstack((a,b))
  Out[7]: 
  array([[ 21.,  -4.],
         [  0.,  -4.],
         [ -1., -10.],
         [ 10., -12.]])
  In [9]: np.hstack((a,b))
  Out[9]: 
  array([[ 21.,  -4.,  -1., -10.],
         [  0.,  -4.,  10., -12.]])
  In [10]: x=np.arange(0,3,1)
  In [11]: y=np.arange(2,5,1)
  In [12]: x
  Out[12]: array([0, 1, 2])
  In [13]: y
  Out[13]: array([2, 3, 4])
  In [15]: np.row_stack((x,y))
  Out[15]: 
  array([[0, 1, 2],
         [2, 3, 4]])
  In [16]: np.column_stack((x,y))
  Out[16]: 
  array([[0, 2],
         [1, 3],
         [2, 4]])
  In [17]: c=np.floor(10*np.random.randn(2,6))
  In [18]: np.hsplit(c,2)
  Out[18]: 
  [array([[-13.,  11.,   2.],
          [ -5.,  15.,   4.]]), array([[-17.,   8.,  -4.],
          [  1.,   6.,  -6.]])]
  In [19]: c
  Out[19]: 
  array([[-13.,  11.,   2., -17.,   8.,  -4.],
         [ -5.,  15.,   4.,   1.,   6.,  -6.]])
  In [20]: np.vsplit(c.reshape(6,2),2)
  Out[20]: 
  [array([[-13.,  11.],
          [  2., -17.],
          [  8.,  -4.]]), array([[-5., 15.],
          [ 4.,  1.],
          [ 6., -6.]])]
  In [21]: np.split(c.reshape(3,4),3)
  Out[21]: 
  [array([[-13.,  11.,   2., -17.]]),
   array([[ 8., -4., -5., 15.]]),
   array([[ 4.,  1.,  6., -6.]])]
  ```

- 广播

  -  使用广播原则可以使数组的运算很方便，如下所示：

  ```python
  In [1]: import numpy as np
  In [2]: a=np.arange(0,10,1)
  In [3]: a
  Out[3]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
  In [4]: a+2
  Out[4]: array([ 2,  3,  4,  5,  6,  7,  8,  9, 10, 11])
  In [5]: a**2
  Out[5]: array([ 0,  1,  4,  9, 16, 25, 36, 49, 64, 81], dtype=int32)
  In [8]: b=np.arange(10,0,-1)
  In [9]: b
  Out[9]: array([10,  9,  8,  7,  6,  5,  4,  3,  2,  1])
  In [10]: a+b
  Out[10]: array([10, 10, 10, 10, 10, 10, 10, 10, 10, 10])
  In [11]: a*b
  Out[11]: array([ 0,  9, 16, 21, 24, 25, 24, 21, 16,  9])
  ```

  

 

​																		**张凡      2020/1/22**
