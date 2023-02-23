# 追踪

追踪(Traces)给我们提供了用户或应用程序发出请求时发生的全貌。

## OpenTelemetry 中的追踪

追踪为我们提供了用户或应用程序发出请求时发生的情况的全貌。OpenTelemetry 为我们提供了一种方法，通过追踪我们的微服务和相关应用，在生产中把可观测性落实到我们的代码中。

样例：

```json
{
    "name": "Hello-Greetings",
    "context": {
        "trace_id": "0x5b8aa5a2d2c872e8321cf37308d69df2",
        "span_id": "0x5fb397be34d26b51",
    },
    "parent_id": "0x051581bf3cb55c13",
    "start_time": "2022-04-29T18:52:58.114304Z",
    "end_time": "2022-04-29T22:52:58.114561Z",
    "attributes": {
        "http.route": "some_route1"
    },
    "events": [
        {
            "name": "hey there!",
            "timestamp": "2022-04-29T18:52:58.114561Z",
            "attributes": {
                "event_attributes": 1
            }
        },
        {
            "name": "bye now!",
            "timestamp": "2022-04-29T18:52:58.114585Z",
            "attributes": {
                "event_attributes": 1
            }
        }
    ],
}
{
    "name": "Hello-Salutations",
    "context": {
        "trace_id": "0x5b8aa5a2d2c872e8321cf37308d69df2",
        "span_id": "0x93564f51e1abe1c2",
    },
    "parent_id": "0x051581bf3cb55c13",
    "start_time": "2022-04-29T18:52:58.114492Z",
    "end_time": "2022-04-29T18:52:58.114631Z",
    "attributes": {
        "http.route": "some_route2"
    },
    "events": [
        {
            "name": "hey there!",
            "timestamp": "2022-04-29T18:52:58.114561Z",
            "attributes": {
                "event_attributes": 1
            }
        }
    ],
}
{
    "name": "Hello",
    "context": {
        "trace_id": "0x5b8aa5a2d2c872e8321cf37308d69df2",
        "span_id": "0x051581bf3cb55c13",
    },
    "parent_id": null,
    "start_time": "2022-04-29T18:52:58.114201Z",
    "end_time": "2022-04-29T18:52:58.114687Z",
    "attributes": {
        "http.route": "some_route3"
    },
    "events": [
        {
            "name": "Guten Tag!",
            "timestamp": "2022-04-29T18:52:58.114561Z",
            "attributes": {
                "event_attributes": 1
            }
        }
    ],
}
```

这个追踪样本输出有三项，分别是 "Hello-Greetings"、"Hello-Salutations" 和 "Hello"。因为每个请求的上下文都有相同的追踪 ID，所有的信息都可以联系在一起。这提供了一个通过请求的各种路线、时间戳和其他属性的追踪。

为了理解 OpenTelemetry 中的追踪是如何工作的，让我们看看在我们的代码中起作用的组件的列表。

- 追踪器(Tracer)
- 追踪器提供者(Tracer Provider)
- 追踪输出器(Tracer Expoter)
- 追踪上下文(Tracer Context)

### 追踪器提供者

追踪器提供者（有时称为 TracerProvider）是一个 Tracers 的工厂。在大多数应用程序中，追踪器提供者被初始化一次，其生命周期与应用程序的生命周期一致。追踪器提供者的初始化也包括资源和导出器的初始化。这通常是使用OpenTelemetry进行追踪的第一步。在一些语言SDK中，已经为你初始化了一个全局Tracer Provider。

### 追踪器

追踪器创建的跨度包含了更多关于一个给定操作的信息，比如一个服务中的请求。追踪器是由追踪器提供者创建的。

### 追踪输出器

追踪输出器将追踪信息发送到一个消费者。这个消费者可以是用于调试和开发时间的标准输出，也可以是 OpenTelemetry 收集器，或任何你选择的开源或供应商的后端。

### 上下文传播

上下文传播(Context Propagation)是实现分布式追踪的核心概念。通过上下文传播，跨度(Spans)可以相互关联，并集合成一个追踪，而不管跨度是在哪里产生的。我们通过两个子概念来定义上下文传播。Context 和 Propagation。

Context 是一个对象，它包含发送和接收服务的信息，以便将一个跨度与另一个跨度相关联，并将其与整个追踪相关联。例如，如果服务A调用服务B，那么其ID在上下文中的服务A的跨度将被用作服务B中创建的下一个跨度的父跨度。

传播是在服务和进程之间移动 Context 的机制。通过这样做，它组装了一个分布式追踪。它序列化或反序列化 Span Context，并提供相关的 Trace 信息，以便从一个服务传播到另一个服务。我们现在有了我们所说的。Trace Context。

Context 是一个抽象的概念--它需要一个具体的实现才能真正发挥作用。OpenTelemetry 支持几种不同的 Context 格式。OpenTelemetry 追踪中使用的默认格式是 W3C `TraceContext`。每个 Context 对象都与一个跨度相关联，并且可以在跨度上访问规范。请看[跨度上下文](https://opentelemetry.io/docs/concepts/signals/traces/#span-context)。

> 更多信息，请参阅[追踪规范](https://opentelemetry.io/docs/reference/specification/overview/#tracing-signal)

## OpenTelemetry 中的跨度

一个跨度(Span)代表一个工作或操作的单位。**跨度是追踪(Tracer)的组成部分**。在 OpenTelemetry 中，它们包括以下信息：

- 名称；Name
- 父跨度 ID
- 开始和结束时间戳
- [跨度上下文(Span Context)](https://opentelemetry.io/docs/concepts/signals/traces/#span-context)
- [属性(Attributes)](https://opentelemetry.io/docs/concepts/signals/traces/#attributes)
- [跨度事件(Span Events)](https://opentelemetry.io/docs/concepts/signals/traces/#span-events)
- [跨度链接(Span Links)](https://opentelemetry.io/docs/concepts/signals/traces/#span-links)
- [跨度状态(Span Status)](https://opentelemetry.io/docs/concepts/signals/traces/#span-status)

样例：

```json
{
  "trace_id": "7bba9f33312b3dbb8b2c2c62bb7abe2d",
  "parent_id": "",
  "span_id": "086e83747d0e381e",
  "name": "/v1/sys/health",
  "start_time": "2021-10-22 16:04:01.209458162 +0000 UTC",
  "end_time": "2021-10-22 16:04:01.209514132 +0000 UTC",
  "status_code": "STATUS_CODE_OK",
  "status_message": "",
  "attributes": {
    "net.transport": "IP.TCP",
    "net.peer.ip": "172.17.0.1",
    "net.peer.port": "51820",
    "net.host.ip": "10.177.2.152",
    "net.host.port": "26040",
    "http.method": "GET",
    "http.target": "/v1/sys/health",
    "http.server_name": "mortar-gateway",
    "http.route": "/v1/sys/health",
    "http.user_agent": "Consul Health Check",
    "http.scheme": "http",
    "http.host": "10.177.2.152:26040",
    "http.flavor": "1.1"
  },
  "events": [
    {
      "name": "",
      "message": "OK",
      "timestamp": "2021-10-22 16:04:01.209512872 +0000 UTC"
    }
  ]
}
```

跨度可以被嵌套，正如父跨度ID的存在所暗示的那样：子跨度代表子操作。这使得跨度能够更准确地捕捉应用程序中所完成的工作。

### 跨度上下文

跨度上下文是每个 Span 上的不可变对象，包括以下内容：

- 代表该跨度是其一部分的追踪ID
- 跨度的跨度ID
- 追踪标志，一种二进制编码，包含关于追踪的信息
- 追踪状态，一个键值对的列表，可以携带供应商特定的追踪信息

**跨度上下文是跨度的一部分**，它被序列化并与[分布式上下文(Distributed Context)](https://opentelemetry.io/docs/concepts/signals/traces/#context-propagation) 和 [Baggage](https://opentelemetry.io/docs/concepts/signals/baggage) 一起传播。

因为跨度上下文包含 Trace ID，所以它在创建[跨度链接](https://opentelemetry.io/docs/concepts/signals/traces/#span-links)时被使用。

### 属性

属性是包含元数据的键值对，你可以用它来注释跨度，以携带关于它所追踪的操作的信息。

例如，如果一个跨度追踪一个在电子商务系统中向用户的购物车添加物品的操作，你可以捕获用户的ID，添加到购物车的物品的ID，以及购物车的ID。

属性有以下规则，每个语言 SDK 都会实现：

- 键必须是非空字符串的值
- 值必须是一个非空字符串、布尔值、浮点值、整数或这些值的一个阵列

此外，还有语义属性（Semantic Attributes），这是已知的元数据的命名惯例，通常存在于常见的操作中。尽可能地使用语义属性命名是很有帮助的，这样常见的各类元数据就可以在不同的系统中实现标准化。

### 跨度事件

跨度事件可以被认为是跨度上的结构化日志消息（或注释），通常用于表示跨度持续期间的一个有意义的、单一的时间点。

例如，考虑在浏览器中的两种情况：

- 追踪页面加载
- 表明一个页面何时具有互动性

跨度最好用于第一种情况，因为它是一个开始和结束的操作。

跨度事件最好用于追踪第二种情况，因为它代表了一个有意义的、单一的时间点。

### 跨度链接

链接的存在是为了让你能把一个跨度与一个或多个跨度联系起来，表明一种因果关系。例如，假设我们有一个分布式系统，其中一些操作通过 Trace 进行追踪。

作为对其中一些操作的回应，一个额外的操作被排队执行，但它的执行是异步的。我们也可以用一个追踪器来追踪这个后续的操作。

我们希望将后续操作的追踪与第一个追踪联系起来，但是我们无法预测后续操作何时开始。我们需要将这两个追踪联系起来，所以我们将使用一个跨度链接。

你可以把第一个追踪中的最后一个跨度与第二个追踪中的第一个跨度联系起来。现在，它们彼此之间有了因果关系。

链接是可有可无的，但它是将追踪跨度相互关联的一个好方法。

### 跨度状态

状态是附加到跨度上的。通常情况下，当应用程序代码中存在一个已知的错误时，你会设置一个跨度状态，例如异常。一个跨度状态将被标记为以下值之一：

- Unset
- Ok
- Error

当一个异常被处理时，一个跨度状态可以被设置为 Error。否则，跨度状态就处于 Unset。通过将跨度状态设置为 Unset，处理跨度的后端现在可以分配一个最终状态。

### 跨度类别

当一个跨度被创建时，它是客户端(Client)、服务器(Server)、内部(Internal)、生产者(Producer)或消费者(Consumer)中的一个。这种跨度为追踪后端提供了一个提示，即追踪应该如何组合。根据 OpenTelemetry 规范，服务器跨度的父级通常是一个远程客户端跨度，而客户端跨度的子级通常是一个服务器跨度。类似地，消费者跨度的父级总是生产者，生产者跨度的子级总是消费者。如果没有提供，跨度类别被认为是内部的。

关于跨度类别的更多信息，请参阅[跨度类别](https://opentelemetry.io/docs/reference/specification/trace/api/#spankind)。

#### 客户端

客户端跨度代表一个同步出站远程调用，如出站 HTTP 请求或数据库调用。请注意，在这种情况下，"同步"并不是指异步/等待，而是指没有排队等待后续处理。

#### 服务端

一个服务器跨度代表一个同步入站的远程调用，如传入的 HTTP 请求或远程过程调用。

#### 内部

内部跨度代表不跨越进程边界的操作。像对一个函数调用或表达式中间件的仪器化，可以使用内部跨度。

#### 生产者

生产者跨度表示创建一个作业，该作业可能在之后被异步处理。它可能是一个远程作业，例如插入到作业队列中的作业或由事件监听器处理的本地作业。

#### 消费者

消费者跨度表示对生产者创建的作业的处理，可能在生产者跨度结束后很久才开始。