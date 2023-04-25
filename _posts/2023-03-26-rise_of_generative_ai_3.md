---
layout: post
title:  "生成式AI的崛起03：ChatGPT API 入门指南：技巧与窍门"
date:   2023-03-26 00:52:50 +0800
category: tech
---

## Step 1 - Get the OPENAI API Token

To use OpenAI API, the first step is to create API Key. 

- Visit [API Key](https://platform.openai.com/account/api-keys) to *Generate new secret key* if you don't have yet, and then copy right after generation since you don't have second chance to get that unless you generate another one.

> With that, if you want to run Python script in your local terminal, you can use `os` library to set environment variable.

~~~python
  import os
  os.environ["OPENAI_API_KEY"] = "sk-xxxx"
~~~
    - :bulb: If met with `module not found` issue, please check out below reference. highly suspicious that it's caused by multiple version of Python installed. 

## Step 2 - Use API Key to call OpenAI API

~~~python
import openai
openai.api_key = "sk-xxxx" # replace with your API key

# Example usage: generate text with GPT-3
prompt = "Once upon a time"
model = "text-davinci-002"
response = openai.Completion.create(engine=model, prompt=prompt, max_tokens=50)
generated_text = response.choices[0].text
print(generated_text)

// This code block shows how to use the OpenAI API to generate text using the GPT-3 model. First, you need to set your API key using `openai.api_key`. Then, you can call `openai.Completion.create` to generate text with the specified model and prompt. The generated text is returned in the `response` object, and can be accessed using `response.choices[0].text`.
~~~

Some tips when using the ChatGPT API:
- Experiment with different prompts to get the desired output.
- Choose the appropriate model for your use case. The `text-davinci-002` model is the most powerful, but also the most expensive.
- Use the `max_tokens` parameter to control the length of the generated text.
- Be mindful of the API usage limits to avoid unexpected charges.

在使用OpenAI API的时候，需要传的参数里面有两个关键参数：`model`, `messages`. 

`model`比较简单，是可以指定你想要实用的LLM模型的类型，比如`gpt-3.5-turbo`, `gpt-4`, `gpt-4-0314`等。 注意使用不同的`model`，价格是不一样的。 

另外一个参数是`messages`，是一对`message`对象的列表，而每个对象又有两个必须的属性：
- `role`： 是指这条消息的角色，包含`system`， `user`和`assistant`  
- `content`： 消息的内容。 

关于`role`， 区分`system`和`assistant`还稍微花点时间。根据OpenAI的官方文档， `system`像是一个定位整个对话的引导员，通常会是高速chatgpt它的角色是什么，比如：

`{'role': 'system', 'content': 'You are an assistant that speaks like Shakespeare. ''`

而 `assistant`就可以看成是chatgpt这个人化的角色。 

详细解释和例子可以在[ChatGPT API Transition Guide](https://help.openai.com/en/articles/7042661-chatgpt-api-transition-guide) 找到。 


### Reference

- [Youtube: Advanced ChatGPT Guide - How to build your own Chat GPT Site](https://www.youtube.com/watch?v=bB7xkRsEq-g)
- [Jupyter module not found issue](https://jonathansoma.com/course/foundations-2021/jupyter-module-not-found/)