# 通用 SDK 配置

用于配置 OpenTelemetry SDK 的通用环境变量。

## `OTEL_SERVICE_NAME`

设置 [service.name](https://opentelemetry.io/docs/reference/specification/resource/semantic_conventions/#service) 资源属性的值。

**默认值：**`"unknown_service"`

如果在 `OTEL_RESOURCE_ATTRIBUTES` 中也提供了 `service.name`，那么 `OTEL_SERVICE_NAME` 将优先。

**例子：**

`export OTEL_SERVICE_NAME="your-service-name"`

## `OTEL_RESOURCE_ATTRIBUTES`

作为资源属性使用的键值对。更多细节请参见[资源 SDK](https://opentelemetry.io/docs/reference/specification/resource/sdk#specifying-resource-information-via-an-environment-variable)。

**默认值：**空

关于常见资源类型应遵循的语义惯例，请参见[资源语义约定](https://opentelemetry.io/docs/reference/specification/resource/semantic_conventions/#semantic-attributes-with-sdk-provided-default-value)。

**例子：**

`export OTEL_RESOURCE_ATTRIBUTES="key1=value1,key2=value2"`

## `OTEL_TRACES_SAMPLER`

指定 SDK 用于对追踪(trace)进行采样的采样器

**默认值：**`"parentbased_always_on"`

**例子：**

`export OTEL_TRACES_SAMPLER="traceidratio"`

`OTEL_TRACES_SAMPLER` 接受的值是：

- `"always_on"`:`AlwaysOnSampler`
- `"always_off"`:`AlwaysOffSampler`
- `"traceidratio"`:`TraceIdRatioBased`
- `"parentbased_always_on"`:`ParentBased(root=AlwaysOnSampler)`
- `"parentbased_always_off"`:`ParentBased(root=AlwaysOffSampler)`
- `"parentbased_traceidratio"`:`ParentBased(root=TraceIdRatioBased)`
- `"parentbased_jaeger_remote"`:`ParentBased(root=JaegerRemoteSampler)`
- `"jaeger_remote"`:`JaegerRemoteSampler`
- `"xray"`:[AWS X-Ray 集中采样（第三方）](https://docs.aws.amazon.com/xray/latest/devguide/xray-console-sampling.html)

## `OTEL_TRACES_SAMPLER_ARG`

指定由 `OTEL_TRACES_SAMPLER` 定义的采样器的参数（如果适用）。只有设置了 `OTEL_TRACES_SAMPLER` 的值，指定的值才会被使用。每个采样器类型都定义了自己的预期输入（如果有的话）。无效的或不被认可的输入会被记录为错误。

**默认值：**空

**例子：**

```shell
export OTEL_TRACES_SAMPLER="traceidratio"
export OTEL_TRACES_SAMPLER_ARG="0.5"
```

根据 `OTEL_TRACES_SAMPLER` 的值，`OTEL_TRACES_SAMPLER_ARG` 可以设置如下：

- 对于 `traceidratio` 和 `parentbased_traceidratio` 采样器：采样概率是一个在 [0..1] 范围内的数字，例如“0.25”。如果未设置，默认为 1.0。
- 对于 `jaeger_remote` 和 `parentbased_jaeger_remote`：该值是逗号分隔的列表：
  - 例如。`"endpointhttp://localhost:14250,pollingIntervalMs=5000,initialSamplingRate=0.25"`
  - `endpoint`：端点格式为 `scheme://host:port` 的 gRPC服务器，为服务提供采样策略([sampling.proto](https://github.com/jaegertracing/jaeger-idl/blob/master/proto/api_v2/sampling.proto))。
  - `pollingIntervalMs`：以毫秒为单位，表示采样器对后端采样策略的更新进行轮询的频率。
  - `initialSamplingRate`：在[0...1] 范围内，当无法到达后端检索采样策略时，它被用作采样概率。一旦采样策略被成功检索到，这个值就不再有影响，因为远程策略将被使用，直到检索到新的更新。

## `OTEL_PROPAGATORS`

指定在逗号分隔的列表中使用的传播器。

**默认值：**`“tracecontext,baggage”`

**例子：**

`export OTEL_PROPAGATORS="b3"`

`OTEL_PROPAGATORS` 接收的值如下：

- `"tracecontext"`:[W3C 追踪上下文](https://www.w3.org/TR/trace-context/)
- `"baggage"`:[W3C 包裹](https://docs.aws.amazon.com/xray/latest/devguide/xray-console-sampling.html)
- `"b3"`: [B3 Single](https://opentelemetry.io/docs/reference/specification/context/api-propagators#configuration)
- `"b3multi"`:[B3 Multi](https://opentelemetry.io/docs/reference/specification/context/api-propagators#configuration)
- `"jaeger"`:[Jaeger](https://docs.aws.amazon.com/xray/latest/devguide/xray-console-sampling.html)
- `"xray"`: [AWS X-Ray](https://docs.aws.amazon.com/xray/latest/devguide/xray-concepts.html#xray-concepts-tracingheader)
- `"ottrace"`:[OT Trace](https://github.com/opentracing?q=basic&type=&language=)
- `"none"`:没有自动配置的传播器。

## `OTEL_TRACES_EXPORTER`

指定使用哪一个导出器来追踪。

**默认值：**`"otlp"`

**例子：**

`export OTEL_TRACES_EXPORTER="jaeger"`

`OTEL_METRICS_EXPORTER` 接受的值如下：

- `"otlp"`:[OTLP](https://opentelemetry.io/docs/reference/specification/protocol/otlp)
- `"prometheus"`:[Prometheus](https://github.com/prometheus/docs/blob/master/content/docs/instrumenting/exposition_formats.md)
- `"none"`:没有自动配置的指标导出器。

## `OTEL_LOGS_EXPORTER`

指定使用哪一个导出器来记录日志。

**默认值：**`"otlp"`

**例子：**

`export OTEL_LOGS_EXPORTER="otlp"`

`OTEL_LOGS_EXPORTER` 接受的值如下：

- `"otlp"`:[OTLP](https://opentelemetry.io/docs/reference/specification/protocol/otlp)
- `"none"`:没有自动配置的日志导出器。

