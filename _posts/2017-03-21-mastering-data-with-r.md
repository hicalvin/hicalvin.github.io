---
layout: post
title:  "R语言初体验"
date:   2017-03-21 22:03:50 +0800
category: tech
---

![R语言](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/R_logo.svg/724px-R_logo.svg.png)

既然入了数据分析的坑，那就让我在坑里耍耍吧。 

尝试了几天R语言， 发现它在数据分析领域中实在太便利了， 因为强大的开发库，所以做数据分析，统计甚至绘图都手到擒来。 工欲善其事，必先利其器。有了这么好用的工具， 做起事情来当然会事半功倍。 Python作为我的另外一个钟爱的语言， 虽然在数据分析领域也驾轻就熟， 但是和R比起来， 还是显得稍逊一筹。 不过Python的强大在于包罗万象，所以还是得说，术业有专攻吧。 

先来抓个数据玩玩。 hglights 包括了2011年从休斯顿起飞的航班的部分数据

```
>install.packages('hflights')
>write.csv(hflights, 'hflights.csv', row.names=FALSE)
```

于是这些数据就会被写成csv文件而存在名为'hflights.csv' 文件中。 那这个文件跑哪儿去了呢？ 这需要看看默认的文件目录。 

```
>getwd()
```


如果要看看读入文件的耗时， 则可以用

```
system.time(read.csv('hflights.csv'))
```
你也可以和linux下的一些命令来进行比较

```
>system.time(system('cat hflights.csv', intern=TRUE))

```
我在本机比较了这两种方法， 结果如下：

```
> system.time(system('cat hflights.csv', intern=TRUE))
   user  system elapsed 
  0.129   0.013   0.134 
> system.time(read.csv('hflights.csv'))
   user  system elapsed 
  2.564   0.055   2.600 
```

在读取文件数据时直接加入条件，从而只获取符合条件的数据，这在R里面轻而易举就可以做到,不过需要安装 'sqldf'

```
>library(sqldf)
>df <- read.csv.sql('hflights.csv', sql="select * from file where Dest = '\"BNA\"'")

```
想尝试直接从网站下载csv数据， 但是却碰壁了

```
> str(read.csv('http://opengeocode.org/download/CCurls.txt'))
'data.frame':	117 obs. of  1 variable:
 $ X..DOCTYPE.html.: Factor w/ 89 levels "                        Contact your hosting provider for more information.",..: 88 76 79 78 81 80 82 84 77 83 ...

```
换个网站数据，然后试试强大的RCurl包。 

```
> library(RCurl)
> url <- 'https://data.consumerfinance.gov/api/views/x94z-ydhh/rows.csv?accessType=DOWNLOAD'
> df <- read.csv(text = getURL(url))
> str(df)
```












