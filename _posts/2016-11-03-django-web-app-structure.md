---
layout: post
title:  "Django第二篇"
date:   2016-11-04 23:11:50 +0800
category: tech
---

![被解救的姜戈](http://pic.77ds.net:878/down/wg7777file2/pic/2013040868905137.jpg)

*---被解救的姜戈*

接着上次对姜戈的讲解， 今天把利用Django打造web application的过程做个简单的梳理。 

## Step1

Django的project／app的结构是树状的。 

Project
   |__app
   |__app

所以第一步当然是新建一个project。 manage.py是个相当重要的文件， 可以做各种事情，包括创建项目。 进入到workspace， 然后敲入一下命令就可以创建了。

```
$> django-admin.py startproject mysite
```

## Step2

按照上面图示的顺序，下一步就可以创建app。 app可以视为模块， 就是组成一个web application的各个组件。 进入mysite目录,然后执行:

```
$> python2.7 manage.py startapp module1
```
执行完就可以发现mysite 目录下多了一个module1目录。 app创建完成。 

新创建的app需要在setting.py里的 **INSTALLED_APPS** 下面注册， 这样django才能认识这个新建的app

## Step3

指定数据库类型， 设置就是在 **setting.py** 里面修改**DATABASES** 修改project以及app下面的 **urls.py**, 完成路由。 

## Step4

进入app定义models.py, 这个文件用于定义和DB对应的实体， 其所定义的字段类型和长度都会被同步到数据库。 注意， 最好一次行定义好字段名和类型， 因为后期只能增加， 没法改，要改的话只能删掉重新加。 

```
$> python2.7 manage.py syncdb
```

如果要检测是否完成数据库初始化， 可以进入 **shell**进行检测。 

```
$> python2.7 manage.py shell
>>> from module1.models import ModelA
>>> modela = ModelA.objects.all()
>>> []
```

## Step5

实体定义好以后可以定义 **views** 了，views用于处理Http请求和返回，其中少不了 **template** 的使用。 页面上的写法和AngularJS比较像， 都是在html页面上插入 {{}} 和 {%%} 这样的表述语句 

完成以上几步， 基本上就可以实现前后端的数据传递了。 

**要注意的是， Django在处理url时非常依赖于正则表达式来匹配url，包括url中对参数的传递， 所以在开始使用Django之前， 正则表达式一定要强化。 其实不光是Django， 由于Python经常被用于统计和网络爬虫， 所以正则表达式的重要性同样显而易见。** 

啰嗦了半天，还是那句话， **Practice Makes Perfect.**







