---
layout: post
title: "假如我来说...OpenTelemetry"
date: 2024-06-27 12:23:50 +0800
category: tech
---


![](https://images.unsplash.com/photo-1594729095022-e2f6d2eece9c?q=80&w=3500&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

-- *by Markus Spiske in Unsplash*

在云原生项目的开发过程中，你将不可避免地接触到一些行业内的热门术语，例如 Kubernetes（简称 K8S）和 Prometheus。这些术语背后，是一个致力于云原生技术生态的庞大开源社区。这个社区专注于开发和维护各种框架与工具，并致力于制定相关标准。他们以开放和中立的姿态，已经取得了以下成就：

- 成功管理了187个项目，其中包括26个已经成熟并"毕业"的项目，以及37个正在孵化中的项目。
- 拥有来自全球的24.3万名贡献者。
- 影响力遍及193个国家。

这个社区名为 CNCF，即 Cloud Native Computing Foundation。CNCF 目前拥有745名正式成员和8.7万名社区成员，共同推动云原生技术的发展和创新。

今天介绍的 OpenTelemetry，是一个专注于系统可观测性机制建立的兴趣小组， 于2019年被 CNCF 接收，并于2021年进入了孵化这一成熟度级别。根据 OpenTelemetry 的治理委员会于[2019年发表的文章](https://opentelemetry.io/blog/2019/opentelemetry-governance-committee-explained/)：

> The main objective of the OpenTelemetry project is to make robust, portable telemetry a built-in feature of cloud-native software. The most effective way to do it is to build a community of passionate people, from existing ecosystem with the diverse expertise and experience. This community will build a project that is attractive to users, who will use it to **instrument** their software, as well as **telemetry** vendors, who will build solutions that work with the open standards.

在 OpenTelemetry 的首页，也清楚地写着它存在的价值：

> OpenTelemetry is a collection of APIs, SDKs, and tools. Use it to instrument, generate, collect, and export telemetry data (metrics, logs, and traces) to help you analyze your software’s performance and behavior.

总结一下，OpenTelemetry 这个 SIG (special interest group)的重点，就是为了**让各种不同的软件通过 Telemetry(遥测) 具备 Observability(可观测性)**。 

## Observability

那么，什么是 Observability（可观测性）？

> Observability lets you understand a system from the outside by letting you ask questions about that system without knowing its inner workings. Furthermore, it allows you to easily troubleshoot and handle novel problems, that is, “unknown unknowns”. It also helps you answer the question “Why is this happening?”

也就是说，对于一个系统的外部使用者或调用者，即使你不了解该系统的内部实现，你也可以通过**向该系统提问**，来判断系统是否正常运行，甚至了解异常情况发生的原因。

为了应对这些**问题**，目标系统需要具备一些**回答**能力，这些回答能力通过释放**信号**来实现。信号的形式包括踪迹（Trace）、指标（Metrics）以及日志（Log）。为了让一个软件系统具备这种回答问题的能力，需要一套开放的方法论，使不同的软件开发者能够轻松应用，而 OpenTelemetry 就提供了这样一套机制，从而使软件系统具备可观测性。

> :bulb: Telemetry refers to data emitted from a system and its behavior. The data can come in the form of traces, metrics, and logs.

那么，我们需要一个软件系统回答的最重要的问题是什么？ 可靠性（Reliability），也就是说，你当前的服务是否满足用户的预期？包括但不限于：

- 你的系统是否24*7小时都在运行
- 你的*加入购物车*功能是否总能正确添加用户想要的商品
- *结算*功能是否总能准确列出订单的数量和商品的总额
- ...

这些基本功能就是你的系统或服务存在的意义。对于可靠性，我们需要各种指标来衡量，这些指标从应用层面到物理系统层面都有不同的分布，来告知系统维护者和使用者当前软件系统的运行状况、潜在隐患，甚至是已经出现的问题。

基于这些指标，我们需要有一个标准来定义，当指标达到某个程度时，系统是正常的，而当指标低于这一程度时，系统服务就会被认定为受损。这个标准就是 SLI（Service Level Indicator）。

SLI 反映的是当前的状态，而作为系统运维人员，我们需要对 SLI 设定治理目标，以确保我们的优化和改进措施有明确的方向，这个目标就是 SLO（Service Level Objective）。SLO 也是软件系统可以向外部组织承诺的标准，更重要的是，要将 SLO 与软件系统的商业价值结合起来，确保目标的制定是实际且合理的。

回到 OpenTelemetry，它的对象是各种软件系统发出的信号（Signal），包括收集、处理和发出信号。这些信号告知外部用户系统当前或过去一段时间的运行状态。例如，主板的温度、CPU 空闲时间、磁盘的剩余容量等。此外，还可以是一连串贯穿多个子系统的事件。对于观察者来说，可能需要通过汇集各种信号，来发现系统潜在的问题，最终告知用户该系统是否健康，即可靠性是否达标。

## Telemetry 

"Telemetry" 这个概念在中文中通常被翻译为“遥测”。遥测是一种远程测量和监控技术，它允许数据从一个地方（通常是传感器或设备）传输到另一个地方（通常是监控站或数据中心）进行分析和处理。这种技术广泛应用于各种领域，包括气象学、航空、航天、工业自动化、医疗监控等。

遥测技术的关键特点包括：

- 远程数据采集：通过传感器收集数据，这些数据可以是温度、压力、速度、位置等物理量。
- 数据传输：采集到的数据通过有线或无线的方式传输到接收端。这可能包括使用无线电波、卫星通信、互联网等通信手段。
- 实时监控：数据传输到监控中心后，可以实时显示和分析，以便进行即时的决策和响应。
- 自动化控制：在某些系统中，遥测不仅用于监控，还可以与自动化控制系统相结合，实现远程控制功能。

遥测技术使得人们能够在不直接接触设备或环境的情况下，获取和处理信息，大大提高了效率和安全性。例如，在医疗领域，遥测可以用来远程监控患者的生理参数；在环境监测中，遥测站可以远距离收集气候数据。

说到信号，形式各种各样。在 OpenTelemetry 这个 SIG 里面定义的最主要的有四种形式的信号

### Trace

Trace 的含义是痕迹，或者踪迹。法证界有句非常有名的话：

> Every contact leaves a trace 凡走过必留下痕迹  -- 法证之父埃德蒙.罗卡

在云原生系统中，[Trace](https://opentelemetry.io/docs/concepts/signals/traces/) 是指一个请求贯穿整个系统留下的路径。如果打开浏览器的开发者模式，打开网络板块，然后在地址栏对任意一个网站发起一个请求，那么在下面就能展现出这个请求在服务端给你应答的各种资源和结果，包括图片、文字、文件等等。

Trace 的好处是提供了一个请求在经过整个系统后留下的完整路径，无论这套系统是简单的单体系统，还是复杂的多个微服务的系统。让这个路径得以呈现的基本单元是 [Span](https://opentelemetry.io/docs/concepts/signals/traces/#spans)。Span 代表了一条请求路径下的其中一个操作单元，是 Trace 里面的最小单位。它可以有上一级的 Span，或者同级的 Span。

### Metrics 指标

Metrics 是我们日常生活中非常熟悉的一个名词。最近的杭州连续降雨，那么每天的降雨量就是一个指标，包括实时温度这些都是。在 OpenTelemetry 文档中，指标是指在运行时捕获的测量值。Metrics 绝对不只是一个数值，要让数值具有意义，还需要发生时的时间点，以及相关的元数据。这点也很好理解，否则数字就没有意义。

在系统的 Metrics 里面，我们关注的重要指标是那些能告诉我们系统可靠性和响应能力方面的，而在那些跟具体业务相关的指标里面，业务人员关心的是那些能告诉他们用户体验、用户满意度、业务转化率等等的指标。

基于这些指标，各个相关人员可以设置自己关心的报警，从而当指标严重偏离期望值时可以采取响应的措施。

### Logs 日志

Log 体现的是在某一个时间点发生的一次事件记录。和 Metrics 的数值形式不同，Log 通常都是带有时间戳的文本。这些文本内容也许是格式化的，比如像 Apache、Tomcat 这些网络中间件的日志，也可能是非结构化的，比如: `Hello World!!!`。从可观测性的角度，当然推荐是结构化的，这样可以通过代码更容易地解析内容，从而获得必要的分析。如果把日志写得像散文一般，对于后续的自动化分析就会非常不便。

在 OpenTelemetry 的定义里面，所有不属于 Trace 和 Metrics 的，都属于 Log。由于各种软件都自带一套自己的日志输出系统，这也导致 OpenTelemetry 这个 SIG 很难重新定义一套 Log 系统来统一各种不同的软件，所以他们在这块的角色更多扮演的是*桥*的功能，来连接不同的 Log 系统。

### Baggage 上下文

不确定是否由于 `Context` 被太多软件语言使用，OpenTelemetry 选用了 `Baggage` 来代表那些可以穿行于各种不同的信号之间的上下文信息。Baggage 实际上就是一个键值对，所以使用者可以自己定义各种他认为需要在上下文之间传输的键值，从而体现在其他三个信号体（Trace、Metrics、Logs）当中。

所以对于一些业务相关的信息，特别是那些从一个请求发生就需要存在的属性，比如 AccountID，UserID，ProductID，original IP 等等，都可以放到 Baggage 里面用来串联业务相关的信息。

小例子:

> Propagating this information using baggage allows for deeper analysis of telemetry in a backend. For example, if you include information like a User ID on a span that tracks a database call, you can much more easily answer questions like “which users are experiencing the slowest database calls?” You can also log information about a downstream operation and include that same User ID in the log data.

## 接入

OpenTelemetry 的接入方式灵活多样，主要可以分为以下三种：

### 零代码接入

零代码接入方式允许开发者在不修改应用源码的情况下，实现可观测性。这种方式主要通过配置应用所依赖的中间件、数据库连接、消息队列等基础设施来实现。例如，可以通过设置环境变量或使用配置文件来启用OpenTelemetry的自动检测和数据收集功能。

- **优点**：无需修改代码，快速部署，适合快速迭代的环境。
- **缺点**：可能无法提供完全定制化的监控需求。

### 基于代码的接入

基于代码的接入方式适合那些在开发初期就考虑了可观测性的系统。开发者可以利用OpenTelemetry提供的API和SDK，直接在代码中嵌入可观测性逻辑，从而实现更精细的监控和跟踪。

- **优点**：高度可定制，能够精确控制数据收集的粒度和范围。
- **缺点**：需要在代码中添加额外的逻辑，增加了开发和维护的复杂性。

#### 实现步骤

1. **引入SDK**：在项目中引入OpenTelemetry的SDK。
2. **配置API**：使用OpenTelemetry的API来生成追踪、度量和日志。
3. **发送数据**：配置数据导出器，将收集到的数据发送到指定的后端服务。

### 库封装接入

OpenTelemetry还提供了封装了可观测性功能的库，这些库可以直接被应用程序调用，从而简化了可观测性的集成过程。

- **优点**：简化开发流程，开发者无需深入了解OpenTelemetry的内部实现。
- **缺点**：可能受限于库的API，不如直接使用SDK灵活。

#### 使用场景

- **微服务架构**：在微服务架构中，使用封装好的库可以快速实现跨服务的追踪和监控。
- **第三方服务集成**：当需要集成第三方服务时，使用OpenTelemetry的库可以确保监控数据的一致性。

### 结合使用

在实际应用中，这三种方式可以根据具体需求和场景灵活结合使用。例如，可以在基础架构层面使用零代码接入，而在业务逻辑层面使用基于代码的接入，以达到既快速部署又能满足定制化需求的平衡。

## Collector 收集器

对于那些简单的系统，通常只需通过 API 或 SDK 直接向外部发送 telemetry 数据即可。然而，作为一种通用的最佳实践，OpenTelemetry 推荐使用 Collector。Collector 使服务能够轻松实现重试、批量处理、加密以及过滤敏感数据等功能。

![](https://opentelemetry.io/docs/collector/img/otel-collector.svg)

OpenTelemetry 提供了通用的实现方式，确保系统在不断扩展的过程中，依然能够持续提供高质量的可观测性数据。

> [Demo Screenshots](https://opentelemetry.io/docs/demo/screenshots/)



## Links

> OpenTelemetry provides a standard for instrumentation that is independent of the tools where logs, metrics and traces are collected. 
>
> [YT: You MUST Instrument Your Code With OpenTelemetry (OTEL)!](https://www.youtube.com/watch?v=oe5YYh9mhzw&t=947s)
