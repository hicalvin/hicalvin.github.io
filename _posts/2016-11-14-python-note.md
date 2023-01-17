---
layout: post
title:  "Python 玩转数据"
date:   2016-11-14 23:45:50 +0800
category: tech
---

![Python](https://www.python.org/static/community_logos/python-logo-master-v3-TM-flattened.png)

*---Python*

Python 的各种类库为快速处理数据提供了诸多便利， 其中包括以下几个：

[SciPy](http://scipy.org/) 下包含的Matplotlib 用于绘制2D图， NumPy 用于科学计算， 以及pandas用于数据分析。 

例子就是用其中的 pandas 和 matplotlib 来抓取Cisco在过去一年内的股票情况  

```
from matplotlib.finance import quotes_historical_yahoo_ohlc
from datetime import date
import pandas as pd

today= date.today()
start=(today.year-1, today.month, today.day)
quotes = quotes_historical_yahoo_ohlc('CSCO', start, today)
fields = ['date','open','high','low','close','volume']

list1 = []
for i in range(0, len(quotes)):
    x = date.fromordinal(int(quotes[i][0]))
    y = x.strftime('%Y-%m-%d')
    list1.append(y)
    
quotesdf = pd.DataFrame(quotes, columns = fields)
quotesdf['trade date'] = pd.Series(list1)
quotesdf = quotesdf.drop(['date'], axis=1)

print quotesdf
```

结果如下： 

```
          open       high        low      close    volume  trade date
0    25.899843  26.354058  25.783874  25.909507  30490200  2015-11-17
1    26.093126  26.247752  25.832194  26.209096  27015700  2015-11-18
2    26.189767  26.721293  26.141445  26.450699  27417400  2015-11-19
3    26.663308  26.846927  26.537674  26.643980  26502800  2015-11-20
4    26.721294  26.904912  26.421706  26.508683  24684600  2015-11-23
5    26.334730  26.518349  26.093127  26.354058  32859200  2015-11-24
6    26.402377  26.470025  26.093125  26.325064  22472500  2015-11-25
7    26.334728  26.557003  26.325064  26.402377   9532300  2015-11-27
8    26.421706  26.557004  26.286409  26.334729  30736700  2015-11-30
9    26.286409  26.721293  26.286409  26.643980  31406300  2015-12-01
10   26.566668  26.962897  26.450699  26.518348  29178200  2015-12-02
11   26.701964  26.759951  25.919171  26.044806  25783800  2015-12-03
12   26.044806  26.624651  26.044806  26.557003  28143700  2015-12-04
13   26.634316  26.634316  26.344393  26.566668  15350200  2015-12-07
14   26.257415  26.373386  26.112453  26.238087  18635700  2015-12-08
15   26.054468  26.431369  25.764545  25.832194  24127400  2015-12-09
16   25.841859  26.131783  25.764546  25.870851  23305200  2015-12-10
17   25.600256  25.600256  25.252347  25.281340  34295700  2015-12-11
18   25.416636  25.629247  25.088056  25.600255  32642100  2015-12-14
19   25.822529  26.199432  25.716226  25.948164  30393700  2015-12-15
20   26.093125  26.373386  25.783873  26.325064  22731500   2015-12-30
..         ...        ...        ...        ...       ...         ...
222  31.410000  31.680000  31.410000  31.590000  11808600  2016-10-05
223  31.570000  31.629999  31.209999  31.480000  14077100    2016-11-08
247  31.040001  31.490000  30.700001  31.360001  38428900  2016-11-09
248  31.410000  31.760000  30.809999  31.000000  38345000  2016-11-10
249  30.930000  31.469999  30.920000  31.360001  23109200  2016-11-11
250  31.430000  31.670000  31.350000  31.370001  22912700  2016-11-14
251  31.270000  31.850000  31.270000  31.700001  24118800  2016-11-15

[252 rows x 6 columns]

```
到这里基本上已经拿到了过去一年思科的全部数据， 但是数字看了太烦了， 要好看还是得用图表， 于是再花了点时间，把图给整出来了。 代码如下：

```
from matplotlib.finance import quotes_historical_yahoo_ohlc
import matplotlib.pyplot as plt
from datetime import date
import pandas as pd


today= date.today()
start=(today.year-1, today.month, today.day)
quotes = quotes_historical_yahoo_ohlc('CSCO', start, today)
fields = ['date','open','high','low','close','volume']

list1 = []
for i in range(0, len(quotes)):
    x = date.fromordinal(int(quotes[i][0]))
    y = x.strftime('%Y-%m-%d')
    list1.append(y)
    
quotesdf = pd.DataFrame(quotes, columns = fields)
quotesdf['trade date'] = pd.Series(list1)
quotesdf = quotesdf.drop(['date'], axis=1)

fig = plt.figure(1) # 创建图表1
ax = fig.add_subplot(111, frameon=False)

#处理x轴的显示与间隔的关系，把刻度转化成时间
alist = range(0, len(quotesdf['close']), 50)
tlist = []
for a in alist:
    print a
    t = quotesdf['trade date'][a]
    tlist.append(t)

ax.set_xticks(range(0, len(quotesdf['close']), 50))
ax.set_xticklabels(tlist)


plt.plot(range(0, len(quotesdf['close'])), quotesdf['close'])
plt.xdata = (quotesdf['trade date'])
plt.show()

```
于是就看到了漂亮的折线图： 

![折线图](/img/posts/20161114-python-csco_stock.png)