---
layout:     post
title:      "数据分析与多项式计算"
subtitle:   " \" matlab learning\""
date:       2019-08-22 11:01:00
author:     "张凡"
header-img: "https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab.jpg"
catalog: true
tags:
    - Matlab
---

# 数据分析与多项式计算

-----

## 一、数据统计分析

------

#### 1.1 求矩阵的最大值与最小值

- max() ：求向量或者矩阵的最大元素

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_max1.png)

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_max2.png)

- min()：求向量或者矩阵的最小元素

  > 与max()函数调用格式相同

#### 1.2  求矩阵的平均值和中值

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_mean.png)

- mean()：求算数平均值

- mediam()：求中值

  > 与max()函数调用格式相同

#### 1.3 求和与求积

- sum()：求和函数

- prod()：求积函数

  > 与max()函数调用格式相同

#### 1.4 累加和与累乘积

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_leijieha.png)

- cumsum()：累加和函数
- cumprod()：累乘积函数

#### 1.5 标准差与相关系数

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_biaozhuncha.png)

> 其中S1称为**样本标准差**，S1称为**总体标准差**

- std()：计算标准差函数

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_biaozhuncha_d.png)

- corrcoef()：相关系数函数

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_corrcoef.png)

#### 1.6 排序

- sort(): 排序函数

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_sort.png)



## 二、多项式计算

------

#### 2.1 多项式的表示

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_duoxiangshi_b.png)

#### 2.2 多项式四则运算

​	多项式加减运算对应向量直接相加减就可以了，乘除则使用下图中的函数。

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_duoxiangshi_jj.png)

​	![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_duoxiangshi_c.png)

#### 2.3 多项式求导

- polyder()：多项式求导函数

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_qiudao.png)

#### 2.4 多项式的求值

- polyval(p,x)：代数多项式求值

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_val.png)

- polyvalm(p,x)：矩阵多项式求值

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_valm.png)

#### 2.5 多项式求根

- roots(p)：多项式求根函数。其中p是多项式系数向量
- 若已知多项式的全部根，则可以用poly函数建立起该多项式，其调用格式为：`p=ploy(x)`



## 三、数据插值

------

#### 3.1 计算机制

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_chazhi.png)

#### 3.2 插值函数

- interp1()：一维插值函数

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_interp1.png)

  - 其中method参数用于指定插值的计算方法，常用的插值方法有下图中所示的四种：

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_interp_m1.png)

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_interp_m2.png)

  - 四种方法的比较

    - 线形插值和最近点插值方法比较简单，插值方法的计算量与样本点n无关。n越大，误差越小。

    - 三次埃尔比特插值和三次样条插值都能保证曲线的光滑性，相比较而言，三次埃尔比特插值具有保形性，而三次样条插值要求其二阶导数也连续，所以插值的形态更好。

- interp2()：二维插值函数

  ![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/matlab_interp2.png)

  **interp2() 插值函数的 method 方法与一维插值类似。**

