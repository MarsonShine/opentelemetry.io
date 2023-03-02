# 分发版

分发版（Distribution）与分支（Fork）不应混淆，前者是 OpenTelemetry 组件的自定义版本。

OpenTelemetry 项目由支持多个信号的多个组件组成。OpenTelemetry 的参考实现可用作：

- 特定语言的仪表库
- 一个采集器二进制文件

可以从任何参考实现中创建一个分发版。

## 什么是分发版？

分发版（Distribution）与分支（Fork）不应混淆，前者是 OpenTelemetry 组件的自定义版本。

分发版包装了一个上游 OpenTelemetry 仓库并进行了一些自定义。分发版的自定义内容可能包括：

- 脚本以简化使用或自定义后端或供应商
- 更改默认设置以满足后端、供应商或最终用户的要求
- 其他包装选项可能是特定于供应商或最终用户的
- 比 OpenTelemetry 提供的测试、性能和安全覆盖范围更广
- 比 OpenTelemetry 提供的功能更多的功能
- 比 OpenTelemetry 提供的功能更少的功能

分发版广泛分为以下几类：

- **“纯粹（Pure）”**: 这些分发版提供与上游相同的功能，并且是 100% 兼容的。自定义通常是为了简化使用或打包。这些自定义可能是后端、供应商或最终用户特定的。
- **“加法”**: 这些分发版提供与上游相同的功能以及更多功能。超出纯分发版的自定义将包括包括未上传到 OpenTelemetry 项目的仪表化库或供应商导出器。例如，这可能包括仪表化库或供应商导出器。
- **“减法”**: 这些分发版提供从上游减少的功能集。例如，可能会删除 OpenTelemetry Collector 项目中找到的仪表化库或接收器/处理器/导出器/扩展。这些分发版可能被提供以增加支持性和安全性考虑。

## 谁创建分发版？

任何人都可以创建一个分发版。今天，有几个[供应商](https://opentelemetry.io/ecosystem/vendors/)提供了分发版。此外，如果终端用户希望使用[注册表](https://opentelemetry.io/ecosystem/registry/)中没有上游到 OpenTelemetry 项目的组件，可以考虑创建一个分发版。

## 贡献或分发？

在你继续学习如何创建自己的分发之前，请问自己一些问题，以确定你在 OpenTelemetry 组件上添加的内容是否对每个人都有益，因此应该包含在参考实现中：

- 你的“易用性”脚本是否可以通用化？
- 你对默认设置的更改是否对每个人都是更好的选择？
- 你的其他包装选项是否真的很特别？
- 你的测试、性能和安全覆盖范围是否也可以与参考实现一起使用？
- 你是否与社区核实过你的其他功能是否可以成为标准的一部分？

## 创建自己的分发版

### 采集器

关于如何创建你自己的分发版的指南可以在这篇博文中找到：["建立你自己的 OpenTelemetry 采集器发行版"](https://medium.com/p/42337e994b63)

如果你要建立自己的分发版，[OpenTelemetry 采集器构造器](https://github.com/open-telemetry/opentelemetry-collector/tree/main/cmd/builder)可能是一个好的起点。

### 特定语言的仪表化库

这里有特定的语言可扩展性机制来定制仪表库。

- [Javaagent](https://opentelemetry.io/docs/instrumentation/java/extensions)

## 为什么你应该了解分发版

当你在使用 OpenTelemetry 项目的标志和名称等宣传资料时，要确保你的行为符合 [OpenTelemetry 贡献组织的商业指南](https://github.com/open-telemetry/community/blob/main/marketing-guidelines.md)。

目前 OpenTelemetry 项目不提供对分发版本的认证。在未来，类似于 Kubernetes 项目，OpenTelemetry 可能会对分发版本和合作伙伴进行认证。在评估分发版本时，确保使用该分发版本不会导致供应商锁定。

> 任何关于分发版本的支持都应该来自分发版本的作者而不是 OpenTelemetry 项目的作者。