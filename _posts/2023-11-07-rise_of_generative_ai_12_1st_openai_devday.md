---
layout: post
title:  "生成式AI的崛起12：OpenAI第一届开发者日"
date:   2023-11-07 21:56:50 +0800
category: tech
---

## 中文

今天（11月7日），首届OpenAI DevDay在旧金山盛大开幕，这一活动标志着人工智能领域达到了一个重要的里程碑。这场由山姆.奥特曼主持的活动，除了简单回顾OpenAI在过去一年中所取得的成就之外，更重要的是发布OpenAI在AI开发领域的领先进展。

首先，他回顾了2022年11月30日OpenAI宣布ChatGPT到来的那一天。这个事件标志着AI开发的一次重大飞跃，引入了一个能够进行微妙且具有情境意识的对话的对话模型。自那时以来，ChatGPT开始不断进化，每次迭代都变得更聪明、更细腻，为用户提供了一个不仅能提供信息，而且能从交互中学习的交互工具。

下一个值得注意的里程碑是2023年3月GPT-4的发布。作为GPT-3的强大继任者，它带来了更为卓越的能力，进一步模糊了人机交互的界限。GPT-4扩大了语言模型的覆盖范围和潜力，整合了更为复杂的理解和回应机制。

延续这一进步的轨迹，OpenAI为ChatGPT引入了声音和视频功能。这种更新使AI能够听、说和看，将用户交互提升到了一个全新的层次。这不再只是键入问题和接收基于文本的回应，为对话体验增加了全新的层次。

在这些技术进步之后，OpenAI推出了ChatGPT的企业版。这个强大的工具为企业提供了一个更加强大、定制的解决方案。借助此工具，OpenAI成功吸引了大量的客户，从初创公司到跨国公司。

开幕致辞中分享的令人印象深刻的统计数据是OpenAI拥有的庞大用户基础。
- 拥有超过两百万的开发者
- 92%的财富500强公司积极使用他们的技术
- 每周有超过一亿的活跃用户

在一系列的成就之后，与会者们观看了一个2.5分钟的视频，回顾了各种ChatGPT用户的故事。其中一个特别让人印象深刻的故事是一个百岁老人在他的百岁生日那天发现了这个工具，这展示了这个AI工具的广泛吸引力。

在过去一年的成就被详细介绍之后，山姆转向了令人兴奋的新进展。

第一个重大的公告是**新模型GPT-4 Turbo**的引入。这个最新的迭代版本充满了增强功能：

- 它支持长达128k token的长文本，相当于一本300页的书，允许进行更深入的交互。
- GPT-4 Turbo为用户提供了更多的控制。这包括为结构化的输入和输出提供的JSON模式，支持一次请求多个功能调用，以及可复制的输出，确保在使用相同参数时得到一致的结果。
- 该模型具有更新的知识，从2021年11月到2023年4月的数据得到了改进。
- GPT-4 Turbo整合了几个功能 - DallE3、GPT4、和TTS，成为一个单一、强大的模型。
- 这个新模型的一个关键特性是能够构建自定义模型，给开发者自由定制AI的能力。
- 最后，GPT-4 Turbo提供了更高的速率限制，使得每分钟的token数量翻倍。

可以说，最让人兴奋的公告是GPT-4 Turbo的价格下降，使其更加可接近。新的定价模型为**每1000个输入token收费1分，每1000个输出token收费3分**，远比其前身GPT-4更经济。

在这些显著的发展的介绍之后，山姆欢迎了一个特别嘉宾，Microsoft的CEO - 萨蒂亚.纳德拉。他上台讨论了OpenAI和Microsoft之间的合作关系，强调了他们共同推进AI技术的努力。

然后OpenAI揭示了**GPTs**，开放给全球开发者构建和定制他们的ChatGPT模型。为了展示这些进步的实际应用，来自OpenAI的工程师展示了如何使用[Zapier](https://zapier.com/)的GPT模型连接她的个人日历和聊天工具,现场展示使用自然语言让不同的工具交互是多么的简单。

既然可以构建自己的GPT，那么OpenAI把GPT的构建再往前推进了一步，只用自然语言，就可以构建一个自己的GPT。山姆亲自演示了这个功能，使用自然语言，利用他在YC做投资时的经验文档，通过与GPT Builder对话。GPT Builder 就开始从命名GPT模型，选择应用图标，到建立GPT的过程页面全过程，完全由自然语言输入驱动。在几分钟内，一个叫'Startup Mentor'的新GPT模型诞生了。

在GPT Builder的成功演示之后，山姆宣布了**GPT Store**上线。这个平台的功能类似于Apple的App Store，允许每个GPT模型都公开使用。它也有像App Store一样的排名系统，为用户提供了最受欢迎和最有效的GPT模型的排行。

当活动接近尾声时，OpenAI又展示了Assistants API的Beta版本。这基本上是[Langchain](https://hicalvin.github.io/tech/2023/04/rise_of_generative_ai_5)的'官方'版本，通过API连接不同的动作(Action)和代理(Agent)。OpenAI的工程师通过创建一个旅行计划App展示了Assistants API的丰富功能，包括展示语音版本的GPT的后台任务链。 

最后环节的一个巨大彩蛋，是OpenAI通过Assistants API的功能给DevDay的每个参会者的OpenAI账户上增加了500美元的积分。这个惊喜不仅使参会者感到欢喜，也作为新的Assistants API能力的强大演示。

总的来说，首届OpenAI DevDay是一次盛大的成功。这是对OpenAI在过去一年中取得的重大进步的庆祝，也是对AI未来的预览。当我们反思这个活动时，很明显，OpenAI不仅在引领AI革命，还在培育一个致力于推动AI可能性边界的创新者和开发者的社区。


## English

On November 7th, the curtains were raised on the inaugural OpenAI DevDay in San Francisco, marking a significant milestone in the realm of artificial intelligence. The event, hosted by Sam Altman, served as a platform to review the progress OpenAI has made over the past year, further solidifying its status as a leading force in AI development.

The opening address by Sam took the attendees on a trip down memory lane, highlighting some landmark achievements that OpenAI has accomplished.

Firstly, he recalled the announcement on November 30th, 2022, when OpenAI heralded the arrival of ChatGPT. This event marked a significant leap in AI development, introducing a conversational model that could engage in nuanced and contextually aware conversations. ChatGPT has since evolved, growing smarter and more nuanced with each iteration, offering users an interactive tool that not only provides information but also learns from interactions.

The next notable milestone was the launch of GPT-4 in March 2023. As a powerful successor to GPT-3, it brought forth even more impressive capabilities, further blurring the line between human and machine interactions. GPT-4 expanded the reach and potential of language models, incorporating more sophisticated comprehension and response mechanisms.

Continuing on this trajectory of progress, OpenAI introduced voice and video functionality to ChatGPT. This transformative update enabled the AI to interpret and respond to vocal cues and video inputs, taking user interactions to a completely new level. It was no longer just about typing questions and receiving text-based responses; ChatGPT could now see and hear, adding a whole new layer to the conversational experience.

Following these technological advances, OpenAI launched an Enterprise version of ChatGPT. This powerful tool offered businesses a more robust, tailored solution for their unique needs. With this, OpenAI managed to attract a vast array of clientele, from startups to multinational corporations.

The most impressive statistic shared during the opening address was the massive user base that OpenAI boasts. With over two million developers and 92% of Fortune 500 companies actively using their technology, OpenAI's reach is truly global. Adding to this, they have over 100 million weekly active users, a testament to the practicality and usability of their AI solutions.

Following the series of achievements, attendees were shown a 2.5-minute video recounting the stories of various ChatGPT users. One particular account that stood out was of a centenarian who discovered the tool on his 100th birthday, illustrating the wide-ranging appeal of this AI tool.

With the past year's achievements laid out, Sam then shifted the focus to the exciting new developments. 

The first major announcement was the introduction of the new model, **GPT-4 Turbo**. This latest iteration is packed with enhancements:

1. It supports long contexts of up to 128k tokens, equivalent to a 300-page book, allowing for more extended, in-depth interactions.
2. GPT-4 Turbo offers more control to users. This includes a JSON mode for structured inputs and outputs, support for one request for multiple function calls, and reproducible output, ensuring consistent results when using the same parameters.
3. The model features updated knowledge, drawing from data improved from November 2021 to April 2023.
4. GPT-4 Turbo amalgamates several functionalities - DallE3, GPT4, and TTS, into a single, powerful model.
5. A key feature of this new model is the ability to build custom models, giving developers the freedom to tailor the AI to their specific needs.
6. Lastly, GPT-4 Turbo provides a higher rate limit, doubling the tokens per minute from the previous version.

Arguably, the most exciting announcement was the reduced pricing for GPT-4 Turbo, making it even more accessible. The new pricing model charges **1 cent for 1000 input tokens and 3 cents for 1000** output tokens, making it more economical than its predecessor, GPT-4. 

After the introduction of these remarkable developments, Sam welcomed a special guest, Satya Nadella, the CEO of Microsoft. He took the stage to discuss the partnership between OpenAI and Microsoft, highlighting their combined efforts to advance AI technology. 

Then OpenAI unveiled GPTs, any customized GPT with different business contexts. This platform allows developers to build and customize their ChatGPT models. To showcase the practical application of these advancements, an engineer from OpenAI, demonstrated how to use Zapier's GPT model to connect her personal calendar and chat tool. This live demo showed how easy it is to interact with different tools using natural language, thanks to the advancements in AI technology. 

Following the insightful discussion with the CEO of Microsoft, Sam took center stage to present a live demonstration of building a GPT model using natural language. The focus of this demonstration was to construct a GPT model based on Sam's experience as a YC venture investor, designed to answer queries from startup founders. 

The magic began when Sam started conversing with the **GPT Builder**. Starting with the naming of the GPT model and selecting a profile avatar, the process of building the GPT was entirely driven by natural language input. The next step involved uploading a transcript of Sam's investor experiences to provide the GPT model with the necessary knowledge base. Upon moving to the 'Configure' tab and uploading the file, a new GPT model named 'Startup Mentor' was created in no time.

With the successful demonstration of the GPT Builder, Sam announced the availability of the **GPT Store**. This platform functions similarly to Apple's App Store, allowing every GPT model to be publicly accessible. It also features a ranking system, providing users an insight into the most popular and effective GPT models.

As the event neared its conclusion, Sam unveiled the Beta version of the **Assistants API**. This system is essentially an 'official' version of Langchain, connecting different actions and agents through API. To demonstrate its capabilities, a live demo was conducted that involved trip planning and voice commands. 

In an exciting turn of events, the engineer used a voice command to award each DevDay attendee a credit of 500 dollars in the OpenAI account. This surprise not only delighted the attendees but also served as a powerful demonstration of the capabilities of the new Assistants API.

In summary, the first OpenAI DevDay was a grand success. It was a celebration of the significant strides OpenAI has made in the past year, and a revealing peek into the future of AI. As we reflect on this event, it's clear that OpenAI is not just leading the AI revolution but also fostering a community of innovators and developers committed to pushing the boundaries of what's possible with AI.

## 参考

- [OpenAI开发者日中英文完整版](https://youtu.be/lydmOkYSLyE?si=7EXUWdalZKb7XMAJ)
- [OpenAI开发者日带来了什么](https://youtu.be/4-SSjvWx1B8?si=hnAitRZct5IMtpOJ)


#ai/openai #ai/openai/chatgpt 