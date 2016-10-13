---
layout: post
title:  "手把手用上Tushare查看电影票房"
date:   2016-10-13 15:30:50 +0800
category: tech
---

今天看到Crossin分享了一个好玩的Python包，叫Tushare, 居然可以用来看实时电影票房， 立刻吸引了我的兴趣， 所以就花了点时间， 配了一堆Python组件以后终于在自己机器上看到了电影实时票房了。  以后查看哪本电影最卖座就方便咯


#如何安装PiP
* 到 [pip官网](https://pip.pypa.io/en/stable/installing/) 下载 get-pip.py
* 运行 python3 get-pip.py


#安装rpm
* brew install rpm

#安装lxml
安装lxml 原本应该蛮简单的，但是安装的时候报错

`Failed building wheel for lxml `

原因是一些以来包没安装， 其中包括**libxml** 以及 **libxslt**. 于是有用一下命令安装

```
brew install libxml
brew install libxslt
brew link libxml2 --force
brew link libxslt --force
```
最后运行 

```
pip install lxml`
```

终于成功了.  

跑到python 下  `import lxml` 终于没问题了 

#安装Tushare

终于可以装Tushare了

```
pip install tushare
```

装好以后， 开始使用Tushare的强大数据吧。 赶紧看看实时票房怎么样， 听说湄公河行动最近很火。 



```
>>> print(tushare.realtime_boxoffice())
   BoxOffice Irank   MovieName boxPer movieDay sumBoxOffice  \
0    1025.86     1       湄公河行动  44.08       14     78575.20   
1     478.06     2    从你的全世界路过  20.54       15     70015.10   
2     279.15     3          宾虚  12.00        4      1419.05   
3     202.12     4          爵迹   8.69       14     37160.67   
4     190.41     5       王牌逗王牌   8.18       14     24195.40   
5      43.88     6      鲁滨逊漂流记   1.89       10      4152.25   
6      17.87     7        圆梦巨人   0.77        0        17.87   
7      10.82     8  逗鸟外传：萌宝满天飞   0.47       21      7615.02   
8      10.64     9       七月与安生   0.46       30     16637.73   
9      10.06    10        幽灵医院   0.43       14       402.56   
10     58.27    11          其它   1.00        0         0.00   

                   time  
0   2016-10-13 15:12:27  
1   2016-10-13 15:12:27  
2   2016-10-13 15:12:27  
3   2016-10-13 15:12:27  
4   2016-10-13 15:12:27  
5   2016-10-13 15:12:27  
6   2016-10-13 15:12:27  
7   2016-10-13 15:12:27  
8   2016-10-13 15:12:27  
9   2016-10-13 15:12:27  
10  2016-10-13 15:12:27 
```


另外推荐一步到位的安装和数据分析相关的组建就安装 [ANACONDA](https://www.continuum.io/downloads#osx)  




