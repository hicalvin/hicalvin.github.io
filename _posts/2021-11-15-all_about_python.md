---
layout: post
title:  "Python Bootcamp"
date:   2021-11-15 18:04:50 +0800
category: tech
---

- Compiled vs Interpreted
  - Compiled: Code -> Machine Code -> Ready to Execute
  - Interpreted: Code -> Ready to Execute -> Interpreted -> Machine Code

- Steps to install Python in MacOS
  - Upgrade Xcode
  - xcode-select --install
  - Using Homebrew to install by visiting brew.sh
  - brew install python

- [How to use Virtual Env](https://py.eastlakeside.cn/book/ProgrammerTools/virtual_environment.html)
- [How to debug in Python](https://py.eastlakeside.cn/book/ProgrammerTools/debugging.html)
- [How to use *Open* method](https://py.eastlakeside.cn/book/Syntax/open_func.html)

```python
f = open('photo.jpg', 'r+')
jpgdata = f.read()
f.close()

```

This is not a good way. You'd better use [*with*](https://blog.csdn.net/u012609509/article/details/72911564) to *Open* a file

- [How to use *args and **kwargs](https://py.eastlakeside.cn/book/Syntax/args_kwargs.html)
  - *args is used for non-keywords arguments

    ```python
    def test_var_args(f_arg, *argv):
    print("first normal arg:", f_arg)
    for arg in argv:
        print("another arg through *argv:", arg)

    test_var_args('yasoob', 'python', 'eggs', 'test')
    ```

  - **kwargs is used for keywords arguments

    ```python 
    def greet_me(**kwargs):
    for key, value in kwargs.items():
        print("{0} = {1}".format(key, value))

    >>> greet_me(name="yasoob")
    name = yasoob
    ```
  
  - [How to use regular expression](https://docs.python.org/3/library/re.html)

### Resource

- [Python进阶](https://py.eastlakeside.cn/)
- [用 jupytertheme 美化Jupyter Notebook, 眼睛轻松多了](https://zhuanlan.zhihu.com/p/46242116)
