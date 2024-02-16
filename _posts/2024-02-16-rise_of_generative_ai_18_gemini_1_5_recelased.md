---
layout: post
title: 生成式AI的崛起18：快马加鞭，Gemini 1.5 Pro 来了
date: 2024-02-16 19:04:50 +0800
category: tech
---

> 今天是ChatGPT诞生第 **443** 天

年前预想到今年的 AI 战场会硝烟四起，但是没想到会卷成这样。 谷歌刚刚2月6日宣布 Gemini 全面接替 Bard，发布 Gemini 1.0， 没想到10天不到的时间就发布了 Gemini 1.5 Pro。

2月15日，Google 和 Deepmind 的两位 CEO 一起宣布了 [**Our next-generation model: Gemini 1.5**](https://blog.google/technology/ai/google-gemini-next-generation-model-february-2024/)。

Gemini 1.5 是基于一个全新的 Mixture-of-Experts 架构，这一架构可以有效的提升计算量，根据[相关论文](https://arxiv.org/abs/1701.06538)的介绍， 将 MoE 应用到大语言模型和机器翻译任务上，可以提升1000倍以上的计算效率。基于这一点，新一代的 Gemini 1.5 可以从容的用于视觉化的计算场景。 之前的 Gemini 1.0 Pro 允许的输入 token 数量为32k，而新的 Gemini 1.5 的 token 限制达到了 1M。 这个 token 量，约等于1个小时的视频，11小时的音频， 3万行的代码，70万字的文本。

在实验中，谷歌工程师还成功的测试了一千万 token 下的表现。

巨量的 token 代表着超长文本的理解能力，从而为大模型的功能提供最基础也最重要的基础数据。在视频中，谷歌工程师将当年阿波罗11号登月的402页长的文本喂给 Gemini 1.5 Pro，然后通过 一幅话了一只脚往下踩的简笔画提问，结果 1.5 Pro 成功的回答了阿姆斯特朗的名言 “这是我个人的一小步，却是人类迈出的一大步”。

1.5 Pro 可以针对不同的包括视频在内的模型，开展高度复杂的理解和推理任务。它在一本44分钟的默片视频中，准确的分析各种情节点和时间，甚至推理出电影中非常容易遗漏的微小细节。

它还能对十万行代码提供有效的帮助、修改以及解释。

超长上下文学习，节省了以前通过大量微调获得的能力。在这点上，和前几天 OpenAI 增强 Memory 的做法如出一辙。

而在 API 方面，谷歌也发布了新的模型 `models/gemini-pro-vision`。这是针对图片发布的 API 模型，输入 token 限制为12k

如果想知道具体有哪些 model，可以调用 `genai.list_models()` 来获得。以下是两个最重要的模型：

```
---
model name: models/gemini-1.0-pro
model display_name: Gemini 1.0 Pro
model input token limit: 30720
model version: 001
description: The best model for scaling across a wide range of tasks
---
model name: models/gemini-pro-vision
model display_name: Gemini 1.0 Pro Vision
model input token limit: 12288
model version: 001
description: The best image understanding model to handle a broad range of applications
---
```

#ai/openai/chatgpt
