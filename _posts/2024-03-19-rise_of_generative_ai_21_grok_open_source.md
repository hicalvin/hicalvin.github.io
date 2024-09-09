---
layout: post
title: "生成式AI的崛起21: 马斯克的豪气 - Grok 成为开源大模型 No.1"
date: 2024-03-19 20:59:50 +0800
category: tech
---

> 今天是ChatGPT诞生第 **475** 天

![](https://x.ai/_next/static/media/grok-os-teaser.b49bf551.png)

进入2024年以后，“生成式 AI 的崛起” 这个主题感觉就是被追着写的节奏，AI领域大事件简直是此起彼伏，从不消停。 这不，3月17日，马斯克将他的 Grok 开源了！！

> March 17, 2024

> Open Release of Grok-1

> We are releasing the weights and architecture of our 314 billion parameter Mixture-of-Experts model, Grok-1.


传说中，Grok的开源之旅是由网友对马斯克的一番挑衅引发的。马斯克此前不断批评OpenAI背离了其创立的初衷，甚至戏称其应更名为CloseAI。这激起了网友的反击，他们调侃马斯克：“你的Grok又在哪里开源了？”出乎意料的是，马斯克接下了这个挑战，在x.com上宣布将在一周内开源Grok。就这样，Grok如期在Github上亮相，仅仅两天时间，就已经吸引了超过3万颗星和5千多次fork，这份大气令人敬佩不已。

Grok的开源为本地部署的大模型提供了一个更强大的选项。让我们看看一些关键数据点来理解其重要性。

首先，Grok是目前最大的开源大语言模型，拥有3140亿参数，是首个突破千亿参数量的开源模型。大量的参数意味着更为强大的语言处理能力。

其次，这个模型完全由x.ai独立训练，使用的数据截至2023年10月。作为一个基础预训练模型，它未针对任何特定应用进行微调。因此，想要使用它的开发者需要从GitHub下载权重并进行必要的微调。

最重要的是，Grok 是用 Apache2.0的许可证下开源的。在Apache2.0许可证的宽松条款下，Grok的权重和架构得以自由地被使用、修改和再发布，无论是个人项目还是商业应用，这无疑为开发者社区带来了前所未有的灵活性。

Grok专注于文本处理，采用了单模态训练方法，而非融合多种数据类型的多模态途径。

在一系列标准化测试中（包括MMLU, GSM8k, Math, HumanEval），Grok的表现超越了其他开源竞争者，如Meta的LLaMa、谷歌的Gemma以及Mistral的8x7B模型，甚至在某些方面超过了GPT3.5。尽管它在性能上仍然落后于Claude2和GPT4，但在开源界，Grok无疑占据了领先地位。

然而，模型之大，也意味着需要更多的资源来运行它，但对于企业而言，有这么强大的模型支持，在硬件上投入应该是值得的。

#ai/xai/grok