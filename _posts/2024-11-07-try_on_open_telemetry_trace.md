---
layout: post
title: 试用 Opentelemetry Trace
date: 2024-11-07 19:19:50 +0800
category: learning
---

## 概念介绍

### OpenTelemetry 

OpenTelemetry是一个由CNCF（Cloud Native Computing Foundation）支持的可观测性框架和工具包，旨在创建和管理遥测数据，如链路（traces）、指标（metrics）和日志（logs）。 OpenTelemetry提供了一套API、SDK、工具和集成方法，以帮助开发者和运维团队收集和分析遥测数据，从而提高分布式系统的透明度和可观测性。 它是一个供应商和工具无关的平台，意味着可以与各种可观测性后端一起使用，包括开源工具如Jaeger和Prometheus，以及商业化产品。

### Trace 的概念

在分布式追踪中，Trace是表示一个完整的请求处理流程，它由多个Span组成，每个Span代表请求在单个服务中的处理过程。 Span是Trace的基本工作单位，可以嵌套，通过父级Span ID来表示子操作。 这样，通过Span之间的关系，可以构建出一个完整的Trace，从而追踪整个请求的处理路径。 Trace和Span共同帮助开发者理解分布式系统中请求的流动和延迟情况。


### Zipkin 的概念和运行方式

Zipkin是一个分布式追踪系统，它收集解决服务架构中的延迟问题所需的计时数据，并提供数据的收集和查找功能。 核心概念包括Trace、Span、Trace ID、Annotations、Binary Annotations、Collector以及Query and Visualization。 Zipkin通过一个全局唯一的Trace ID将不同的Span关联到同一个Trace上，从而构建起整个请求的调用链路。

Zipkin的工作流程包括：在用户发起调用时，Zipkin客户端为整条调用链路生成一个全局唯一的Trace ID，并为每次分布式调用生成一个Span ID。一个Trace由一组Span组成，可以看作是以Trace为根节点，Span为若干子节点的树。 通过这种方式，Zipkin能够详细记录和展示服务间的调用链路，帮助开发者定位性能瓶颈和故障点

### Jaegar

Jaeger是一个开源的分布式跟踪系统，由Uber Technologies开发并贡献给云原生计算基金会（CNCF）。它受到Dapper和OpenZipkin的启发，兼容OpenTracing以及Zipkin追踪格式。Jaeger主要用于监控和诊断基于微服务的分布式系统，包括分布式上下文传播、分布式事务监控、根本原因分析、服务依赖性分析以及性能/延迟优化等功能

### Grafana

Grafana是一个开源的度量分析和可视化套件，它提供了一个功能丰富的仪表板，用于展示和监控各种指标和日志。Grafana支持多种数据源，包括但不限于Prometheus、InfluxDB、Elasticsearch、MySQL、PostgreSQL等，使其能够广泛应用于不同的监控场景。

## 安装和配置

## 1. 安装 Zipkin 以进行可视化

Zipkin 可以通过 Docker 快速安装

### 步骤 1: 运行 Zipkin 容器

在您的终端中运行以下命令，以在后台启动 Zipkin 容器，并将其端口映射到本地的 `9411` 端口。

```bash
docker run -d -p 9411:9411 openzipkin/zipkin
```

### 步骤 2: 访问 Zipkin Dashboard

启动 Zipkin 后，您可以通过访问以下 URL 来查看 Zipkin 的仪表板： [http://localhost:9411/](http://localhost:9411/)

## 2. 安装 Jaeger

Jaeger 是一个开源的端到端分布式追踪系统，它包括 Zipkin 兼容的 UI，所以如果没有安装 Zipkin 的话也可以直接安装 Jaegar 全家桶。以下是如何安装 Jaeger 的步骤。

### 步骤 1: 安装 Jaeger-all-in-one

Jaeger 提供了一个 all-in-one 安装包，包括所有必需的组件。您可以通过以下命令安装 Jaeger：

```bash
docker run --rm --name jaeger \
  -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \
  -p 6831:6831/udp \
  -p 6832:6832/udp \
  -p 5778:5778 \
  -p 16686:16686 \
  -p 4317:4317 \
  -p 4318:4318 \
  -p 14250:14250 \
  -p 14268:14268 \
  -p 14269:14269 \
  -p 9411:9411 \
  jaegertracing/all-in-one:1.62.0

```
```

### 步骤 2: 访问 Jaeger Dashboard

安装 Jaeger 后，您可以通过以下 URL 访问其仪表板： [http://localhost:16686/](http://localhost:16686/)

## 3. 安装 Grafana

Grafana 是一个跨平台的开源分析和监控解决方案，它可以用来可视化追踪数据。对于目前很多数据呈现都通过 Grafana 展示 Prometheus，那么对于 Trace 的数据，只要在 Grafana 里面增加一个数据源就可以获得Trace 的视觉化图标。

### 步骤 1: 更新 Homebrew

如果您使用的是 macOS，首先更新您的 Homebrew：

```bash
brew update
```

### 步骤 2: 安装 Grafana

使用 Homebrew 安装 Grafana：

```bash
brew install grafana
```

### 步骤 3: 重置管理员密码

重置 Grafana 的管理员密码：

```bash
/usr/local/bin/grafana cli --config /usr/local/etc/grafana/grafana.ini --homepath /usr/local/share/grafana --configOverrides cfg:default.paths.data=/usr/local/share/grafana admin reset-admin-password xxx
```

### 步骤 4: 启动 Grafana 服务

启动 Grafana 服务：

```bash
brew services start grafana
```

### 步骤 5: 访问 Grafana Dashboard

启动 Grafana 后，您可以通过以下 URL 访问其仪表板：[http://localhost:3000/](http://localhost:3000/)

### 步骤 6: 配置数据源

在 Grafana 中，您需要将数据源配置为 `Jaeger`。这将允许您在 Grafana 中查看和分析追踪数据。


## 代码和配置

外部环境都好了，接下来就可以写带有 Trace 的代码

### Maven注册依赖

在 `pom.xml` 中需要添加针对 opentelemetry api 和 zipkin exporter 的依赖

```xml
<dependency>  
    <groupId>io.opentelemetry</groupId>  
    <artifactId>opentelemetry-api</artifactId>  
</dependency>  
<dependency>  
    <groupId>io.opentelemetry</groupId>  
    <artifactId>opentelemetry-exporter-zipkin</artifactId>  
</dependency>
```

### 样例代码

#### ExampleConfiguration 

定义一个配置类，用来初始化 TraceProvider 和 Zipkin Exporter:

```java

public final class ExampleConfiguration {  
  
  // Name of the service  
  private static final String SERVICE_NAME = "opentelemetry-trace-demo";  
  
  /** Adds a SimpleSpanProcessor initialized with ZipkinSpanExporter to the TracerSdkProvider */  
  static OpenTelemetry initializeOpenTelemetry(String ip, int port) {  
    String endpoint = String.format("http://%s:%s/api/v2/spans", ip, port);  
    ZipkinSpanExporter zipkinExporter = ZipkinSpanExporter.builder().setEndpoint(endpoint).build();  
  
    Resource serviceNameResource =  
        Resource.create(Attributes.of(ResourceAttributes.SERVICE_NAME, SERVICE_NAME));  
  
    // Set to process the spans by the Zipkin Exporter  
    SdkTracerProvider tracerProvider =  
        SdkTracerProvider.builder()  
            .addSpanProcessor(SimpleSpanProcessor.create(zipkinExporter))  
            .setResource(Resource.getDefault().merge(serviceNameResource))  
            .build();  
    OpenTelemetrySdk openTelemetry =  
        OpenTelemetrySdk.builder().setTracerProvider(tracerProvider).buildAndRegisterGlobal();  
  
    // add a shutdown hook to shut down the SDK  
    Runtime.getRuntime().addShutdownHook(new Thread(tracerProvider::close));  
  
    // return the configured instance so it can be used for instrumentation.  
    return openTelemetry;  
  }  
}
```

然后就可以写 main 函数

```java
public static void main(String[] args) {  
    // Parsing the input  
    if (args.length < 2) {  
        System.out.println("Missing [hostname] [port]");  
        System.exit(1);  
    }  
  
    String ip = args[0];  
    int port = Integer.parseInt(args[1]);  
  
    // it is important to initialize the OpenTelemetry SDK as early as possible in your process.  
    OpenTelemetry openTelemetry = ExampleConfiguration.initializeOpenTelemetry(ip, port);  
    TracerProvider tracerProvider = openTelemetry.getTracerProvider();  
  
    try {  
        ZipkinExample example = new ZipkinExample(tracerProvider);  
        example.demoTrace();  
    } catch (InterruptedException e) {  
        throw new RuntimeException(e);  
    }  
  
}

public void demoTrace() throws InterruptedException {  
    Span span = tracer.spanBuilder("Demo Trace").startSpan();  
  
    try (Scope scope = span.makeCurrent()) {  
  
        methodA();  
        methodB();  
        methodC();  
  
  
    } catch (RuntimeException | InterruptedException e) {  
        span.recordException(e);  
        throw e;  
    } finally {  
        span.end();  
    }  
  
}
```

在每个具体的 `methodA()`, `methodB()`, 以及 `methodC()`中， 可以继续创建 Span，这些新创建的 Span会自动挂在最外层 Span 的下面。 从 JSON 内容上可以很清楚的看到这个关系。 另外 Trace 提供了一些方法用于给每个 Span 添加更多的信息，例如：

`methodASpan.setAttribute("user", "SpiderMan");` - 来给方法添加一个用户属性

`methodASpan.setStatus(StatusCode.ERROR, "Data Not Found");` - 定义这个 Span 的状态，这个状态可以被吸收到外层 Span 来作为整个 Span 的成功失败状态



```json
"traceID": "55e00ba1ddb5f27b12e1d16aa2327e29",
            "spans": [
                {
                    "traceID": "55e00ba1ddb5f27b12e1d16aa2327e29",
                    "spanID": "5f424cbffc13d841",
                    "operationName": "method A",
                    "references": [
                        {
                            "refType": "CHILD_OF",
                            "traceID": "55e00ba1ddb5f27b12e1d16aa2327e29",
                            "spanID": "8b562110e2f7d918"
                        }
                    ],
                    "startTime": 1730876891727723,
                    "duration": 2007788,
                    "tags": [
                        {
                            "key": "http.method",
                            "type": "string",
                            "value": "GET"
                        },
                        {
                            "key": "internal.span.format",
                            "type": "string",
                            "value": "zipkin"
                        },
                        {
                            "key": "net.host.ip",
                            "type": "string",
                            "value": "10.140.217.177"
                        },
                        {
                            "key": "otel.scope.name",
                            "type": "string",
                            "value": "io.opentelemetry.example.ZipkinExample"
                        },
                        {
                            "key": "otel.scope.name",
                            "type": "string",
                            "value": "io.opentelemetry.example.ZipkinExample"
                        },
                        {
                            "key": "user",
                            "type": "string",
                            "value": "IronMan"
                        }
                    ],
                    "logs": [],
                    "processID": "p1",
                    "warnings": null
                },
```

## 参考
- [OpenTelemetry - Trace](https://opentelemetry.io/docs/concepts/signals/traces/)
- [OpenTelemetry - Trace API](https://opentelemetry.io/docs/specs/otel/trace/api/)
- [Zipkin architecture](https://segmentfault.com/img/remote/1460000042686005)
- [Zipkin链路追踪技术分享与源码解析](https://zhuanlan.zhihu.com/p/81182997)
- [Evolving Distributed Tracing at Uber Engineering](https://www.uber.com/en-JP/blog/distributed-tracing/)
