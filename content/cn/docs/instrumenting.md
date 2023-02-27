# 仪表化

OpenTelemetry 如何促进应用程序的自动和手动仪表化。

为了使一个系统可以可观测，它必须被仪表化。也就是说，来自系统组件的代码必须发出[追踪](./concepts/signals/traces.md)、[度量](./concepts/signals/metrics.md)和[日志](./concepts/signals/logs.md)。

在不需要修改源代码的情况下，你可以使用自动仪表化从一个应用程序中收集遥测数据。如果你以前使用 APM 代理从你的应用程序中提取遥测数据，[自动仪表化](https://opentelemetry.io/docs/reference/specification/glossary/#automatic-instrumentation)(Automatic Instrumentation) 会给你类似的开箱即用体验。

为了更方便地检测应用程序，你可以通过对 OpenTelemetry APIs 进行编码来[手动检测](https://opentelemetry.io/docs/reference/specification/glossary/#manual-instrumentation)你的应用程序。

为此，你不需要对你的应用程序中使用的所有依赖关系进行检测：

- 你的一些库可以通过直接调用 OpenTelemetry API 本身来观察。这些库有时被称为原生工具。
- 对于没有这种整合的库，OpenTelemetry 项目提供了特定语言的[仪表库](https://opentelemetry.io/docs/reference/specification/overview/#instrumentation-libraries)。

注意，对于大多数语言来说，可以同时使用手动和自动仪表。**自动仪表可以让你快速了解你的应用程序，手动仪表可以让你在代码中嵌入细粒度的观察能力。**

根据你所开发的语言，手动和自动仪表的具体安装机制有所不同，但在下面的章节中涵盖了一些相似之处。

## 自动仪表

如果适用，特定语言的 OpenTelemetry 实现将提供一种无需修改源代码即可仪表化应用程序的方式。尽管底层机制取决于语言，但最少会向应用程序添加 OpenTelemetry API 和 SDK 功能。此外，它们还可能添加一组仪表库和导出器依赖项。

配置可以通过环境变量和可能的特定语言手段，如 Java 中的系统属性。至少，必须配置一个服务名称，以确定被检测的服务。其他各种配置选项也是可用的，可能包括：

- 数据源特定配置
- 导出器配置
- 传播配置
- 资源配置

## 手动仪表

### 导入 OpenTelemetry APIs 和 SDK

你首先需要把 OpenTelemetry 导入到你的服务代码中。如果你正在开发一个库或其他一些旨在被可运行的二进制文件使用的组件，那么你将只依赖 API。如果你的构件是一个独立的进程或服务，那么你就需要依赖 API 和 SDK。关于 OpenTelemetry API 和 SDK 的更多信息，请参见[规范](https://opentelemetry.io/docs/reference/specification/)。

### 配置 OpenTelemetry APIs

为了创建追踪或度量，你需要首先创建一个跟踪器/度量器提供者。一般来说，我们建议 SDK 应该为这些对象提供一个单一的默认提供者。然后，你将从提供者那里获得一个追踪器或测量器实例，并给它一个名称和版本。你在这里选择的名字应该能识别被检测的具体内容--例如，如果你正在编写一个库，那么你应该以你的库命名（例如`com.legitimatebusiness.myLibrary`），因为这个名字将为所有产生的跨度或度量事件命名。我们还建议你提供一个版本字符串（如 semver:1.0.0），与你的库或服务的当前版本相一致。

### 配置 OpenTelemetry SDK

如果你正在建立一个服务流程，你还需要用适当的选项来配置 SDK，以便将你的遥测数据导出到一些分析后端。我们建议通过配置文件或其他机制以编程方式处理这种配置。还有一些你可能希望利用的每一种语言的调整选项。

### 创建遥测数据

一旦你配置了 API 和 SDK，你就可以通过你从供应商那里获得的跟踪器和仪表对象自由地创建跟踪和计量事件。为你的依赖性使用仪表库--查看[登记表](https://opentelemetry.io/ecosystem/registry/)或你的语言资源库以获得更多相关信息。

### 导出数据

一旦你创建了遥测数据，你会想把它送到某个地方。OpenTelemetry 支持两种主要方法将数据从你的进程导出到分析后端，可以直接从进程中导出，也可以通过 [OpenTelemetry 收集器](https://opentelemetry.io/docs/collector)代理。

进程内导出需要你导入并依赖一个或多个导出器，这些库将 OpenTelemetry 的内存跨度和度量对象转换成适合遥测分析工具的格式，如 Jaeger 或 Prometheus。此外，OpenTelemetry 支持一个被称为 `OTLP` 的协议，所有 OpenTelemetry SDK 都支持该协议。这个协议可以用来发送数据到 OpenTelemetry 收集器，这是一个独立的二进制进程，可以作为你的服务实例的代理或边车运行，或在一个单独的主机上运行。然后，收集器可以被配置为转发和输出这些数据到你选择的分析工具。

除了 Jaeger 或 Prometheus 等开源工具外，越来越多的公司支持从 OpenTelemetry 提取遥测数据。详情请见[供应商](https://opentelemetry.io/ecosystem/vendors/)。