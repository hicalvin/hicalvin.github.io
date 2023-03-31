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



### Reference

- [Youtube: Advanced ChatGPT Guide - How to build your own Chat GPT Site](https://www.youtube.com/watch?v=bB7xkRsEq-g)
- [Jupyter module not found issue](https://jonathansoma.com/course/foundations-2021/jupyter-module-not-found/)