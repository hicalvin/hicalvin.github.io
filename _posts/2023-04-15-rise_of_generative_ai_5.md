---
layout: post
title:  "生成式AI的崛起04：LlamaIndex 和 LangChain 两把AI利刃"
date:   2023-04-15 22:33:50 +0800
category: tech
---

## LlamaIndex

LlamaIndex is a project that provides a central interface to connect your LLM's with external data like database and files(pdf, json, docx, epub etc). It also can access to some site like bilibili, reddit etc. There's a [Llama Hub](https://llamahub.ai/) to collect all the interfaces. 

LlamaIndex provides a simple pattern to connect your external data to OpenAI:

1. Build `document` by using `Reader`
2. Create `index` from `document`
3. Query with your questions by using `index.qeury`

Simple like that. More cases could be found in its [Ref](https://gpt-index.readthedocs.io/en/latest/index.html)

简单来说，LlamaIndex可以看成是一个将外部数据接入LLM的连接器。有了LlamaIndex，用户可以将存在于各种静态文本或者动态网站APP的数据接入LLM。 由于有了统一的使用模式，所以无论什么外部数据源，大家都可以将其导入成Document对象，然后通过Index来对数据提问。底层它接入了OpenAI的API，所以需要OpenAI API的token (不小心导入了一本神雕侠侣和一本笑傲江湖，终于成功的把免费的token用完了)。 

LlamaIndex 还为各种接口提供了[Hub](https://llamahub.ai/)，所以如果想要什么导入器，可以先去Hub上找找 

目前这个社区相当活跃，大家都在贡献各种数据源，甚至包括B站。 

## LangChain

The core idea of the library is that we can “chain” together different components to create more advanced use cases around LLMs. Chains may consist of multiple components from several modules:

- Prompt templates: Prompt templates are templates for different types of prompts. Like “chatbot” style templates, ELI5 question-answering, etc
- LLMs: Large language models like GPT-3, BLOOM, etc
- Agents: Agents use LLMs to decide what actions should be taken. Tools like web search or calculators can be used, and all are packaged into a logical loop of operations.
- Memory: Short-term memory, long-term memory.

这个是相对更加偏模型侧的项目，通过引入`Agents`, `Prompts`, `Chains` 等把`prompt`分解成更细的`prompt`和行为。和LlamaIndex一样，LangChain 也提供了一个 [Hub站点](https://blog.langchain.dev/langchainhub/)，供其他人去找优质的Prompt。 

> (AI)对每个人都将产生深远和系统性影响。我们的假设是每个人很快将有副驾驶员，不光是1个，可能是5个、6个。 有些副驾驶员足够强，变成正驾驶员，他自动可以去帮你做事。更长期，我们每个人都有一个驾驶员团队服务。未来的人类组织是真人，加上他的副驾驶员和真驾驶员一起协同。  -- 陆奇

### Key concepts

#### Chain of Thoughts

`Chain of Thoughts (CoT)` is a prompting technique used to encourage the model to generate a series of intermediate reasoning steps. A less formal way to induce this behavior is to include “Let’s think step-by-step” in the prompt.

> Here is a sample of CoT
> Here is a sample of how to use chain of thoughts to solve a problem:
> 
> I am hungry.
I need to eat something.
I could make a sandwich.
I need bread, meat, and cheese.
I have bread in the fridge.
I need to go to the store for meat and cheese.
I will go to the store after I finish this work.

#### Action Plan Generation

`Action Plan Generation` is a prompting technique that uses a language model to generate actions to take. The results of these actions can then be fed back into the language model to generate a subsequent action.

行动计划生成是指创建一个实现特定目标的行动计划的过程。它涉及识别需要采取的步骤、所需资源和完成的时间表。

#### ReAct

`ReAct` is a prompting technique that combines Chain-of-Thought prompting with action plan generation. This induces the to model to think about what action to take, then take it.

### Reference

- [LLAMA-Index vs LangChain](https://alphasec.io/query-your-own-documents-with-llamaindex-and-langchain/)
- [Langchain Introduction](https://www.pinecone.io/learn/langchain-intro/)
- [Huggingface - AI Community](https://huggingface.co/)
- [Getting Started with LangChain](https://towardsdatascience.com/getting-started-with-langchain-a-beginners-guide-to-building-llm-powered-applications-95fc8898732c)