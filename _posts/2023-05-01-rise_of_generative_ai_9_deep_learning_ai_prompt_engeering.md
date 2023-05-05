---
layout: post
title:  "生成式AI的崛起09：吴恩达老师的Prompt Engineering课开始了"
date:   2023-05-01 20:50:50 +0800
category: tech
---

![Andrew's courses](/assets/doc_img/2023-05-01-rise_of_generative_ai_9_chatgpt_prompt.jpg)

吴恩达又发干货了。

他的Deeplearning.ai 和OpenAI合作一起制作了一套 "ChatGPT Prompt Engineering" 课程，邀请了OpenAI的工程师 Isa Fulford 和他一起来讲这部分内容，而后者也是github上 openai-cookbook 和 chatgpt-retrieval-plugin 两个代码库的重要成员， 在Twitter上拥有1w多的追随者。

## 介绍

大语言模型，也就是LLM(Large Language Models) 又分为两种类型，一种叫 Base LLM，另外一种叫 Instruction Tuned LLM. 

Base LLM 是基于预训练的数据给出下个词的提示。如：

> ME: Once upon a time, there was a unicorn (很久很久以前，曾经有一直独角兽...)

那么基于Base LLM，对于上述的提示词也许会接上：

> Base LLM: that lived in a magical forest with all her unicorn friends. (...和他的其他独角兽朋友生活在一片有魔法的森林里。)

但是如果你问以下的问题：

> ME: What is the capital of France?  (法国首都是哪里？)

Base LLM的回复会是如下结果：

> Base LLM: What is France's largest city?  (哪里是法国最大的城市？)
> What is France's population?              (法国的人口是多少？)
> What is the currency of France?           (法国的货币是什么？)

原因可能因为它的训练预料都来自网上，而网上很可能是把关于法国相关的问题作为列表放在一起形成了上下文。 

在这种场景下， Instruction Tuned LLM 就会给出更好地答案，也是让整个LLM往前发展的重要技术环节，因为它会很好的调优并且去遵循指令。 

所以如果是上面同样一个问题：

> ME: What is the capital of France?  (法国首都是哪里？)

它给出的答案就会是：

> Instruction Tuned LLM: The capital of France is Paris. 

所以在我们使用ChatGPT的过程中，我们更多的是会用到 Instruction Tuned LLM的部分，而吴老师也是着重说这方面内容。 

## 指南

ChatGPT就像一个无所不知的智者，与它交流，必须要明确，不能模棱两可。 比如说如果你想知道阿兰.图灵，你不能只是简单问 "请告诉我关于图灵的事"， 而最好是明确你到底想知道的是他的学术成就，还是个人生活，甚至有可能是他的历史作用。

所以如果要和ChatGPT聊天，一定要 **清晰、具体**。 

> 注意： 清晰并不等于短。有时候需要比较长的提示词才能描述清楚你的要求。 


### 技巧1： 使用定界符，如 "```", "~~~", "---", "< > "

~~~jupyter
text = f"""
You should express what you want a model to do by \
providing instructions that are as clear and \
specific as you can possibly make them. \
This will guide the model towards the desired output, \
and reduce the chances of receiving irrelevant \
or incorrect responses. Don't confuse writing a \
clear prompt with writing a short prompt. \
In many cases, longer prompts provide more clarity \
and context for the model, which can lead to \
more detailed and relevant outputs.
"""
Summarize the text delimited by triple backticks \
into a single sentence.
```{text}```

~~~

### 技巧2: 要求使用结构化的输出，比如 JSON， HTML

~~~jupyter
prompt = f"""
Generate a list of three made-up book titles along \
with their authors and genres.
Provide them in JSON format with the following keys:
book_id, title, author, genre.
"""
response = get_completion(prompt)
print(response)
~~~

### 技巧3: 询问模型确保条件是否满足

~~~jupyter
text_1 = f"""
Making a cup of tea is easy! First, you need to get some \ 
water boiling. While that's happening, \ 
grab a cup and put a tea bag in it. Once the water is \ 
hot enough, just pour it over the tea bag. \ 
Let it sit for a bit so the tea can steep. After a \ 
few minutes, take out the tea bag. If you \ 
like, you can add some sugar or milk to taste. \ 
And that's it! You've got yourself a delicious \ 
cup of tea to enjoy.
"""
prompt = f"""
You will be provided with text delimited by triple quotes. 
If it contains a sequence of instructions, \ 
re-write those instructions in the following format:

Step 1 - ...
Step 2 - …
…
Step N - …

If the text does not contain a sequence of instructions, \ 
then simply write \"No steps provided.\"

\"\"\"{text_1}\"\"\"
"""
response = get_completion(prompt)
print("Completion for Text 1:")
print(response)
~~~ 

### 技巧4: 给出示例问答

~~~jupyter

prompt = f"""
Your task is to answer in a consistent style.

<child>: Teach me about patience.

<grandparent>: The river that carves the deepest \ 
valley flows from a modest spring; the \ 
grandest symphony originates from a single note; \ 
the most intricate tapestry begins with a solitary thread.

<child>: Teach me about resilience.
"""
response = get_completion(prompt)
print(response)

~~~

## 基于第一个原则之上，第二个原则，就是给予ChatGPT足够的时间 :) 

### 技巧1: 指导ChatGPT需要完成任务的每一步，并指定输出结构，从而可以更好找到想要的内容

~~~jupyter
prompt_2 = f"""
Your task is to perform the following actions: 
1 - Summarize the following text delimited by 
  <> with 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the 
  following keys: french_summary, num_names.

Use the following format:
Text: <text to summarize>
Summary: <summary>
Translation: <summary translation>
Names: <list of names in Italian summary>
Output JSON: <json with summary and num_names>

Text: <{text}>
"""
response = get_completion(prompt_2)
print("\nCompletion for prompt 2:")
print(response)
~~~

### 技巧2: 建议ChatGPT在得出结论之前，先给出自己的办法

~~~jupyter
prompt = f"""
Your task is to determine if the student's solution \
is correct or not.
To solve the problem do the following:
- First, work out your own solution to the problem. 
- Then compare your solution to the student's solution \ 
and evaluate if the student's solution is correct or not. 
Don't decide if the student's solution is correct until 
you have done the problem yourself.

Use the following format:
Question:
```
question here
```
Student's solution:
```
student's solution here
```
Actual solution:
```
steps to work out the solution and your solution here
```
Is the student's solution the same as actual solution \
just calculated:
```
yes or no
```
Student grade:
```
correct or incorrect
```

Question:
```
I'm building a solar power installation and I need help \
working out the financials. 
- Land costs $100 / square foot
- I can buy solar panels for $250 / square foot
- I negotiated a contract for maintenance that will cost \
me a flat $100k per year, and an additional $10 / square \
foot
What is the total cost for the first year of operations \
as a function of the number of square feet.
``` 
Student's solution:
```
Let x be the size of the installation in square feet.
Costs:
1. Land cost: 100x
2. Solar panel cost: 250x
3. Maintenance cost: 100,000 + 100x
Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
```
Actual solution:
"""
response = get_completion(prompt)
print(response)
~~~

### 模型缺陷：幻觉

这点在试过ChatGPT的人当中都心知肚明，就是它会一本正经的胡说八道。据说这是作为一个聊天机器人所能容忍的缺陷，因为它最怕的不是错误，而是怕把天聊死...

> Hallucination - Makes statements that sound plausible but are not true

那么如何避免呢？其中一个办法就是要求模型先找到相关的信息，然后基于相关信息再来回答问题。

## 迭代 (Iterative)

针对Prompt Engineering，也要采用想其他机器学习开发一样的迭代模式：

Idea -> Implementation -> Experimental result & Error Analysis

所以针对Prompt的优化流程就是 

- Be clear and specific
- Analyze why result does not give desired output
- Refine the idea and the prompt
- Repeat

针对返回的结果，会出现不同的情况。

### 情况1: 结果太长

这时候可以用字数、句数或者词数来限定返回的内容长度。 

> e.g. Use at most 50 words. 

### 情况2: 模型聚焦在错误的细节上

这时候可以提示ChatGPT这个任务是给谁服务的。 

> The description is intended for furniture retailers, 
so should be technical in nature and focus on the 
materials the product is constructed from.

### 情况3: 描述需要有个表格展示

可以提示ChatGPT用表格的形式列出产品的某些维度

> After the description, include a table that gives the 
product's dimensions. The table should have two columns.
In the first column include the name of the dimension. 
In the second column include the measurements in inches only.
> 
> Give the table the title 'Product Dimensions'.

## 总结内容 (Summarizing)

可以给出限定要求，让ChatGPT按指定要求进行总结。

### 技巧1: 给出词数、字数、句数

~~~jupyter
prompt = f"""
Your task is to generate a short summary of a product \
review from an ecommerce site. 

Summarize the review below, delimited by triple 
backticks, in at most 30 words. 

Review: ```{prod_review}```
"""

response = get_completion(prompt)
print(response)

~~~

### 技巧2: 按给出的关注点总结，例如物流

~~~jupyter
prompt = f"""
Your task is to generate a short summary of a product \
review from an ecommerce site to give feedback to the \
Shipping deparmtment. 

Summarize the review below, delimited by triple 
backticks, in at most 30 words, and focusing on any aspects \
that mention shipping and delivery of the product. 

Review: ```{prod_review}```
"""

response = get_completion(prompt)
print(response)

~~~

### 技巧3: 尽量用 `extract`， 而不是 `summarize`

### 技巧4: 可以用循环一次性生成多个summary

~~~jupyterpython
for i in range(len(reviews)):
    prompt = f"""
    Your task is to generate a short summary of a product \ 
    review from an ecommerce site. 

    Summarize the review below, delimited by triple \
    backticks in at most 20 words. 

    Review: ```{reviews[i]}```
    """

    response = get_completion(prompt)
    print(i, response, "\n")

~~~

## 推断 (Inferring)

作为语言模型的一种， ChatGPT最擅长的当然是自然语言处理。我们可以用它来判断一段评论的情绪倾向，也包括从一段话中提取信息。 

~~~jupyter
lamp_review = """
Needed a nice lamp for my bedroom, and this one had \
additional storage and not too high of a price point. \
Got it fast.  The string to our lamp broke during the \
transit and the company happily sent over a new one. \
Came within a few days as well. It was easy to put \
together.  I had a missing part, so I contacted their \
support and they very quickly got me the missing piece! \
Lumina seems to me to be a great company that cares \
about their customers and products!!
"""

prompt = f"""
What is the sentiment of the following product review, 
which is delimited with triple backticks?

Review text: '''{lamp_review}'''
"""
response = get_completion(prompt)
print(response)

prompt = f"""
Identify the following items from the review text: 
- Item purchased by reviewer
- Company that made the item

The review is delimited with triple backticks. \
Format your response as a JSON object with \
"Item" and "Brand" as the keys. 
If the information isn't present, use "unknown" \
as the value.
Make your response as short as possible.
  
Review text: '''{lamp_review}'''
"""
response = get_completion(prompt)
print(response)
~~~

## 转换 (Transforming)

转换包括不同语言之间的翻译，语言的识别等等，包括正式或非正式场合的语气。

~~~jupyter
prompt = f"""
Translate the following English text to Spanish: \ 
```Hi, I would like to order a blender```
"""
response = get_completion(prompt)
print(response)
~~~

~~~jupyter
prompt = f"""
Translate the following from slang to a business letter: 
'Dude, This is Joe, check out this spec on this standing lamp.'
"""
response = get_completion(prompt)
print(response)
~~~

~~~jupyter
text = [ 
  "The girl with the black and white puppies have a ball.",  # The girl has a ball.
  "Yolanda has her notebook.", # ok
  "Its going to be a long day. Does the car need it’s oil changed?",  # Homonyms
  "Their goes my freedom. There going to bring they’re suitcases.",  # Homonyms
  "Your going to need you’re notebook.",  # Homonyms
  "That medicine effects my ability to sleep. Have you heard of the butterfly affect?", # Homonyms
  "This phrase is to cherck chatGPT for speling abilitty"  # spelling
]
for t in text:
    prompt = f"""Proofread and correct the following text
    and rewrite the corrected version. If you don't find
    and errors, just say "No errors found". Don't use 
    any punctuation around the text:
    ```{t}```"""
    response = get_completion(prompt)
    print(response)
~~~

## 扩充 (Expanding)

这部分的应用场景，是针对客户的抱怨写一封客服的回信。 这里提到了关于`Temperature`的设定。 `Temperature` 这个参数控制结果的随机性，取值范围是 0-1。 如果`Temperatur=0`, 则返回训练数据中概率最高的值，而如果取一个比较大的值，那么很有可能会选择更加有创意的，平时出现可能性较低的值。


本课程最后演示了如何制作一个聊天机器人，通过使用Python的Panel库生成了一个交互式的界面。课程总时长为1.5小时，虽然时长较短，但几乎涵盖了与ChatGPT交互的全部内容。此外，整个课程都是通过Jupyter Notebook演示，使用OpenAI的API进行调用。通过学习这门课程，您可以基本掌握如何使用API与OpenAI进行交互的方法。总之，这门课程是非常值得推荐的。

