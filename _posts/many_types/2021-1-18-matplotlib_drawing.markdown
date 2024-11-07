---
title: "Matplot Drawing Parameters"
subtitle: "Pandas基础使用，常用函数、操作与读写"
layout: post
author: "zelin"
header-style: text
catalog: true
tags:
  - Python
  - Programming
---

# Draw lineage tree experiment

## CMAP

```
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(100)
y = x
t = list(np.arange(5,10,0.1))+list(np.arange(5,6,0.02))
plt.scatter(x, y, c=t,cmap=plt.get_cmap('hsv'))
plt.show()
```
**TRY THE CODE ABOVE YOURSELF, I AM LAZY TO PUT THE FIGURE HERE**

## color collection
see the picture and code, no need to talk.

['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd', '#8c564b', '#e377c2', '#7f7f7f', '#bcbd22', '#17becf']
down to up:

**蓝色，橙色，绿色，红色，紫色，褐色，粉色，灰色，灰绿，灰蓝**

![showing color](https://github.com/chiellini/pictures_sources/raw/master/WeChat%20Image_20210118174655.png)


```
plt.scatter(x=[20,20,20,20,20,22,22,22,22],y=[2,3,4,5,6,2,3,4,6],marker='s',s=10)

plt.scatter(x=[2,2,2,2,222,222,222,222],y=[2,3,4,6,2,3,4,6],marker='s',s=10,c='red')

plt.scatter(x=4,y=6,marker='s',s=10,c='#1f77b4')
plt.scatter(x=4,y=7,marker='s',s=10,c='#ff7f0e')
plt.scatter(x=4,y=8,marker='s',s=10,c='#2ca02c')
plt.scatter(x=4,y=9,marker='s',s=10,c='#d62728')
plt.scatter(x=4,y=10,marker='s',s=10,c='#9467bd')
plt.scatter(x=4,y=11,marker='s',s=10,c='#8c564b')
plt.scatter(x=4,y=12,marker='s',s=10,c='#e377c2')
plt.scatter(x=4,y=13,marker='s',s=10,c='#7f7f7f')
plt.scatter(x=4,y=14,marker='s',s=10,c='#bcbd22')
plt.scatter(x=4,y=15,marker='s',s=10,c='#17becf')

plt.xlim(0,400)
plt.ylim(0,180)

plt.show()
```


