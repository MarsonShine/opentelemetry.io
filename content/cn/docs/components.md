# 组件

组成 OpenTelemetry 的主要组件

OpenTelemetry 目前是由下面几个主要部分组成的：

- [跨语言规范](https://opentelemetry.io/docs/reference/specification/)
- [OpenTelemetry 收集器](https://opentelemetry.io/docs/collector)
- [各种语言的 SDK](https://opentelemetry.io/docs/instrumentation)
- [各种语言的仪表库(instrumentation libraries)](https://opentelemetry.io/docs/concepts/instrumenting-library/)
- [各种语言的自动仪表化](https://opentelemetry.io/docs/concepts/instrumenting/#automatic-instrumentation)
- [K8s Operator](https://opentelemetry.io/docs/k8s-operator)

OpenTelemetry 允许您替换需要使用供应商特定的 SDK 和工具来生成和导出遥测数据的需求。

## 规范

描述了对所有实现的跨语言要求和期望。除了术语的定义，该规范还定义了以下内容：

- **API**：定义了数据类型和操作，用于生成和关联追踪(trace)、指标(metrics)和日志(log)数据。
- **SDK**：定义了对 API 的特定语言实现的要求。配置、数据处理和输出的概念也在此定义。
- **数据**：定义了遥测后端可以提供支持的 OpenTelemetry 协议（OTLP）和厂商无关的语义约定。

更多信息，参见[规范](https://opentelemetry.io/docs/reference/specification/)

此外，在 [proto 仓储库](https://github.com/open-telemetry/opentelemetry-proto)中可以找到针对 API 概念的大量注释的 protobuf 接口文件。

## 收集器

OpenTelemetry 收集器是一个厂商无关的代理，可以接收、处理和输出遥测数据。它支持接收多种格式的遥测数据（如OTLP、Jaeger、Prometheus 以及许多商业/专有工具）并将数据发送到一个或多个后端。它还支持在遥测数据被导出之前对其进行处理和过滤。Collector contrib 包带来了对更多数据格式和供应商后端的支持。

更多信息，请参见[收集器](https://opentelemetry.io/docs/collector/)。

## 语言 SDKs

OpenTelemetry 还提供了各种语言 SDK，让您可以使用 OpenTelemetry API 使用所选语言生成遥测数据，并将该数据导出到首选的后端。这些 SDK 还让您集成常用库和框架的仪器库，以便您可以连接到应用程序中的手动仪器。

更多信息，请参见[仪器化](https://opentelemetry.io/docs/concepts/instrumenting)。

> 所谓手动仪器(manual instrumentation)：可以理解为将手动与自动仪器(instrumentation libraries)连接起来。手动仪器是指手动在应用程序中添加的，而自动仪器指的是使用自动仪器库在应用程序中添加的仪器。在使用 OpenTelemetry 语言 SDK 时，你可以将手动添加的仪器与自动仪器库中的仪器一起使用，从而更好地生成和导出遥测数据。

## 仪表库

OpenTelemetry 支持大量的组件，从支持的语言的流行库和框架中生成相关的遥测数据。例如，来自 HTTP 库的入站和出站请求将产生关于这些请求的数据。

一个长期的目标是，流行的库被编写成开箱即可观察到的，这样就不需要拉到一个单独的组件。

更多信息，请参见 [Instrumenting Libraries](https://opentelemetry.io/docs/concepts/instrumenting/#automatic-instrumentation)。

## K8s Operator

OpenTelemetry 运营商是 Kubernetes 运营商的一个实现。操作员负责管理 OpenTelemetry 收集器和使用 OpenTelemetry 的工作负载的自动测量。

更多信息，请参加 [K8s Operator](https://opentelemetry.io/docs/k8s-operator/)

