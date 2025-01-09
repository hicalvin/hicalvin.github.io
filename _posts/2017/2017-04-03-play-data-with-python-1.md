---
layout: post
title:  "用Python玩数据"
date:   2017-04-03 16:39:50 +0800
category: tech
---

![Big Data](https://www.packtpub.com/sites/default/files/Article-Images/3450_12_01.png)

## Series

```
>>> from pandas import Series
>>> s3 = Series([3, 9, 4, 7], index=['a', 'b', 'c', 'd'])
>>> s3
a    3
b    9
c    4
d    7
dtype: int64
>>> s3 * 5
a    15
b    45
c    20
d    35
dtype: int64
>>> s3
a    3
b    9
c    4
d    7
```


## DataFrame

```
>>> from pandas import DataFrame
>>> data = {"name":["yahoo", "google", "facebook"], "marks":[200, 400, 800], "price":[9, 3, 7]}
>>> data
{'price': [9, 3, 7], 'name': ['yahoo', 'google', 'facebook'], 'marks': [200, 400, 800]}
>>> f1 = DataFrame(data)
>>> f1
   marks      name  price
0    200     yahoo      9
1    400    google      3
2    800  facebook      7
>>> f2 = DataFrame(data, columns=['name','price', 'marks'])
>>> f2
       name  price  marks
0     yahoo      9    200
1    google      3    400
2  facebook      7    800
>>> 
```











