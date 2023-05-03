---
layout: post
title:  "生成式AI的崛起07：用GPT-4完成整本小说"
date:   2023-04-28 10:42:50 +0800
category: tech
---

![GPT4](/assets/doc_img/2023-04-29-gpt4.jpg)

## Echoes of Atlantis -- by GPT-4

居然已经有人用GPT-4完成整本小说的创作。

用过ChatGPT的人应该感觉到，让ChatGPT一直围绕固定的主题输出长篇的内容，其实并不容易，因为它总是会不受控的发散。如果要限制它一直按照一个主题输出，还是需要挺多技巧的。 这也就是Prompt Engineering的意义所在。

创作者叫Chiara，小说题目叫"Echoes of Atlantis"，我觉得作为第二语言的学习，这个故事还算是不错的阅读材料，不过比起专业小说家写的小说，内容的惊喜程度还是差了点。

但这本小说可以说是百分之百纯AI作品，无论是故事的提纲、类型，还是体裁、细节，都是AI自己决定的，Chiara做的是如何一步步的引导整个步骤，从提出类型要求，到一步步生成故事大纲、然后到一幕幕的具体场景等等，最终经历10天时间，完成了12个章节，115页的幻想冒险类小说。 

这个过程是一个很好的Prompt Engineering的示例。按照作者分享的整个过程，针对提示语的使用大概可以分为4个层次：

### Level 1: Top-level outline

> Me: Please write a high-level outline for a book. Include a list of characters and a short description of each character. Include a list of chapters and a short summary of what happens in each chapter. You can pick any title and genre you want.

### Level 1: Updating outline after each chapter

> Me: Please edit and update the high-level outline for the book below, taking into account what has already happened in Chapter 1.

### Level 2: Scenes (bounding)

> Me: Please write a detailed outline describing the first scene of each chapter. It should describe what happens in that opening scene and set up the story for the rest of the chapter. Do not summarize the entire chapter, only the first scene.

### Level 2: Scenes

> Me: Given the following book outline, and the following opening and final scenes for Chapter 1, write a detailed chapter outline giving all the scenes in the chapter and a short description of each. Begin the outline with the Opening Scene below, and finish the outline with the Final Scene below.

### Level 3: Rough draft

> Me: Given the following book outline, and following detailed chapter outline for Chapter 1, write a first draft of Chapter 1. Label each of the scenes. Stop when you reach the end of Chapter 1. It should set up the story for Chapter 2, which will come immediately afterwards. It should be written in a narrative style and should be long, detailed, and engaging.

### Level 4: Paragraphs (bounding)

> Me: Given the following book outline, and the following draft of Chapter 1, imagine that you have expanded this draft into a longer, more detailed chapter. For each scene, give me both the first opening paragraph, and the last, final paragraph of that longer, more detailed version. Label them as Opening Paragraph and Final Paragraph. The opening paragraph should introduce the scene. The final paragraph should set up the story for the following scene, which will come immediately afterwards. The last paragraph of the final scene should set the story up for the following chapter, which will come immediately afterwards.

### Level 4: Paragraphs

> Me: Given the following book outline, and the following draft of Chapter 1, write a longer, more detailed version of Scene 1. The scene must begin and end with the following paragraphs: (opening and closing paragraphs here)

### Continuity Notes

> Me: Please briefly note any important details or facts from the scene below that you will need to remember while writing the rest of the book, in order to ensure continuity and consistency. Label these Continuity Notes.

> Me: Combine and summarize these notes with the existing previous Continuity Notes below.

在创作过程中，她还特别提到了两个有意思的点， 一个是GPT-4居然自发创作了一首谜语诗歌，：

> “Within my walls I hold a sea,
Yet not a drop of water you’ll see.
Many paths there are to roam,
But only one will lead you home.
What am I?”

谜底是地图

另外有几处GPT-4提到了下一章的内容，成功的接上了之前章节的结尾。

有网友问她有没有尝试多做几个答案来让自己选择，她说自己并没有这么做，除非她发现一些严重的影响流程上的问题，或者是逻辑问题。总共算起来也就出现4-5次。所以说将近95%的时间都是GPT-4 一次性生成的。 

也有网友在读了她的小说之后说看起来一般，并没有专业作家写的号。她同意这一点，但这不是她关注的点，因为这只是作为AI可以完成一本完整小说的例证。

她也提到了相对于GPT-3来说，是不是必须得用GPT-4来完成这件事情。她说她尝试了GPT-3，但是遇到了问题，主要的问题是非常容易跑偏。

## 引用

- [Generating a full-length work of fiction with GPT-4](https://medium.com/@chiaracoetzee/generating-a-full-length-work-of-fiction-with-gpt-4-4052cfeddef3)