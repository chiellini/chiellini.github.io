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

* DataFrame(data,columns=name[],index=name[])

* 获取一列，获得一个Series
  * frame[(name)] or
  * frame.(name)

* 修改一列
  * 直接赋值会全部变成常数。 or
  * frame['(name)']=np.arrage(5.)
  * 也可以创建一个Series赋值给frame的某一列

* 直接给不存在的列赋值，会自动创建

* 删除某一列：
  * del frame['(name)']

* frame.T 即列和index（索引）变换

* 取某一个行：
  * frame.ix['(name)']
