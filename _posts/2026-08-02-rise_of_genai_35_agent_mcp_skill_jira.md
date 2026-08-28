---
layout: post
title:  生成式AI的崛起35：Agent、MCP 和 SKILL：从我的 Jira 工作流理解 AI 的三个组成部分
date: 2026-08-02 10:00:00 +0800
category: tech
---

今天讲讲跟 AI 相关的几个名词：Agent、MCP 和 SKILL。它们在 AI 讨论中经常出现，但我发现很多人对它们的理解还停留在表面。听多了甚至容易混淆，所以通过我在 Jira 工作流中的实践，我对它们有了更具体的理解。

这里我用一个专门关系 Jira Task，也就是平时我们工作的一个任务单位来举例。我们用的是两周一次的 Sprint，也就是迭代周期，管理任务的工具就是 Jira，Task 当然就是记录在 Jira 里面的任务了。对于 Jira 的操作，以前都是通过浏览器完成，在有了 AI 以后，说实话我已经很久没有打开浏览器来操作 Jira 了，基本上都是假手给一个数字助手，也就是 Agent - `jira-operator`。这里我拿一个最日常的请求作为例子：“告诉我当前 Sprint 的状态。”  

这句话看起来很简单，但要得到一个真正有用的结果，背后需要完成好几个判断：
- 当前到底是哪一个 Sprint？
- 我属于哪个团队？
- 应该从 Jira 取哪些数据？
- 我希望看到什么样的报告？
- 报告应该保存在哪里？

这个小小的工作流，帮助我用更具体的方式理解了 AI 领域经常出现的三个词：Agent、MCP 和 SKILL。对我来说，它们是同一个系统中的三个组成部分：Agent 是承担角色并做决定的工作者，SKILL 描述工作应该怎样完成，MCP 则负责让 Agent 连接到 Jira 这样的外部系统。

## Agent：一个能调用工具的数字工作者

Agent 不只是一个回答问题的聊天机器人。它是一套能够理解意图、判断下一步行动、使用工具，并持续执行直到得到结果或需要人介入的工作流。

[OpenAI 关于构建 Agent 的实践指南](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)把 Agent 的基本组成概括为三部分：负责推理和决策的模型、负责获取信息或执行操作的工具，以及定义行为和安全边界的指令。当这几部分组合起来，并允许 Agent 根据工作状态选择工具时，它才真正具备了 Agent 的工作方式。

我有时会把 Agent 形容成一个数字人，因为这个比喻很直观：它有自己的角色，可以完成多个相关任务，也可以根据上下文响应请求。但从工程角度看，更准确的说法是：Agent 是一个有角色边界的工作流，由模型、工具、指令和执行循环组成。

在我的工作空间里，`jira-operator` Agent 负责普通的 Jira 操作。它可以创建、更新和添加标签，也可以生成报告。Jira hygiene 不属于它的职责，因为那是另一个 Agent 负责的工作。定义一个 Agent 做什么很重要，定义它不做什么同样重要。

## MCP：连接 AI 与外部系统的协议

MCP 是 Model Context Protocol，也就是模型上下文协议。[MCP 官方规范](https://modelcontextprotocol.io/specification/2025-06-18/server/index)将它定义为一种开放协议，用来把 LLM 应用连接到外部数据源和工具。它规范了 Host、Client 和 Server 之间的关系：应用发起连接，Client 负责连接，Server 提供上下文和能力。

[Anthropic 在 2024 年开源并介绍了 MCP](https://www.anthropic.com/news/model-context-protocol)，它的目标是让 AI 助手能够连接到数据实际存在的地方，包括业务工具、内容仓库和开发环境。理解 MCP 最简单的比喻，是把它看成 AI 世界里的 USB Type-C：一个相对统一的连接方式，可以让 AI 应用更容易接入不同的系统。

不过，这个比喻需要一个补充：MCP 并不意味着 API 消失了。MCP Server 的后面仍然可以使用现有 API、数据库或其他集成方式。MCP 的价值在于，AI 应用可以通过一个更一致的协议去发现和使用外部上下文与工具，而不必为每一个系统都采用完全不同的连接模型。

MCP 规范中包含多种能力，例如 Resources、Prompts 和 Tools。放到 Jira 工作流里，最关键的是：Agent 可以通过 MCP 连接的服务读取 Jira 数据，也可以在授权范围内执行操作。

## SKILL：把工作经验写下来

SKILL 可以理解为可复用的工作经验。它描述一个重复性场景应该怎样处理：哪些上下文重要、应该经过哪些步骤、需要考虑哪些边界情况，以及最终输出应该是什么样子。

在我的本地工作空间里，SKILL 通常用 Markdown 编写。这样做的好处是，我可以直接阅读和修改它，让工作流随着实践不断演化。SKILL 还可以保存那些不适合每次都重新写进 prompt 的偏好。例如，我可以在里面定义“当前 Sprint”应该怎样判断、如何识别我的团队，以及 Sprint 报告中哪些字段最重要。

[OpenAI Academy 对 Skills 和 Agents 的解释](https://academy.openai.com/en/public/clubs/news-organizations-b9osl/videos/skills-vs-agents-2026-07-13)提供了一个很清晰的区分：Skill 是关于工作应该如何完成的可复用模板，而 Agent 是能够收集材料、使用工具、遵循指令并应用这个 Skill 的工作流。

我在实践中还有一个更具体的体会：SKILL 不应该只是很长的一段自然语言说明。当准确性和一致性很重要时，最好让 Markdown 和代码一起工作。Markdown 记录经验和期望行为，代码则可以让重复性的解析、筛选、排序、格式化和文件生成更加确定。

## 实例：从一句话到一份 Jira 报告

当我向 `jira-operator` 请求当前 Sprint 的状态时，Agent 首先会根据 SKILL 中定义的项目和组织上下文，理解这句简短的话到底意味着什么。实际过程大概是这样：

1. 识别当前 Sprint。
2. 根据项目和组织上下文，识别我所属的团队。
3. 把 Sprint 和团队作为参数，通过 MCP 调用 Jira，获取相关数据。
4. 根据 SKILL 中的报告偏好，筛选和组织返回结果。
5. 在本地生成 Markdown 报告，并告诉我文件保存在哪里。
6. 如果我明确要求 HTML，则按照一致的格式生成 HTML 报告。

这中间最重要的地方，是 Agent 并不是只把 Jira API 的结果原样返回。它需要先理解我的请求，再决定参数和输出形式。

数据返回之后，Agent 并不会把所有字段原样打印出来。我的偏好是高层次报告。因为我通常可以从 issue title 理解上下文，所以不需要重复每一条 issue 的 description。对我来说，最关键的信息是 status、assignee 和 priority。

所以，最后得到的并不是“AI 返回的一堆 Jira 数据”，而是一份经过角色、连接方式、工作经验和输出偏好共同塑造的报告。

整个过程可以概括为：

```text
用户请求
    ↓
Agent 理解角色和上下文
    ↓
SKILL 定义工作方式和报告偏好
    ↓
MCP 连接 Jira 数据和操作
    ↓
代码支持可重复的处理和格式化
    ↓
本地 Markdown 或 HTML 报告
```

## 把三个词放进同一个工作模型

现在我会这样解释它们之间的关系：

- **Agent**：谁在做这件事，以及谁负责做决定。
- **SKILL**：这件事应该怎样完成。
- **MCP**：Agent 如何连接外部数据和工具。

这个模型也说明了，不能把它们都笼统地称为“AI 自动化”。如果没有正确的工具连接，模型就拿不到 Jira 的上下文；如果只有工具连接，没有 SKILL，结果可能只是数据被取出来，却没有按照我习惯的方式组织；如果只有 SKILL，没有 Agent 去执行，它也无法真正参与工作流。

真正有用的结果，来自这几部分的组合。

这个模型也让边界变得清楚。我的 Jira operator 可以执行普通 Jira 操作和生成报告，但它不负责 hygiene check。这个职责由另一个 Agent 处理。清晰的职责边界不是事后补上的限制，而是 Agent 设计的一部分。

## 实践总结

我最重要的体会是：Agent 的能力并不只由背后的模型决定。它最终是否有用，还取决于它能访问什么上下文、遵循什么指令、使用哪些工具、有没有代码支持重复性操作，以及它的职责边界是否清楚。

所以，对我来说，`SKILL.md` 不只是文档。它是一份简短的工作经验记录。它告诉 Agent，在某个项目里一句简短的话是什么意思，哪些信息重要，什么样的输出才有价值，以及工作应该在哪里停止。当代码和它配合起来时，这些经验就更容易被稳定地重复使用。

## 当前产出与价值

通过这个 Jira 工作流，我现在可以用一句自然语言请求完成一条相对完整的链路：

- 不需要先手动查找当前 Sprint。
- 不需要每次重新解释我属于哪个团队。
- 不需要重新说明报告只关注哪些字段。
- 不需要手动复制和整理 Jira 数据。
- 需要时可以在 Markdown 和 HTML 之间选择输出格式。

这并不意味着 Agent 取代了我的判断。我仍然需要确认上下文、检查结果，并在工作流不符合预期时修改 SKILL 或代码。但重复性的查找、筛选和格式化工作，已经可以沉淀成一个可复用的系统。

## 结尾：三个概念如何协作

这就是我在 Jira 工作中用到的跟 AI 操作相关的基本架构：Agent 是工作者，SKILL 是工作经验，MCP 是连接外部世界的方式。

如果只记住一句话，可以这样理解：Agent 决定做什么，SKILL 规定怎样做，MCP 负责连接需要访问的系统。代码则让其中重复性较高的部分更加稳定。

## 引用

- [OpenAI：A practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/2025-06-18/server/index)
- [Anthropic：Introducing the Model Context Protocol](https://www.anthropic.com/news/model-context-protocol)
- [OpenAI Academy：Skills vs. Agents](https://academy.openai.com/en/public/clubs/news-organizations-b9osl/videos/skills-vs-agents-2026-07-13)

#ai #agent #mcp #skill #jira #agenticengineering

---

I have been using my local `jira-operator` Agent more frequently while organizing my local Agent workflow. One of the shortest requests I give it is: “Show me the status of the current sprint.”

The sentence sounds simple, but a useful answer requires several decisions. Which sprint is current? Which team do I belong to? What Jira data should be retrieved? What kind of report do I want to read? Where should the report be saved?

This small workflow helped me understand three terms that appear frequently in AI discussions: Agent, MCP, and SKILL. I see them as three parts of one system. The Agent is the worker that owns a role and makes decisions. The SKILL describes how the work should be done. MCP lets the Agent connect to an external system such as Jira.

## Agent: a digital worker that can use tools

An Agent is more than a chatbot that answers questions. It is a workflow that can interpret an intention, decide what steps are needed, use tools, and continue until it reaches an outcome or needs human input.

[OpenAI’s practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/) describes three basic components: a model for reasoning and decision-making, tools for gathering context or taking action, and instructions that define behavior and guardrails. When these components work together, and the Agent can select tools according to the state of the workflow, it starts to behave like an Agent rather than a simple question-and-answer interface.

I sometimes describe an Agent as a digital human because the analogy is easy to understand. It has a role, can perform several related tasks, and can respond using available context. From an engineering perspective, a more precise definition is a role-based workflow made from a model, tools, instructions, an execution loop, and clear boundaries.

In my workspace, the `jira-operator` Agent owns ordinary Jira operations. It can create, update, and label issues, and it can generate reports. Jira hygiene is outside its responsibility because another Agent owns that work. Defining what an Agent must not do is as important as defining what it can do.

## MCP: the protocol connecting AI to external systems

MCP stands for Model Context Protocol. The [official MCP specification](https://modelcontextprotocol.io/specification/2025-06-18/server/index) describes it as an open protocol for connecting LLM applications with external data sources and tools. It standardizes the relationship between a host, a client connector, and a server that provides context and capabilities.

[Anthropic introduced MCP as an open standard](https://www.anthropic.com/news/model-context-protocol) for connecting AI assistants to the systems where data lives, including business tools, content repositories, and development environments. The easiest analogy is USB Type-C: one relatively common connection pattern can make it easier for an AI application to work with different systems.

There is an important qualification. MCP does not mean that APIs disappear. An MCP server can still use an existing API, database, or other integration behind the protocol. MCP’s value is that an AI application can discover and use external context and tools through a more consistent interface instead of requiring a completely different integration model for every system.

The MCP specification includes capabilities such as resources, prompts, and tools. In a Jira workflow, the important part is that the Agent can use an MCP-connected service to retrieve Jira data or perform an authorized operation.

## SKILL: turning working experience into reusable instructions

A SKILL is reusable operational knowledge. It describes how a recurring use case should be handled: which context matters, which steps to follow, which edge cases to consider, and what the final output should look like.

In my local workspace, a SKILL is usually written in Markdown. This makes it possible for me to read and revise it as the workflow evolves. It can preserve preferences that would be inconvenient to repeat in every prompt. For example, I can define what “current sprint” means, how my team should be identified, and which fields matter in a sprint report.

[OpenAI Academy’s explanation of Skills and Agents](https://academy.openai.com/en/public/clubs/news-organizations-b9osl/videos/skills-vs-agents-2026-07-13) offers a useful distinction: a Skill is a reusable template for how work should be done, while an Agent is the workflow that gathers material, uses tools, follows instructions, and applies that Skill.

I have also learned that a SKILL should not be only a long natural-language document. When accuracy and consistency matter, Markdown should be accompanied by code. Markdown records the experience and intended behavior. Code can make repeated parsing, filtering, sorting, formatting, and file creation more deterministic.

## The example: from one sentence to a Jira report

When I ask the `jira-operator` for the status of the current sprint, the Agent first uses the project and organizational context defined in the SKILL to understand what my short request means. The actual process is roughly:

1. Identify the current sprint.
2. Identify my team from project and organizational context.
3. Pass the sprint and team as parameters to Jira through MCP.
4. Filter and organize the returned data according to the SKILL’s reporting preferences.
5. Generate a local Markdown report and tell me where it was saved.
6. If I explicitly ask for HTML, generate it using a consistent format.

The important point is that the Agent does not simply return the raw result of a Jira API call. It first interprets the request, then decides the parameters and the output format.

The Agent also does not print every field exactly as it arrives. My preference is a high-level report. I usually understand the context from issue titles, so I do not need every issue description repeated. The key information for me is status, assignee, and priority.

The result is therefore not just “a set of Jira data returned by AI.” It is a report shaped by a role, a connection, documented working experience, and an output preference.

The workflow can be summarized as:

```text
User request
    ↓
Agent interprets the role and context
    ↓
SKILL defines the workflow and report preference
    ↓
MCP connects to Jira data and actions
    ↓
Code supports repeatable processing and formatting
    ↓
Local Markdown or HTML report
```

## Putting the three terms into one working model

This is how I now explain the relationship:

- **Agent**: who is doing the work and making the decisions.
- **SKILL**: how the work should be done.
- **MCP**: how the Agent reaches external data and tools.

This model also explains why the three terms should not be collapsed into the vague idea of “AI automation.” Without the right tool connection, the model cannot access the relevant Jira context. With a tool connection but no SKILL, the data may be retrieved without being organized in the way I need. With a SKILL but no Agent to execute it, the workflow cannot actually do anything.

The useful result comes from combining these parts.

The model also makes boundaries visible. My Jira operator can perform normal Jira operations and generate reports, but it does not own hygiene checks. A separate Agent handles that responsibility. Clear boundaries are part of the Agent’s design, not a limitation added afterward.

## What I learned from using this pattern

My most important lesson is that an Agent’s practical capability is not determined only by the model behind it. It also depends on the context it can access, the instructions it follows, the tools it can use, the code supporting repeated operations, and the clarity of its responsibility boundaries.

For me, `SKILL.md` is therefore more than documentation. It is a compact record of working experience. It tells the Agent what a short phrase means in a particular project, which information matters, what output is useful, and where the workflow should stop. When code accompanies it, that experience becomes easier to apply consistently.

## Current output and value

Through this Jira workflow, I can now use one natural-language request to complete a fairly long chain:

- I do not need to find the current sprint manually first.
- I do not need to explain my team context every time.
- I do not need to restate which fields the report should contain.
- I do not need to copy and organize Jira data manually.
- I can choose between Markdown and HTML when needed.

This does not mean the Agent replaces my judgment. I still need to confirm the context, review the result, and revise the SKILL or code when the workflow does not behave as expected. But the repetitive work of finding, filtering, and formatting information can now be captured as a reusable system.

## Conclusion: how the three concepts work together

This is the basic architecture I see in my Jira practice: the Agent is the worker, the SKILL is the working experience, and MCP is the way to connect to the outside world.

If I had to reduce it to one sentence: the Agent decides what to do, the SKILL defines how to do it, and MCP connects the Agent to the system it needs to access. Code makes the repetitive parts more stable.

## References

- [OpenAI: A practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/2025-06-18/server/index)
- [Anthropic: Introducing the Model Context Protocol](https://www.anthropic.com/news/model-context-protocol)
- [OpenAI Academy: Skills vs. Agents](https://academy.openai.com/en/public/clubs/news-organizations-b9osl/videos/skills-vs-agents-2026-07-13)

#ai #agent #mcp #skill #jira #agenticengineering

