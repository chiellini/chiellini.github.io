---
title: "常用statistical learning concept and methods"
subtitle: "PRINCIPAL COMPONENT ANALYSIS"
layout: post
author: "zelin"
header-style: text
catalog: true
tags:
  - Concept
---

# Statistical Learning

## Concept

* mean 数学期望（均值）


以下三者的区别：https://www.cnblogs.com/bigmonkey/p/11097322.html
* variance 方差
  * https://en.wikipedia.org/wiki/Variance

* root-mean-square deviation, root-mean-square error, RMSD, RMSE（均方差，标准差）
  * 开根与原数据差别大，开根之后更利于观察
* 

## Non-singular A matrix Inverse and Singular A matrix minimun solution

```
import numpy.linalg as la
import scipy.linalg as spla

import numpy as np


A=np.random.rand(10,10)
x_real=np.arange(1,11)
b=A.dot(x_real)

print(A,x_real,b)

Q, R = la.qr(A)


print(Q,R)

qr_x=spla.solve_triangular(R, Q.T.dot(b),lower=False)

print(qr_x)

inverse_component_matrix = np.linalg.inv(A)

print(inverse_component_matrix.dot(b))
```

## PCA

X是去平均值的
Consider an nxp data matrix, X, with column-wise zero empirical mean (the sample mean of each column has been shifted to zero), where each of the n rows represents a different repetition of the experiment, and each of the p columns gives a particular kind of feature (say, the results from a particular sensor).


用于降维。找到一个方向上，这个方向上all samples' variation最大，即该方向上所有数据点（observations)projection的方差最大。大的方差意味能表达更多的信息。

### 定义

*reference*


https://zh.wikipedia.org/wiki/%E4%B8%BB%E6%88%90%E5%88%86%E5%88%86%E6%9E%90


