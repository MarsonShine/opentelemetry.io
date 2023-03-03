# 概述

本文档概述了 OpenTelemetry 项目并定义了重要的基本术语。

可以在词汇表中找到其他[术语](../../glossary.md)定义。

## OpenTelemetry 客户端架构

![](../../asserts/architecture.png)

在最高层面上，OpenTelemetry 客户端被组织成了[信号](https://opentelemetry.io/docs/reference/specification/glossary/#signals)。每个信号提供一种专门的可观测性形式，例如追踪、指标和包裹是三个独立的信号。信号共享一个通用子系统——上下文传播——但它们相互独立地运行。

每个信号提供了一种描述自身的软件机制。例如，Web 框架或数据库客户端等代码库依赖于各种信号以便描述自身。OpenTelemetry 仪表化代码可以混合到该代码库中的其他代码中。这使得 OpenTelemetry 成为一个[横切关注点](https://en.wikipedia.org/wiki/Cross-cutting_concern)——一种混合到许多其他软件中以提供价值的软件。由于其本质，横切关注点违反了核心设计原则——关注点分离。因此，OpenTelemetry 客户端的设计需要额外的关注和注意，以避免为依赖这些横切 API 的代码库创建问题。

OpenTelemetry 客户端的设计旨在将必须作为横切关注点导入的每个信号的部分与可以独立管理的部分分开。OpenTelemetry 客户端还被设计为可扩展框架。为了实现这些目标，每个信号由四种类型的软件包组成：API、SDK、语义约定（Semantic Conventions）和贡献软件包（Contrib）。

### API

SDK 是 OpenTelemetry 项目提供的 API 的实现。在应用程序中，SDK 由应用程序所有者安装和管理。请注意，SDK 包括其他公共接口，这些接口不被视为 API 包的一部分，因为它们不是横切关注点。这些公共接口被定义为构造函数和插件接口。应用程序所有者使用 SDK 构造；插件作者使用 SDK 插件接口。仪表化作者不应直接引用任何 SDK 包，只能引用 API。

### 语义约定

语义约定指定了用于描述应用程序常见观察概念、协议和操作的键和值。

- [资源约定](https://opentelemetry.io/docs/reference/specification/resource/semantic_conventions/)
- [跨度约定](https://opentelemetry.io/docs/reference/specification/trace/semantic_conventions/)
- [指标约定](https://opentelemetry.io/docs/reference/specification/metrics/semantic_conventions/)

收集器和客户端库都应该自动生成语义约定的键和枚举值到常量中（或者是语言的习惯等价物）。生成的值不应该在稳定的包中分发，直到语义约定稳定。[YAML](https://github.com/open-telemetry/opentelemetry-specification/blob/main/semantic_conventions/_index.md) 文件必须用作生成的真相源。每种语言实现应该为[代码生成](https://github.com/open-telemetry/build-tools/tree/main/semantic-conventions#code-generator)器提供语言特定的支持。

### 贡献软件包

OpenTelemetry 项目维护与重要的用于观测现代 Web 服务的开源项目的集成。API 集成的示例包括用于 Web 框架、数据库客户端和消息队列的仪表化。SDK 集成的示例包括插件，用于将遥测导出到流行的分析工具和遥测存储系统。

某些插件，例如 OTLP Exporters 和 TraceContext Propagators，是 OpenTelemetry 规范所必需的。这些必需插件作为 SDK 的一部分包含在其中。

**可选的插件和仪表化包是与 SDK 分离的并且可选的，称为 Contrib包**。API Contrib 指仅依赖于 API 的包；SDK Contrib 指还依赖于 SDK 的包。

术语“Contrib”特指由 OpenTelemetry 项目维护的插件和仪表化的集合，而不是指托管在其他地方的第三方插件。

### 版本控制与稳定性

OpenTelemetry 重视稳定性和向后兼容性。详情请参阅版[本控制和稳定性指南](https://opentelemetry.io/docs/reference/specification/versioning-and-stability/)。

## 追踪信号

分布式追踪是指一组事件，这些事件由一个单一的逻辑操作触发，在应用程序的各个组件之间进行整合。一个分布式追踪包含跨越进程、网络和安全边界的事件。一个分布式追踪可以在某人按下网站上的按钮以启动操作时启动 - 在这个例子中，追踪将表示由按下按钮引发的请求链中处理的下游服务之间的调用。



