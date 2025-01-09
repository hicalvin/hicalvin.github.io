---
layout: post
title:  "用词云的方式展示十九大报告"
date:   2017-10-19 10:12:50 +0800
category: tech
---
![词云图](/img/posts/20171019-wordcloud.jpg)

### 源码

```

import jieba
from jieba.analyse import extract_tags
from collections import Counter
from wordcloud import WordCloud
import matplotlib.pyplot as plt

def stopwordslist(filepath):
    stopwords = [line.strip() for line in open(filepath, 'r', encoding='utf-8').readlines()]
    return stopwords

# 对句子去除停用词
def movestopwords(sentence):
    stopwords = stopwordslist('lib/stop_words.txt')  # 这里加载停用词的路径
    outstr = ''
    for word in sentence:
        if word not in stopwords:
            if word != '\t'and'\n':
                outstr += word
                # outstr += " "
    return outstr

text = open('report.txt', 'r').read()
text = re.sub("[^\u4e00-\u9fa5]", "", text). # 中文的UTF8代码区间
filtered_content = movestopwords(text)


result = jieba.lcut(filtered_content)
count_array = Counter(result)
sorted(count_array.items())

common_c = count_array.most_common(100)
wc = WordCloud(
    font_path="/Library/Fonts/Songti.ttc",
    # 设置背景色
    background_color='white',
    # 允许最大词汇
    max_words=200,
    # 最大号字体
    max_font_size=100,
)
wc.generate_from_frequencies(dict(common_c))
plt.figure()
plt.imshow(wc)
plt.axis('off')
plt.show()
wc.to_file('wordcloud.jpg')

```

### 停用词 stop_words.txt

```
的
了
和
是
就
都
而
及
與
著
或
一個
沒有
我們
你們
妳們
他們
她們
是否

```

### 结果
![词云图](/img/posts/20171019-wordcloud.jpg)

### 踩过的坑

 - WordCloud中一定要设定字体，否则会出现一堆框框
