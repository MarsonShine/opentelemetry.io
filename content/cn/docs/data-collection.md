# 数据采集

OpenTelemetry 项目通过 OpenTelemetry 采集器来收集遥测数据。

OpenTelemetry 项目通过 OpenTelemetry 采集器来收集遥测数据。OpenTelemetry 采集器提供了一种厂商无关的实现方式，用于接收、处理和导出遥测数据。它消除了需要运行、操作和维护多个代理/收集器以支持开源可观测数据格式（例如 Jaeger、Prometheus 等）并发送到一个或多个开源或商业后端的需求。此外，采集器还使最终用户能够控制他们的数据。采集器是仪表库导出其遥测数据的默认位置。

> 采集器可以作为发行版提供，更多信息见[这里](https://opentelemetry.io/docs/concepts/distributions)。

## 部署

OpenTelemetry 采集器提供一个二进制文件和两种部署方法：

- Agent（代理）：在应用程序上运行的采集器实例或与应用程序在同一主机上运行（例如，二进制文件、sidecar 或 daemonset）。
- Gateway（网关）：一个或多个作为独立服务运行的采集器实例（例如，容器或 deployment），通常每个集群、数据中心或区域一个。

有关如何使用采集器的信息，请参阅[入门文档](https://opentelemetry.io/docs/collector/getting-started)。

## 组件

采集器通常由以下三个组件组成：

- 接收器（receivers）：将数据收集到采集器中；可以是推或拉模式
- 处理器（processors）：对接收到的数据进行处理
- 导出器（exporters）：将接收到的数据发送到目标；可以是推或拉模式

这些组件是通过管道（pipelines）启用的。可以通过 YAML 配置定义多个组件实例和管道。

有关这些组件的更多信息，请参阅[配置文档](https://opentelemetry.io/docs/collector/configuration)。

## 仓库

OpenTelemetry 项目提供两个版本的采集器。

- [Core](https://github.com/open-telemetry/opentelemetry-collector/releases)：基础组件，如配置和普遍适用的接收器、处理器、输出器和扩展。
- [Cortrib](https://github.com/open-telemetry/opentelemetry-collector-contrib/releases)：核心的所有组件加上可选的或可能的实验性组件。为流行的开源项目提供支持，包括 Jaeger、Prometheus 和 Fluent Bit。还包含更多专门的或供应商特定的接收器、处理器、输出器和扩展。