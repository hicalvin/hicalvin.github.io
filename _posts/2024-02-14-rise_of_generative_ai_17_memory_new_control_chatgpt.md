---
layout: post
title: 生成式AI的崛起17：初試 LangChain + RAG + Gemini
date: 2024-02-14 21:21:50 +0800
category: tech
---

> 今天是ChatGPT诞生第 **441** 天


今天是大年初五，迎财神咯！！ 

![chatgpt](https://images.unsplash.com/photo-1679403766680-9aa2b959417d?q=80&w=3570&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

*by [Andrew Neel](https://unsplash.com/@andrewtneel) in Unsplash*

今天，[OpenAI](https://openai.com/) 再次发布重要信息，ChatGPT 将对部分免费和 Pro 版本的用户开放[增强记忆（Memory）版本 ChatGPT](https://openai.com/blog/memory-and-new-controls-for-chatgpt)。 这对于 ChatGPT 的使用者来说又是一项重要的提升。

使用过 ChatGPT 或者其他 LLM 大模型的用户来说，一个非常头疼的问题就是对话的上下文过短，所以在进行一段长对话时，对话越往后，AI 的反馈越离谱，原因就是上下文的丢失，也就是 Memory 太短。OpenAI 针对这方面的提升，算是抓住了当前使用体验的一个痛点。 

![](https://images.openai.com/blob/d77c453f-fa97-4a74-9363-5fee31a478be/memory-and-new-controls-for-chatgpt.png?trim=0,0,0,0&width=3200)

那么 Memory 到底能怎么用？官网给了一些例子：

```
- You’ve explained that you prefer meeting notes to have headlines, bullets and action items summarized at the bottom. ChatGPT remembers this and recaps meetings this way.
- You’ve told ChatGPT you own a neighborhood coffee shop. When brainstorming messaging for a social post celebrating a new location, ChatGPT knows where to start. 
- You mention that you have a toddler and that she loves jellyfish. When you ask ChatGPT to help create her birthday card, it suggests a jellyfish wearing a party hat. 
- As a kindergarten teacher with 25 students, you prefer 50-minute lessons with follow-up activities. ChatGPT remembers this when helping you create lesson plans.
```

它可以记住你的一些文档格式偏好，所以当你让 ChatGPT 生成文档时就不需要每次都告诉它需要的格式时什么。 它也可以记住你的一些个人信息，从而让它的回答更加符合你的需要。 

如此种种，可以让你所使用的 ChatGPT 变得更加符合你的需要。

按照 OpenAI 所述，你可以在任何时候通过设置 (Settings > Personalization > Memory)来启用或者关闭这一功能。

针对团队或者企业用户，这个功能也许更加方便，可以让 ChatGPT 记住你的语气和表达方式，从而可以更加高效的生成有你风格的内容。 

```
- ChatGPT can remember your tone, voice, and format preferences, and automatically apply them to blog post drafts without needing repetition.
- When coding, you tell ChatGPT your programming language and frameworks. It can remember these preferences for subsequent tasks, streamlining the process.
- For monthly business reviews, you securely upload your data to ChatGPT and it creates your preferred charts with three takeaways each.
```

如此一来，每个人几乎都可以有一个或者几个数字分身，看来那些做数字分身的框架和应用又可以转行了... 

#ai/openai/chatgpt 