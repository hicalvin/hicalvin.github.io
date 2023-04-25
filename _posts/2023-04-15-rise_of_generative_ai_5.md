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

## LangChain

The core idea of the library is that we can “chain” together different components to create more advanced use cases around LLMs. Chains may consist of multiple components from several modules:

- Prompt templates: Prompt templates are templates for different types of prompts. Like “chatbot” style templates, ELI5 question-answering, etc
- LLMs: Large language models like GPT-3, BLOOM, etc
- Agents: Agents use LLMs to decide what actions should be taken. Tools like web search or calculators can be used, and all are packaged into a logical loop of operations.
- Memory: Short-term memory, long-term memory.

> (AI)对每个人都将产生深远和系统性影响。我们的假设是每个人很快将有副驾驶员，不光是1个，可能是5个、6个。 有些副驾驶员足够强，变成正驾驶员，他自动可以去帮你做事。更长期，我们每个人都有一个驾驶员团队服务。未来的人类组织是真人，加上他的副驾驶员和真驾驶员一起协同。  -- 陆奇

### Reference

- [LLAMA-Index vs LangChain](https://alphasec.io/query-your-own-documents-with-llamaindex-and-langchain/)
- [Langchain Introduction](https://www.pinecone.io/learn/langchain-intro/)
- [Huggingface - AI Community](https://huggingface.co/)