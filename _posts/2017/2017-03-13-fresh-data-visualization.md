---
layout: post
title:  "鲜活的数据"
date:   2017-03-13 16:10:50 +0800
category: tech
---

![鲜活的数据](http://www.ituring.com.cn/bookcover/819.776.big.jpg)

关于数据可视化，在拥有了足够以及可信的数据以后，剩下的就是如何展现了。 先分享几个python的几个插件，因为python用来处理数据实在是太强大了。 

- [mpld3](http://mpld3.github.io/index.html)
- [bokeh](http://bokeh.pydata.org/en/latest/)

## 有关时间趋势的可视化

时间数据分为离散时间和延续时间。 离散时间数据来自于某个具体的时间点或者时段， 可能的数值也是有限的。 类似温度这样的数据则是延续性的。 

### 柱形图

处理的数据都是正数时，请永远让柱形图的数值轴从0开始，否则会让人们难以从视觉上比较各柱形的高度。 

***站在读者的角度来设计数据图表。 好的数据设计可以帮助读者更清楚的理解整个故事***

### 圆点

这种类型的图表通常叫散点图(scatterplot)， 占据空间少， 能更好的体现出“流”的感觉，也可以用来表现非时间数据。 


### 折线图

如果数据长时间停留在一个数值上， 适合用阶梯图。 


##  有关比例的可视化

对于比例，通常会寻求三件事情： 最大值， 最小值和总体分布。 最大最小很简单，将数据从大到小排列，两头就是最大值和最小值。 至于比例， 最简单的是总和为1或者100%。 

### 饼图/面包圈图

饼图的缺陷是不够精确。 可以不要分太多类别。 

很多时候，面包圈的中心都用于放置标签或其他内容

### 堆叠柱形图

与禊形相比， 长度更容易比较，所以堆叠柱形图用来比较

### 板块层级图 (treemap)

基于面积的可视化方案

### 堆叠面积图

带时间属性的比例

## 有关关系的可视化

明确你要讲述的故事的重点， 然后在图表设计中有意强化这些地方。 但请不要扭曲事实。

### 气泡图

用R运行一下block， 可以看看2005年美国各州的犯罪率
```
>crime <- read.csv("http://datasets.flowingdata.com/crimeRatesByState2005.tsv", header=TRUE, sep="\t")
>radius <- sqrt(crime$population/pi)
>symbols(crime$murder, crime$burglary, circles=radius, inches=0.35, fg="white", bg="red", xlab="Murder Rate", ylab="Burglary Rate")
```



### 分布

- 平均数（mean）  	将所有数据点相加然后除以数据点的个数。 
- 中位数（median）	将所有数据从小到大排列， 然后找出位于最中间的那个数据点	
- 众数（mode）		所有数据点中出现频率最高的那个数字


### 切尔诺夫脸谱图

通过脸部特征的长宽大小来代表数据

```
>library(aplpack)
>bball <- read.csv("http://datasets.flowingdata.com/ppg2008.csv", header=TRUE)
>faces(bball[,2:16], ncolors=0)
```


TIPS

- [热力图调色板](http://colorbrewer2.org/) 

## 有关空间关系的可视化

### 地图

R有非常强大的地图展现功能

先要安装地图所需要的包。 在install后要在弹出框内选择maps
```
r> install.packages()
r> library("maps")
r> map()
```

就可以展现出世界地图了。 但是默认是美国，所以如果要展现祖国， 还要安装和加载 mapdata.

```
r> install.packages()
r> library(mapdata)
r> map("china")
```

对地图的使用可以参考[R时代，你要怎样画地图？](https://cos.name/2013/01/drawing-map-in-r-era/) 的这篇博客。 








