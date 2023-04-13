---
layout: post
title:  "生成式AI的崛起04：程序员的'福音'"
date:   2023-04-13 21:29:50 +0800
category: tech
---

面多如此多的chatgpt应用场景，首先遭殃的大概就是发明了chatgpt的软件工程师自己了， 有一句话说的好：

> 走自己的路，让自己无路可走

真是悲摧的程序员。

目前的chatgpt已经可以毫不费力的通过自然语言生成代码。下面就是我曾经在学习Python的画图功能时尝试过的例子:

~~~python

import numpy as np
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt


# Input data
x = np.array([2019, 2020, 2021, 2022]).reshape((-1, 1))
y = np.array([320000, 459000, 543000, 349000])

# Create a linear regression object
model = LinearRegression()

# Fit the model to the data
model.fit(x, y)

# Predict the population of x city in 2023
year_2023 = np.array([2023]).reshape((-1, 1))
predicted_pop_2023 = model.predict(year_2023)

print("Predicted population of x city in 2023:", int(predicted_pop_2023))

# Input data
years = [2019, 2020, 2021, 2022, 2023]
population = [320000, 459000, 543000, 349000, int(predicted_pop_2023)]

# Create the plot
plt.plot(years, population)

# Add labels and title
plt.xlabel("Year")
plt.ylabel("Population")
plt.title("Population Trend of x City (2019-2023)")

# Show the plot
plt.show()

~~~

完全是由下面这个prompt生成的：

~~~shell
I have below data to tell the population of x city. Can you use python to plot the trend of year 2023?

2019, 320,000
2020, 459,000
2021, 543,000
2022, 349,000

~~~

其他的类似文本转化，正则表达式生成等等就更是不在话下了。

### 示例1 - 文本转化成Markdown格式

~~~shell
Prompt: 

Please change below markdown list:

- XXX v15.2.0: releaseNotes/202109.md
- XXX v15.3.0: releaseNotes/202110.md
- XXX v15.4.0: releaseNotes/202111.md
- XXX v16.0.0: releaseNotes/202112.md

into markdown list with hyperlink like below:

- [MCT v15.0.0](olderReleases/202107.md)

and output as markdown source
~~~

转化结果：

~~~shell
- [XXX v15.2.0](releaseNotes/202109.md)
- [XXX v15.3.0](releaseNotes/202110.md)
- [XXX v15.4.0](releaseNotes/202111.md)
- [XXX v16.0.0](releaseNotes/202112.md)
- [XXX v16.0.0](releaseNotes/202201.md)
~~~

### 示例2 - 正则剔除html标签

~~~shell 

Prompt:


 <tr>
          <td id="L8617" class="blob-num js-line-number js-code-nav-line-number js-blob-rnum" data-line-number="8617"></td>
          <td id="LC8617" class="blob-code blob-code-inner js-file-line">令狐冲道：“你也坏得够了，
</td>
        </tr>
        <tr>
          <td id="L8618" class="blob-num js-line-number js-code-nav-line-number js-blob-rnum" data-line-number="8618"></td>
          <td id="LC8618" class="blob-code blob-code-inner js-file-line">令狐冲道：“啊，是了
</td>

Please use regular expression to remove all the html tags and only leave chinese content in upper block

~~~

~~~python
# ChatGPT:

import re

html_text = """
<tr>
  <td id="L8617" class="blob-num js-line-number js-code-nav-line-number js-blob-rnum" data-line-number="8617"></td>
  <td id="LC8617" class="blob-code blob-code-inner js-file-line">令狐冲道：“你也坏得够了，
</td>
</tr>
<tr>
  <td id="L8618" class="blob-num js-line-number js-code-nav-line-number js-blob-rnum" data-line-number="8618"></td>
  <td id="LC8618" class="blob-code blob-code-inner js-file-line">令狐冲道：“啊，是了
</td>
"""

pattern = re.compile(r'<[^>]+>')
chinese_text = re.sub(pattern, '', html_text).strip()

print(chinese_text)

# Output:
#令狐冲道：“你也坏得够了，
#令狐冲道：“啊，是了

~~~

除了ChatGPT，还有其他一些快速生成代码的工具。其中Github Copilot和tabnine插件非常受欢迎，尤其是tabnine，因为它有免费版本可用，虽然功能有所限制，但也已经可以体验到非常好的开发效率提升。今天我还发现了一个专为开发人员设计的类chatgpt工具 - phind.com。它不需要任何注册认证，可以直接在网页上使用，与ChatGPT非常相似。此外，在页面右侧还会出现网页链接，这极大地提高了开发效率，简直就像集成了Google和ChatGPT的利器。我尝试问了它关于Go和Java的性能比较，甚至还提出了“为什么Go比Java慢”的问题，但它居然没有上当，相反地，它告诉我实际上Go会更快。

我还让它写了一段针对面向对象的Go和Java代码。它不仅写得非常清晰，而且还给出了这两个语言关于这方面知识的网站链接，为我提供了额外的帮助。正如它自己在首页所宣称的，“The AI search engine for developers”，这个工具名副其实，真的为开发人员带来了很多的便利。


### Reference

- [phind](https://www.phind.com/)
- [tabnine](https://www.tabnine.com/)