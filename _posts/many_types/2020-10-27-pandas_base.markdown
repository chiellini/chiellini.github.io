---
title: "Pandas基础使用"
subtitle: "Pandas基础使用，常用函数、操作与读写"
layout: post
author: "zelin"
header-style: text
catalog: true
tags:
  - Python
  - 软件基础
  - Programming
---

# Pandas基础使用
**https://blog.csdn.net/u011746554/article/details/74911215**

## 功能

* 数据结构可对齐。
* 集成时间序列功能。
* 对轴求和。
* 缺失数据（设置为零or what）。 
* SQL关系型数据库中的常见功能。

## 常用类

### Series 

* Series常用

  * obj=Series(value[],index=index[])
  * obj.values
  * obj.index

* 可以通過索引取值：obj['index1']
  
* 可以直接使用numpy的方法：np.exp(obj)

* 直接用字典生成Series:
  * obj=Series(dict{})

* pd.isnull(obj)
* pd.notnull(obj)

* obj1+obj2 不同索引，缺失的，都可以直接得出結果，像excel一樣

* Series和其index都可以命名，name

### DataFrame

DataFrame使用二維塊來保存數據的。

* 可以使用等長的列表或者Numpy数组

* DataFrame(columns=name\[\],index=name\[\])

#### 列

* 获取一列，获得一个Series
  * df[(name)] or
  * df.(name)

* 修改一列
  * 直接赋值会全部变成常数。 or
  * df['(name)']=np.arrage(5.)
  * 也可以创建一个Series赋值给frame的某一列

* 直接给不存在的列赋值，会自动创建

* 删除某一列：
  * del df['(name)']
  * df.drop(index='name',inplace=True)

* df.T 即列和index（索引）变换

#### 行
* 创建行：
  * df.loc['name']=list()

* 取某一个行：
  * df.ix['(name)']
  * df.loc['name']

#### little tips

**https://blog.csdn.net/u011746554/article/details/74911215**
* 前几行后者后几行
  * df.head(6)表示显示前6行数据，若head()中不带参数则会显示全部数据。
  * df.tail(6)表示显示后6行数据，若tail()中不带参数则也会显示全部数据。

* 查看DataFrame的index，columns以及values
  * a.index ; a.columns ; a.values 即可

* describe()函数对于数据的快速统计汇总
  * a.describe()对每一列数据进行统计，包括计数，均值，std，各个分位数等。

https://www.cnblogs.com/wodexk/p/10316793.html
* loc和iloc 可以更换单行、单列、多行、多列的值
  * df1.loc[0,'age']=25      先用loc找到要更改的值，再用赋值（=）的方法实现更换值
  * df1.iloc[0,2]=25       iloc：用索引位置来查找

* at 、iat只能更换单个值
  * df1.iat[0,2]=25      # iat 用来取某个单值,只能用数字 as index
  * df1.at[0,'age']=25         # at 用来取某个单值,只能用index和columns索引名称


### Moreover

* dataframe.round() 保留几位小数
* df.astype('float64') make NaN as 0, 否则round不work

https://blog.csdn.net/akenseren/article/details/80711895
https://www.cnblogs.com/wuzhiblog/p/python_new_row_or_col.html
* 行和，纵向求和
  * df.loc['Cluster_sum'] = df.apply(lambda x: x.sum(), axis=0) 
* 列和，横向求和
  * df['Cluster_sum'] = df.apply(lambda x: x.sum(), axis=1)
  * df['col3'] = df.apply(lambda x: x['col1'] + 2 * x['col2'], axis=1)  

* pd.read_csv
  * the first columns index, may become unknown1 column.


