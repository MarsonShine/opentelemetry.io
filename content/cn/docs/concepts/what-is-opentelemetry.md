# 什么是 OpenTelemetry

***关于OpenTelemetry的背景信息***

微服务架构使开发者能够更快、更独立地构建和发布软件，因为他们不再受制于与单体架构相关的复杂的发布流程。

随着这些分布式系统的扩展，开发人员越来越难看到自己的服务是如何依赖或影响其他服务的，特别是在部署后或停电期间，这时速度和准确性至关重要。

> [可观测性](https://opentelemetry.io/docs/concepts/observability-primer/#what-is-observability)使开发者和运营商都有可能获得对其系统的这种可见性。

## 那又怎样？

为了使一个系统可被观察到，它必须被仪表化(instrumented)。也就是说，代码必须发出[追踪](https://opentelemetry.io/docs/concepts/observability-primer/#distributed-traces)、[度量](https://opentelemetry.io/docs/concepts/observability-primer/#reliability--metrics)和[日志](https://opentelemetry.io/docs/concepts/observability-primer/#logs)。然后，这些被检测的数据必须被发送到Observability后端。现在有很多可观测的后端，从自我托管的开源工具（如 [Jaeger](https://www.jaegertracing.io/) 和 [Zipkin](https://zipkin.io/)），在到商业 SaaS 产品。

过去，对代码进行检测的方式各不相同，因为每个Observability后端都有自己的检测库和代理来向工具发送数据。

这意味着向可观测后端发送数据时没有标准化的数据格式。此外，如果一个公司选择更换可观测后端，就意味着他们必须重新对其代码进行测量，并配置新的代理，以便能够向所选择的新工具发射遥测数据。

> 由于缺乏标准化，最终的结果是缺乏数据的可移植性和用户维护仪表库(instrumented libs)的负担。

认识到标准化的需要，云计算社区走到了一起，两个开源项目应运而生。[OpenTracing](https://opentracing.io/)（[云原生计算基金会（CNCF）](https://www.cncf.io/)项目）和 [OpenCensus](https://opencensus.io/)（[谷歌开源](https://opensource.google/)社区项目）。

**OpenTracing** 提供了一个供应商中立的 API，用于将遥测数据发送到可观测后端；然而，它依赖于开发者实现自己的库来满足规范。

**OpenCensus** 提供了一套特定语言的库，开发者可以用它来检测他们的代码，并将其发送到他们支持的任何一个后端。

## 你好，OpenTelemetry

为了实现一个统一的标准，在[2019年5月](https://www.cncf.io/blog/2021/08/26/opentelemetry-becomes-a-cncf-incubating-project/)，OpenCensus 和 OpenTracing 合并成为 OpenTelemetry（简称OTel）。作为 CNCF 的孵化项目，OpenTelemetry 融合了两者的优点，除此之外还有更多创新和改进。

OTel的目标是提供一套标准化、与厂商无关的SDK、API和工具，用于将数据传送到一个可观测性后端（即开源或商业厂商）的数据摄取、转换和发送。

## OpenTelemetry 能为我做什么？

OTel 得到了云供应商、[厂商](https://opentelemetry.io/ecosystem/vendors/)和最终用户的广泛支持和采用。它为您提供了以下功能：

- [每种编程语言](https://opentelemetry.io/docs/instrumentation)都有一个单一、与厂商无关的仪表化库，支持自动和手动仪表化。
- 一个单一的与厂商无关的[收集器](https://opentelemetry.io/docs/collector)二进制文件，可以以多种方式部署。
- 一个端到端实现，用于生成、发出、收集、处理和导出遥测数据。
- 通过配置实现向多个目的地并行发送数据的完全控制权。
- 开放的标准语义约定，确保厂商无关的数据收集。
- 支持多种[上下文传播](https://opentelemetry.io/docs/reference/specification/overview/#context-propagation)格式，以帮助随着标准的发展进行迁移。


- 无论您在可观测性旅程的哪个阶段，都有前进的道路。

OpenTelemetry 支持多种开源和商业协议、格式和上下文传播机制，并提供对 OpenTracing 和 OpenCensus 项目的桥接，因此采用 OpenTelemetry 非常容易。

## OpenTelemetry不是什么

OpenTelemetry 不像 Jaeger 或 Prometheus 那样的可观察性后端。相反，它支持将数据导出到各种开源和商业后端。它提供了一个可插拔的架构，因此可以很容易地添加其他技术协议和格式。