# OTLP 导出器 Configuration

为你的 OTLP 导出器配置环境变量

## 终结点配置

以下环境变量让你为你的追踪(trace)、指标(metric)和日志(log)配置一个 OTLP/gRPC 或 OTLP/HTTP 终结点。

### `OTEL_EXPORTER_OTLP_ENDPOINT`

任何信号类型的基本端点 URL，并可选择指定端口号。当你向同一个终结点发送多个信号，并希望用一个环境变量来控制终结点时，这很有帮助。

**默认值：**

- gRPC: `"http://localhost:4317"`
- HTTP: `"http://localhost:4318"`

**例子：**

- gRPC: `export OTEL_EXPORTER_OTLP_ENDPOINT="my-api-endpoint:443"`
- HTTP: `export OTEL_EXPORTER_OTLP_ENDPOINT="http://my-api-endpoint/"`

对于 OTLP/HTTP，当这个环境变量被设置时，SDK 中的导出器会构建信号特定的 URL。这意味着，如果你要发送追踪、度量和日志，就会从上面的例子中构建以下 URL。

- Traces: `"http://my-api-endpoint/v1/traces"`
- Metrics: `"http://my-api-endpoint/v1/metrics"`
- Logs: `"http://my-api-endpoint/v1/logs"`

### `OTEL_EXPORTER_OTLP_TRACES_ENDPOINT`

仅用于追踪数据的终结点 URL，可选择指定的端口号。如果使用 OTLP/HTTP，必须以 `v1/traces` 结尾。

**默认值：**

- gRPC:`"http://localhost:4317"`
- HTTP:`"http://localhost:4318/v1/traces"`

**例子：**

- gRPC:`export OTEL_EXPORTER_OTLP_TRACES_ENDPOINT="my-api-endpoint:443"`
- HTTP:`export OTEL_EXPORTER_OTLP_TRACES_ENDPOINT="http://my-api-endpoint/v1/traces"`

### `OTEL_EXPORTER_OTLP_METRICS_ENDPOINT`

仅用于指标数据的终结点 URL，可选择指定端口号。如果使用 OTLP/HTTP，必须以 `v1/metrics` 结尾。

**默认值:**

- gRPC: `"http://localhost:4317"`
- HTTP: `"http://localhost:4318/v1/metrics"`

**例子:**

- gRPC: `export OTEL_EXPORTER_OTLP_METRICS_ENDPOINT="my-api-endpoint:443"`
- HTTP: `export OTEL_EXPORTER_OTLP_METRICS_ENDPOINT="http://my-api-endpoint/v1/metrics"`

### `OTEL_EXPORTER_OTLP_LOGS_ENDPOINT`

仅用于日志数据的终结点 URL，可选择指定端口号。如果使用 OTLP/HTTP，必须以 `v1/metrics` 结尾。

**默认值:**

- gRPC: `"http://localhost:4317"`
- HTTP: `"http://localhost:4318/v1/logs"`

**例子:**

- gRPC: `export OTEL_EXPORTER_OTLP_LOGS_ENDPOINT="my-api-endpoint:443"`
- HTTP: `export OTEL_EXPORTER_OTLP_LOGS_ENDPOINT="http://my-api-endpoint/v1/logs"`

## 头部配置

下面的环境变量让你配置额外的头文件，作为键值对的列表，添加到传出的 gRPC 或 HTTP 请求中。

### `OTEL_EXPORTER_OTLP_HEADERS`

适用于所有出向数据（追踪、指标和日志）的头部集合。

**默认值:** N/A

**例子:** `export OTEL_EXPORTER_OTLP_HEADERS="api-key=key,other-config-value=value"`

### `OTEL_EXPORTER_OTLP_TRACES_HEADERS`

适用于所有出向追踪的头部集合。

**默认值:** N/A

**例子:** `export OTEL_EXPORTER_OTLP_TRACES_HEADERS="api-key=key,other-config-value=value"`

### `OTEL_EXPORTER_OTLP_METRICS_HEADERS`

适用于所有出向指标的头部集合。

**默认值:** N/A

**例子:** `export OTEL_EXPORTER_OTLP_METRICS_HEADERS="api-key=key,other-config-value=value"`

### `OTEL_EXPORTER_OTLP_LOGS_HEADERS`

适用于所有出向日志的头部集合。

**默认值:** N/A

**例子:** `export OTEL_EXPORTER_OTLP_LOGS_HEADERS="api-key=key,other-config-value=value"`

## 超时配置

以下环境变量配置了 OTLP 导出器在传递大批网络数据之前等待的最大时间（以毫秒计）。

### `OTEL_EXPORTER_OTLP_TIMEOUT`

所有传出数据（traces、metrics 和 logs）的超时值，单位是毫秒。

**默认值:** `10000` (10s)

**例子:** `export OTEL_EXPORTER_OTLP_TIMEOUT=500`

### `OTEL_EXPORTER_OTLP_TRACES_TIMEOUT`

所有出向追踪的超时值，单位是毫秒。

**默认值:** 10000 (10s)

**例子:** `export OTEL_EXPORTER_OTLP_TRACES_TIMEOUT=500`

### `OTEL_EXPORTER_OTLP_METRICS_TIMEOUT`

所有出向指标的超时值，单位是毫秒。

**默认值:** 10000 (10s)

**例子:** `export OTEL_EXPORTER_OTLP_METRICS_TIMEOUT=500`

### `OTEL_EXPORTER_OTLP_LOGS_TIMEOUT`

所有出向日志的超时值，单位是毫秒。

**默认值:** 10000 (10s)

**例子:** `export OTEL_EXPORTER_OTLP_LOGS_TIMEOUT=500`

### `OTEL_EXPORTER_OTLP_PROTOCOL`

指定所有遥测数据要使用的 OTLP 传输协议。

**默认值:** SDK-dependent, but will typically be either `http/protobuf` or `grpc`.

**例子:** `export OTEL_EXPORTER_OTLP_PROTOCOL=grpc`

有效值如下:

- `grpc` 使用 OTLP/gRPC
- `http/protobuf` 使用 OTLP/HTTP + protobuf
- `http/json` 使用 OTLP/HTTP + json

### `OTEL_EXPORTER_OTLP_TRACES_PROTOCOL`

指定所有追踪数据要使用的 OTLP 传输协议。

**默认值:** SDK-dependent, but will typically be either `http/protobuf` or `grpc`.

**例子:** `export OTEL_EXPORTER_OTLP_TRACES_PROTOCOL=grpc`

有效值如下:

- `grpc` 使用 OTLP/gRPC
- `http/protobuf` 使用 OTLP/HTTP + protobuf
- `http/json` 使用 OTLP/HTTP + json

### `OTEL_EXPORTER_OTLP_METRICS_PROTOCOL`

指定所有指标数据要使用的 OTLP 传输协议。

**Default value:** SDK-dependent, but will typically be either `http/protobuf` or `grpc`.

**例子:** `export OTEL_EXPORTER_OTLP_METRICS_PROTOCOL=grpc`

有效值如下:

- `grpc` 使用 OTLP/gRPC
- `http/protobuf` 使用 OTLP/HTTP + protobuf
- `http/json` 使用 OTLP/HTTP + json