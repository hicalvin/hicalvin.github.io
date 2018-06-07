---
layout: post
title:  "Touch of Aansible"
date:   2018-06-07 21:56:50 +0800
category: tech
---
![Ansible](http://static.open-open.com/lib/uploadImg/20161129/20161129150713_902.jpg)


之前在和另外的一个团队合作的时候就听说了Ansible，当时就被它简单的批量操作整的心痒痒。 今天遇到一个场景，需要拷贝一个文件到20台Linux机器上。作为一个Engineer，当然不能通过敲20遍相同的Linux命令来解决问题了，所以想到了Ansible。 

[Ansible](https://docs.ansible.com/) 默认通过SSH协议管理机器。如果用本机管理一组机器， 只要在本机上安装好Ansible，就可以开始管理远程机器了，不需要在远端机器安装任何东西，非常方便。 

使用Ansible的前提是安装Python。有了pip以后，就可以用 ```pip install --upgrade ansible``` 来安装ansible。

安装好了以后， 需要有个配置文件来制定默认使用什么协议联接远端机器。 文件名是ansible.cfg, 可以到 [github](https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg). (以后是不是要到Gitlab 找了，因为Github居然被 M$ 买了。 -_-|||

完了以后，就缺配置一组机器了。 这个文件叫 Inventory.  格式类似于这样：

```
[centos7]
10.224.244.58
10.252.223.47
```

中括号里面的是组名，下面是这组对应的机器。 不需要任何后缀名， 只是一个文本， 不过这个文件地址要在 **ansible.cfg** 里面指明:

```
[defaults]
# some basic default values...
inventory      = ./inventory
```

有了Inventory文件后就可以开始操作了。 如果只是对这组机器运行单条命令就可以用了

```
> ansible centos7 -u calviny --ask-pass --sudo --ask-sudo-pass -m copy -a "src=/my_path/file_a.jmx dest=/tmp/"

```

上面的命令是要求提示两次密码输入，分别是用本地用户连以及sudo的时候。 如果密码输入没错，应该就会返回ping的成功结果：

```
10.252.57.21 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

但是如果我们需要好几条命令来完成一个复杂任务的时候，就需要用到它的最重要的功能： **Playbook** 这基本上可以看作是一个剧本， 让Ansible按照剧本一步步执行并清晰的告诉我们进行到哪一步，而且是并行哦～～ Playbook是通过制定一个Yaml文件来的。 yaml文件的格式和Json非常相似， 非常易读。

```
---
- hosts: webservers
  remote_user: root
  tasks:
    - name: test connection
      ping:
      remote_user: yourname
```

等到你把想做的任务写好以后，就可以运行 

```
> ansible-playbook my_tasks.yml

```
来做任何你想做的事情了。 

YEAH!!!

 