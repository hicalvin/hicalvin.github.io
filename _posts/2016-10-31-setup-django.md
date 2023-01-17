---
layout: post
title:  "Django起步"
date:   2016-10-31 13:29:50 +0800
category: tech
---

[pic:被解救的姜戈](https://img1.doubanio.com/view/photo/m/public/p1959232369.webp)

*---被解救的姜戈*

今天虽然用了这个海报，但是内容跟它没半毛钱关系， 仅仅只是因为有Django， Python下的Web Framework。 要看电影的观众可以散场了。

# 安装

上手第一步，当然是安装了。 Python 提供了easy_install这个组件可以很方便的安装相关的内容， 其中就包括Django。 由于本身机器上已经装了不同的Python，所以还是先要找到对应正确的Python版本， 可以用下面这个命令： 

```
which python3
```
显示我的python3目录为  
```
/Library/Frameworks/Python.framework/Versions/3.5/bin/python3
```
然后就可以到
```
/Library/Frameworks/Python.framework/Versions/3.5/bin
```
下面找到 **easy_install-3.5**

接下来就简单了，

```
./easy_install-3.5 django
```

就可以完成安装。 当然最好是检查一下版本。 

```
django-admin --version
```
就可以了。 我的是1.10.2 

# 运行

接着我们就可以启动第一个应用了。 

到任何一个打算放置项目的目录， 然后运行 

```
django-admin startproject myapp
```
django就会创建一个初始项目。 这个项目包含一个manage.py文件以及一个目录

接下来进入项目目录运行
```
python3 manage.py runserver
```
就会显示

```
November 01, 2016 - 06:40:43
Django version 1.10.2, using settings 'website.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

然后访问这个url就可以看到 **It worked!** 的页面，就表示成功了。 恭喜哦！！

PS: 如果需要指定Python的版本进行安装， 比如安装Python2.6.x + Django 1.5.10, 那就要按照以下来做:

### Step 1

前往Python官网下载安装包, 就是[这里](https://www.python.org/downloads/mac-osx/)

### Step 2

安装好需要的Python版本以后， 再去安装对应的Django

```
sudo pip install 'https://www.djangoproject.com/download/1.5.10/tarball/'

```

这样就可以了 

***不过看到个帖子，Python2.6顶多只能装1.4的Django， 如果要装跟高版本的Django就只能升级Python到2.7.*** 尝试了一下， 的确在2.6下面没法 ```import django```。   



