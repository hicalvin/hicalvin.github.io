---
layout: post
title:  生成式AI的崛起34：Open Knowledge Format 的实践与思考
date: 2026-06-24 10:00:00 +0800
category: tech
---

Google 最近在它的 `knowledge-catalog` 仓库里发布了 Open Knowledge Format，也就是 OKF。第一眼看上去，它非常简单：一个 Markdown 文件目录、YAML frontmatter、普通链接、可选的 `index.md`、可选的 `log.md`，再加上一些用来描述知识的轻量约定。它不是一个新的数据库，也不是一个复杂的知识图谱产品，更像是一种文档约定。

但我觉得，这恰恰是它有意思的地方。

很长一段时间里，知识管理像是一个大家都在意、但又很少真正正面解决的问题。我们都会抱怨 wiki 过时、上下文缺失、链接散落、文档只有写的人自己懂。但这个问题经常停留在工具选择层面：到底用 Confluence、Notion、Google Docs、Markdown，还是别的东西？

OKF 像是一个更大的信号。如果 Andrej Karpathy 的 LLM-wiki 更像是一种个人实践，那么 Google 把 OKF 作为 spec 发布出来，就说明这个方向正在变得更普遍：文档不再只是写给人看的，它正在变成人和 AI Agent 共同使用的上下文。

过去，文档主要是给人看的参考资料。教程帮助人学习一个东西，手册解释系统如何工作，wiki 页面记录一段内部知识，方便以后有人搜索。

它的使用方式也很简单：一个人有问题，于是搜索文档，打开几个页面，阅读，然后在自己的脑子里重新拼出上下文。这个过程本来就不轻松，但至少读者是人。人可以容忍模糊，可以猜一个标题大概是什么意思，可以问同事，也可以在文档不完整的时候靠经验补足中间缺失的部分。

但这个模式有一个隐藏成本。它默认知识可以被分散保存，然后以后再被找回来；它默认总有人知道哪个页面重要；它默认缺失的上下文可以通过沟通补回来。在真实工作里，这些假设经常并不成立。

我在工作中的 wiki 环境里经常有一个感受：我只有读了很多东西以后，才知道自己到底应该读什么。

当我需要理解一个新项目时，知识经常散落在很多页面里。一个页面解释某个团队，另一个页面解释某个项目模块，还有一个页面记录几个月前的某个决定。某个图表里有关键指标，某个 schema 里有数据模型，一部分上下文在源代码里，还有一部分上下文只在某个同事脑子里，而这个同事可能已经转组，甚至已经离开公司。

更加严重的一个问题是，有时候这些知识已经过时，你根本没法从文档里找出正确的答案，因为这些文档无法随着时间的推移而更新。你只能去问同事，而同事可能已经离开了团队，或者已经忘记了当时的决策背景。这个时候，文档就不再是一个可靠的参考资料，而是一个潜在的陷阱。有时候我们只能转向代码、日志或者其他非文档的资料去寻找答案，而这些资料可能也不完整，或者需要花费更多的时间去理解，而且同样存在过时的问题。

问题不只是搜索花时间。更深的问题是，我很难获得完整图景。如果每个人读到的是不同的一小部分页面，那大家进入规划和讨论时，脑子里的 mental model 就是不一样的。一个人理解架构，另一个人只理解客户问题，还有一个人只记得某个旧决定。当共享图景缺失时，规划会更难，讨论会更长，团队 ownership 重新规划时风险也会更高。

而且过往解决这个问题的办法，往往是新建一套系统，这不仅不能解决老问题，还会因为新系统的引入让知识的分散变得更加严重。 

AI Agent 让文档问题变得更加明显。

当读者只有人时，模糊的文档虽然痛苦，但有时候还能勉强撑住。可当读者也包括 AI Agent 时，模糊的文档就会直接变成能力上限。Agent 需要的上下文必须可读、可链接、有边界、足够新，并且容易遍历。糟糕的标题、缺失的 index、断裂的上下文、散落的假设，不只是让人读得慢，也会让 Agent 的回答和推理变差。

我真正关心的变化是：文档正在从静态参考资料，变成一种运行中的上下文。它不只是我们困惑以后才去读的东西，而是人和 Agent 理解系统、回答问题、规划工作、保存组织记忆的一部分。

这也是为什么 OKF 很适合作为这篇文章的切入点。

用很简单的话说，OKF 的意思是：把知识表示成一组 Markdown 文件。每个 concept 是一个带 YAML frontmatter 的 Markdown 文档。用普通 Markdown links 连接不同 concept。用 `index.md` 帮助读者理解一个目录里有什么。用 `log.md` 记录变化历史。整个格式保持最小化、适合 Git、容易迁移，并且不依赖特殊工具也能读。

这听起来甚至有点太简单了。但简单正是重点。OKF 很接近很多人已经理解的模式：Karpathy 的 LLM-wiki、Obsidian 的双链笔记、Notion 式知识空间，以及 metadata-as-code。它的价值不在于发明一种新的写作方式，而在于把一小组约定固定下来，让知识更容易交换和消费。

对人来说，它提供引导。对 Agent 来说，它提供结构。对团队来说，它提供一种可以持续增长的共享格式，而不需要把所有东西都交给某一个中心化工具。

对我来说，最重要的问题不只是 OKF spec 说了什么。更重要的问题是：如果一个团队采用类似 OKF 的实践，最终的输出会发生什么变化？

一种可能的输出，是一个有引导性的知识库。它不是一堆 wiki 页面，而是一个 knowledge bundle，可以帮助人和 Agent 从整体图景进入细节。它可以指向项目上下文、模块、source code、dashboards、schemas、runbooks、客户问题和历史决策。它可以先告诉读者“这里有什么”，而不是逼读者把所有页面都打开一遍以后才知道自己该看什么。

另一种可能的输出，是更好的 single source of truth。它不是一个完美的中心大脑，而是一个被维护的知识层，可以减少重复解释，也可以减少对某几个同事个人记忆的隐藏依赖。当团队 ownership 发生变化时，这样的知识库可以降低透明度风险。当新人加入时，它可以降低 onboarding 摩擦。当客户问题出现时，它可以帮助 AI Agent 基于人也信任的结构化上下文来回答。

Knowledge-base AI Agent 的能力，很大程度上取决于它能读到什么样的 knowledge base。如果文档是碎片化、过时、无结构的，那 Agent 只是一个界面更好的搜索框。但如果知识库是有引导、有链接、有引用、持续维护的，Agent 才可能成为真正的 operational assistant。

其实我自己已经在做一个很小版本的类似实践。

比如，我会用 file-tree Markdown 文件告诉 Agent 某个 folder 或 file structure 大概长什么样，这样 Agent 不需要每次都从零开始推断。我也会用 `log.md` 记录 AI Agent 做过哪些变化。这些实践都很小，但它们是有意义的。它们帮助 Agent 用更少上下文理解文件分布、历史变化和边界。

我比较确定的是，这样做可以节省 LLM context。相比每次都让模型重新发现整个结构，我可以给它一个更紧凑的 map。但我还不确定的是，这到底能多大程度提升 Agent 的实际表现。它只是减少 token 使用吗？它会让 Agent 更可靠吗？它会提升规划质量吗？这些问题还需要继续观察。

但这种不确定并不是缺点。它反而是理解 OKF-like practice 的正确方式。重点不是相信一个 spec 可以神奇地解决知识管理问题。重点是建立一种约定，让我们可以实践、观察，然后继续改进。

OKF 最后会不会成为一个被广泛采用的格式，我觉得不是最重要的。

更重要的是它代表的方向。文档正在从只给人看的参考资料，变成人和 Agent 共享的记忆。一个好的文档不再只是解释某件事的页面，它也是更大知识系统里的一个节点：可链接、可索引、有引用、有版本历史，并且能同时被人和机器读取。

在 AI Agent 时代，问题不再只是“我们应该把文档写在哪里？”更好的问题是：“我们的文档实践，最终应该创造什么样的知识输出？”

如果输出只是更多页面，那问题仍然存在。如果输出是一个有引导性的知识库、一个共享的项目图景，并最终支撑一个能基于可信上下文回答问题的 AI Agent，那么文档就不再只是文档。

**它会变成组织记忆的运行层。**

---

Google recently published the Open Knowledge Format, or OKF, in its `knowledge-catalog` repository. At first glance, it looks simple: a directory of Markdown files, YAML frontmatter, normal links, optional `index.md`, optional `log.md`, and a few lightweight conventions for describing knowledge. It is not a new database. It is not a complex knowledge graph product. It is closer to a documentation convention.

But I think that is exactly why it is interesting.

For a long time, knowledge management felt like a problem everyone cared about but nobody wanted to touch directly. We all complained about outdated wiki pages, missing context, scattered links, and documents that only made sense to the person who wrote them. But the problem often stayed at the level of tooling preference: should we use Confluence, Notion, Google Docs, Markdown, or something else?

OKF feels like a broader signal. If Andrej Karpathy's LLM-wiki idea represents an individual practice, then Google publishing OKF as a spec suggests that this direction is becoming more general: documentation is no longer only for humans to read. It is becoming shared context for both people and AI agents.

Traditionally, documentation was human reference material. A tutorial helped a human learn something. A manual explained how a system worked. A wiki page captured a piece of internal knowledge so that someone could search for it later.

The workflow was simple: a person had a question, searched for documents, opened several pages, read them, and reconstructed the context in their own head. This was already difficult, but at least the reader was human. Humans can tolerate ambiguity. We can guess what a vague title means. We can ask colleagues. We can read between the lines when a document is incomplete.

But this model has a hidden cost. It assumes that knowledge can be scattered and still recovered later. It assumes that someone will know which page matters. It assumes that missing context can be repaired through conversation. In real work, those assumptions often fail.

One pain I often feel in workplace wiki environments is that I do not know what to read until I have already read too much.

When I need to understand a new project, the knowledge is often spread across many pages. One page explains a team. Another page explains one project module. Another page records a decision from months ago. A chart contains useful metrics. A schema explains the data model. Some context lives in source code. Some context lives only in a colleague's memory, and that colleague may already have moved to another team or left the company.

An even more serious problem is that sometimes the knowledge is already outdated. You cannot find the correct answer from the documents because the documents did not evolve with time. You can only ask colleagues, but those colleagues may have already left the team, or may have forgotten the decision context from that time. At that moment, documentation is no longer a reliable reference. It becomes a potential trap. Sometimes we have to turn to code, logs, or other non-documentation materials to find the answer, but those materials may also be incomplete, harder to understand, and outdated in their own ways.

The problem is not only that search takes time. The deeper problem is that I miss the whole picture. If everyone reads a different subset of pages, everyone enters planning and discussion with a different mental model. One person understands the architecture. Another only understands the customer issue. Another only remembers an old decision. When the shared picture is missing, planning becomes harder, discussion becomes longer, and ownership replanning becomes riskier.

Another common way to solve this problem is to create a new system. But often, this does not solve the old problem. Instead, the introduction of a new system makes knowledge fragmentation even worse.

AI agents make this documentation problem more visible.

When the reader is only human, vague documentation is painful but sometimes survivable. When the reader is also an AI agent, vague documentation becomes a direct limitation. An agent needs context that is readable, linked, scoped, current, and easy to traverse. Poor titles, missing indexes, broken context, and scattered assumptions do not only slow people down. They also make agent answers weaker.

This is the shift I care about: documentation is moving from static reference to operational context. It is not just something we read after we get confused. It becomes part of how people and agents understand a system, answer questions, plan work, and preserve organizational memory.

This is why OKF is a useful trigger for this conversation.

In plain language, OKF says: represent knowledge as a bundle of Markdown files. Each concept is a Markdown document with YAML frontmatter. Use normal Markdown links to connect concepts. Use `index.md` to help readers discover what is inside a directory. Use `log.md` to record change history. Keep the format minimal, Git-friendly, portable, and readable without special tooling.

This sounds almost too simple. But the simplicity is the point. OKF is close to patterns many people already understand: Karpathy's LLM-wiki idea, Obsidian-style linked notes, Notion-like knowledge spaces, and metadata-as-code. Its value is not that it invents a new way to write. Its value is that it pins down a small set of conventions that make knowledge easier to exchange and consume.

For humans, this gives guidance. For agents, it gives structure. For teams, it creates a shared format that can grow over time without requiring one central tool to own everything.

For me, the most important question is not only what the OKF spec says. The more important question is: if a team adopts an OKF-like practice, what changes in the output?

One possible output is a guided knowledge base. Not a pile of wiki pages, but a knowledge bundle that helps people and agents move from the whole picture to details. It can point to project context, modules, source code, dashboards, schemas, runbooks, customer issues, and historical decisions. It can show what exists before forcing the reader to open every page.

Another possible output is a better single source of truth. Not a perfect central brain, but a maintained knowledge layer that reduces duplicated explanations and hidden dependencies on individual colleagues. When team ownership changes, this kind of knowledge base can reduce transparency risk. When new people join, it can reduce onboarding friction. When a customer question arrives, it can help an AI Agent answer from the same structured context that humans trust.

This is where the idea becomes practical. A knowledge-base AI Agent is only as good as the knowledge base it can read. If the documents are fragmented, outdated, and unstructured, the agent becomes another search box with a nicer interface. But if the knowledge base is guided, linked, cited, and maintained, the agent can become a real operational assistant.

I am already doing a small version of this in my own workspace.

For example, I use file-tree Markdown files to explain what a folder or file structure looks like, so an agent does not need to infer everything from scratch. I also use `log.md` files to record changes made by AI agents. These are small practices, but they matter. They help the agent understand distribution, history, and boundaries with less context.

I am confident this saves LLM context. Instead of asking the model to rediscover the whole structure every time, I can give it a compact map. What I am less sure about is how much this improves actual agent performance. Does it only reduce token usage? Does it make the agent more reliable? Does it improve planning quality? Those are still open questions.

But this uncertainty is not a weakness. It is the right way to think about OKF-like practices. The point is not to believe that a spec magically solves knowledge management. The point is to create a convention that lets us practice, observe, and improve.

OKF may or may not become a widely adopted format. That is not the most important thing for me.

The more important point is the direction it represents. Documentation is changing from human-only reference into shared memory for people and agents. A good document is no longer only a page that explains something. It is also a node in a larger knowledge system: linked, indexed, cited, versioned, and readable by both humans and machines.

In the AI Agent age, the question is no longer only "Where should we write the docs?" The better question is: "What kind of knowledge output do we want our documentation practice to create?"

If the output is only more pages, the problem remains. If the output is a guided knowledge base, a shared project picture, and eventually an AI Agent that can answer from trusted context, then documentation becomes much more than documentation.

**It becomes the operating layer of organizational memory.**

References

- GoogleCloudPlatform `knowledge-catalog`: Open Knowledge Format `okf/SPEC.md`
- Andrej Karpathy's LLM-wiki idea
- Obsidian-style linked notes and bi-directional knowledge practice
