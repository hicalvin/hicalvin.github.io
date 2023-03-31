---
layout: post
title:  "搭建本地Python开发环境和Swagger Editor"
date:   2019-12-20 14:42:50 +0800
category: tech
---

太久没有写代码了，这真的不好...

所以介绍一个可以记录自己写代码的时间的小工具 - [WakaTime](!https://wakatime.com/dashboard)

根据网站介绍，在PyCharm上面安装Waka的插件，就可以顺利的记录起自己在过去7天的编码时间了。而且强大的是不仅Pycharm，基本上只要你想的到的IDE，都提供了相应的插件集成，所以无论用那个IDE，只要想记录，都可以用Wakatime。 在这里感谢Summer老大的推荐。 

至于报表，也非常详尽，包括语言， IDE，每天时间段等等，可以说是应有尽有。 对于一个工程师，当然想知道自己的代码时间如何花费，而这个工具真的是比自己更加了解你自己。 

#### 本地环境恢复

本地的环境因为一次系统升级，导致之前的开发环境配置荡然无存，只能重新搭建。 一路碰到各种问题，做个记录，便于以后再次尝试。

```
brew install python3
```



错误信息

```
could not lock config file .git/config: Permission denied
```

解决方法

```
sudo chgrp -R admin /usr/local
sudo chmod -R g+w /usr/local
```

重新安装 Homebrew 

```
brew update
```



#### 安装Swagger Editor

1. Install node.js  including npm, using **brew install node**

2. install *http-server*, using **npm install -g http-server**

3. visit [Swagger Editor](!https://github.com/swagger-api/swagger-editor/releases) to download source code

4. After installing *http-server*, it will create soft link of */usr/local/bin/hs -> /usr/local/lib/node_modules/http-server/bin/http-server* by default

5. Start Swagger Editor locally by below commands

   ```
   CALVINY-M-M1S5:~ calviny$ /usr/local/bin/hs /Users/calviny/Documents/01_work/04_tools/swagger-editor-3.7.1
   Starting up http-server, serving /Users/calviny/Documents/01_work/04_tools/swagger-editor-3.7.1
   Available on:
     http://127.0.0.1:8080
     http://10.140.213.59:8080
   Hit CTRL-C to stop the server
   ```

6. After visiting **http://localhost:8080**, by default there will be a pet store to start. Leveraging that will speed the defintiion of your own API specification, and then you can export to a .yaml file for offline communication



#### 如何设计RESTful API

强烈推荐一篇非常极客的文章 [RESTful API Design — Step By Step Guide](https://hackernoon.com/restful-api-design-step-by-step-guide-2f2c9f9fcdbf)

里面一句非常有震撼力的话是  **Anyone who doesn’t do this will be fired**

对于需要设计API的开发人员，可以参照 [OpenaPI Specification](!We need to always keep in mind that the API design should be full proof and fool proof.)

- [brew install python3 报错](!Mac-brew报错error: could not lock config file .git/config: Permission denied)
- [Module Not Found](https://jonathansoma.com/course/foundations-2021/jupyter-module-not-found/)

