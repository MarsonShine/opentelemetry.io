# 术语表

OpenTelemetry 项目使用的一些术语可能对您来说很陌生。此外，该项目可能会对术语的定义与其他人有所不同。本页记录了项目中使用的术语及其含义。

## 通用术语

### 聚合(Aggragation)

将多个测量值组合成关于在程序执行期间的时间间隔内进行的测量的确切或估计统计数据的过程。[Metric](https://opentelemetry.io/docs/concepts/glossary/#metric)，[数据源](https://opentelemetry.io/docs/concepts/glossary/#data-source)使用此术语。

### API

### Application

### APM

### 特性（Attribute）

### 自动仪表（Automatic Instrumentation）

### 包裹（Baggage）

### 客户端库

### 客户端应用程序（Client-side App）

### 采集器（Collector）

### 贡献（Contrib）

### 上下文传播（Context Propagation）

### DAG

[有向无环图](https://en.wikipedia.org/wiki/Directed_acyclic_graph)

### 数据源（Data Source）

详见 [`Signal`](https://opentelemetry.io/docs/concepts/glossary/#signal)

### **规模（Dimension）**

详见[标签（Label）](https://opentelemetry.io/docs/concepts/glossary/#label)

### 分布式追踪（Distributed Tracing）

### **事件（Event）**

Something that happened where representation depends on the [`Data Source`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#data-source). For example, [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span).

### **导出器（Exporter）**

Provides functionality to emit telemetry to consumers. Used by [`Instrumentation Libraries`](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/glossary/#exporter-library) and the [`Collector`](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/collector/configuration#basics). Exporters can be push- or pull-based.

### **字段（Field）**

Name/value pairs added to [`Log Records`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log-record) (similar to [`Attributes`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#attribute) for [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span) and [`Labels`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#label) for [`Metrics`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metric)). See [field spec](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/logs/data-model#field-kinds).

### **gRPC**

A high-performance, open source universal [`RPC`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#rpc) framework. More on gRPC [here](https://grpc.io).

### **HTTP**

Short for [Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol).

### **被仪表化的库（Instrumented Library）**

Denotes the [`Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#library) for which the telemetry signals ([`Traces`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#trace), [`Metrics`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metric), [`Logs`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log)) are gathered. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/glossary/#instrumented-library).

### **仪表化库（Instrumentation Library）**

Denotes the [`Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#library) that provides the instrumentation for a given [`Instrumented Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#instrumented-library). [`Instrumented Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#instrumented-library) and [`Instrumentation Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#instrumentation-library) may be the same [`Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#library) if it has built-in OpenTelemetry instrumentation. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/glossary/#instrumentation-library).

> `Instrumented Library` 指的是已经被 OpenTelemetry 工具自动或手动地注入了 OpenTelemetry 代码的第三方库。这些注入的代码可以帮助收集该库生成的跟踪和度量数据，并将其发送到 OpenTelemetry 收集器进行处理和分析。
>
> `Instrumentation Library` 指的是一组 API 和实现，用于将应用程序中的跟踪和度量数据暴露给 OpenTelemetry 工具。使用 Instrumentation Library，开发人员可以将 OpenTelemetry 代码添加到他们的应用程序中，以便收集关于应用程序性能的有用数据，并将其发送到 OpenTelemetry 收集器进行处理和分析。 **Instrumentation Library 可以包含多个 Instrumentation 模块，每个模块都负责捕获一个特定的操作或技术的跟踪和度量数据。**

### **JSON**

Short for [JavaScript Object Notation](https://en.wikipedia.org/wiki/JSON).

### **Label**

See [Attribute](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#attribute).

### **Language**

Programming Language.

### **Library**

A language-specific collection of behavior invoked by an interface.

### **Log**

Sometimes used to refer to a collection of [`Log Records`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log-record). May be ambiguous, since people also sometimes use [`Log`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log) to refer to a single [`Log Record`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log-record), thus this term should be used carefully and in the context where ambiguity is possible additional qualifiers should be used (e.g. `Log Record`). See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/glossary#log).

### **Log Record**

A recording of an [`Event`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#event). Typically the record includes a timestamp indicating when the [`Event`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#event) happened as well as other data that describes what happened, where it happened, etc. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/glossary#log-record).

### **Metadata**

A name/value pair added to telemetry data. OpenTelemetry calls this [`Attributes`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#attribute) on [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span), [`Labels`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#label) on [`Metrics`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metric) and [`Fields`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#field) on [`Logs`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log).

### **Metric**

Records a data point, either raw measurements or predefined aggregation, as time series with [`Metadata`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metadata). See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/concepts/signals/metrics).

### **OC**

Short form for [`OpenCensus`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#opencensus).

### **OpenCensus**

A set of libraries for various languages that allow you to collect application metrics and distributed traces, then transfer the data to a backend of your choice in real time. [Precursor to OpenTelemetry](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/concepts/what-is-opentelemetry/#so-what). See [more](https://opencensus.io).

### **OpenTracing**

Vendor-neutral APIs and instrumentation for distributed tracing. [Precursor to OpenTelemetry](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/concepts/what-is-opentelemetry/#so-what). See [more](https://opentracing.io).

### **OT**

Short form for [`OpenTracing`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#opentracing).

### **OTel**

Short form for [OpenTelemetry](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/concepts/what-is-opentelemetry).

### **OTelCol**

Short form for [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#collector).

### **OTLP**

Short for [OpenTelemetry Protocol](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/protocol/otlp).

### **Processor**

Operation performed on data between being received and being exported. For example, batching. Used by ['Instrumentation Libraries'](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#instrumentation-library) and the [Collector](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/collector/configuration/#processors).

### **Propagators**

Used to serialize and deserialize specific parts of telemetry data such as span context and [`Baggage`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#baggage) in [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span). See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/instrumentation/go/manual/#propagators-and-context).

### **Proto**

Language independent interface types. See [more](https://github.com/open-telemetry/opentelemetry-proto).

### **Receiver**

Term used by the [`Collector`](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/collector/configuration/#receivers) to define how telemetry data is received. Receivers can be push- or pull-based. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/collector/configuration/#receivers).

### **Request**

See [`Distributed Tracing`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#distributed-tracing).

### **Resource**

Captures information about the entity for which telemetry is recorded. For example, a process producing telemetry that is running in a container on Kubernetes has a pod name, it is in a namespace and possibly is part of a deployment which also has a name. All three of these attributes can be included in the `Resource` and applied to any data source.

### **REST**

Short for [Representational State Transfer](https://en.wikipedia.org/wiki/Representational_state_transfer).

### **RPC**

Short for [Remote Procedure Call](https://en.wikipedia.org/wiki/Remote_procedure_call).

### **Sampling**

A mechanism to control the amount of data exported. Most commonly used with the [`Tracing`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#trace) [`Data Source`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#data-source). See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/sdk#sampling).

### **SDK**

Short for Software Development Kit. Refers to a telemetry SDK that denotes a [`Library`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#library) that implement the OpenTelemetry [`API`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#api).

### **Semantic Conventions**

Defines standard names and values of [`Metadata`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metadata) in order to provide vendor-agnostic telemetry data.

### **Service**

A component of an [`Application`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#application). Multiple instances of a [`Service`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#service) are typically deployed for high availability and scalability. A [`Service`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#service) may be deployed in multiple locations.

### **Signal**

One of [`Traces`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#trace), [`Metrics`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metric) or [`Logs`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#log). More on Signals [here](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/concepts/signals).

### **Span**

Represents a single operation within a [`Trace`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#trace). See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/api#span).

### **Span Link**

A span link is a link between causally-related spans. For details see [Links between spans](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/overview#links-between-spans) and [Specifying Links](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/api#specifying-links).

### **Specification**

Describes the cross-language requirements and expectations for all implementations. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/concepts/components/#specification).

### **Status**

The result of the operation. Typically used to indicate whether an error occurred. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/api#set-status).

### **Tag**

See [`Metadata`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#metadata).

### **Trace**

A [`DAG`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#dag) of [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span), where the edges between [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span) are defined as parent/child relationship. See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/overview#traces).

### **Tracer**

Responsible for creating [`Spans`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#span). See [more](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/api#tracer).

### **Transaction**

See [`Distributed Tracing`](https://github.com/open-telemetry/opentelemetry.io/blob/main/content/en/docs/concepts/glossary.md#distributed-tracing).

### **zPages**

An in-process alternative to external exporters. When included, they collect and aggregate tracing and metrics information in the background; this data is served on web pages when requested. See [more](https://github.com/open-telemetry/opentelemetry-specification/blob/main/experimental/trace/zpages.md).

## 术语补充

### Traces

#### **[Trace API Terminology](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/api)**

#### **[Trace SDK Terminology](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/sdk)**

### Metrics

#### **[Metric API Terminology](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/metrics/api#overview)**

#### **[Metric SDK Terminology](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/metrics#specifications)**

### Logs

#### **[Trace Context Fields](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/logs/data-model#trace-context-fields)**

#### **[Severity Fields](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/logs/data-model#severity-fields)**

#### **[Log Record Fields](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/logs/data-model#log-and-event-record-definition)**

### Semantic Conventions

#### **[Resource Conventions](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/resource/semantic_conventions)**

#### **[Span Conventions](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/trace/semantic_conventions)**

#### **[Metric Conventions](https://github.com/open-telemetry/opentelemetry.io/blob/main/docs/reference/specification/metrics/semantic_conventions)**