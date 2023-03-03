# 日志

日志是一个有时间戳的文本记录，可以是结构化的（推荐），也可以是非结构化的，带有元数据。虽然日志是一个独立的数据源，但它们也可以被附加到跨度上。在 OpenTelemetry 中，任何不属于分布式追踪或度量的数据都是一个日志。例如，事件是一种特定类型的日志。日志通常用于确定问题的根本原因，通常包含关于谁改变了什么以及改变的结果信息。

> 更多信息，参见[日志规范](https://opentelemetry.io/docs/reference/specification/overview/#log-signal)