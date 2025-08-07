---
description: 了解 use_mcp_tool 如何通过集成外部 MCP 服务器来扩展 Roo Code，提供专业工具、领域特定功能和外部服务。
keywords:
  - use_mcp_tool
  - MCP 工具
  - 模型上下文协议
  - 外部工具
  - Roo Code 集成
  - MCP 服务器
  - 领域工具
  - 工具扩展
  - VS Code AI
image: /img/social-share.jpg
---

# 使用MCP工具

`use_mcp_tool` 工具可以与连接的模型上下文协议 (MCP) 服务器提供的外部工具进行交互。它通过标准化协议，使用领域特定功能扩展 Roo 的能力。

---

## 参数

该工具接受以下参数：

- `server_name`（必需）：提供工具的 MCP 服务器名称
- `tool_name`（必需）：要执行的工具名称
- `arguments`（必需/可选）：包含工具输入参数的 JSON 对象，遵循工具的输入模式。对于不需要输入的工具，该参数可以是可选的。

---

## 功能

此工具允许 Roo 访问由外部 MCP 服务器提供的专业功能。每个 MCP 服务器可以提供具有独特功能的多个工具，从而扩展 Roo 的内置功能。系统会根据模式验证参数，管理服务器连接，并处理各种内容类型（文本、图像、资源）的响应。

---

## 使用场景

- 需要核心工具中不可用的专业功能时
- 需要领域特定操作时
- 需要与外部系统或服务集成时
- 处理需要特定处理或分析的数据时
- 通过标准化接口访问专有工具时

---

## 主要特性

- 通过 `@modelcontextprotocol/sdk` 库使用标准化的 MCP 协议
- 支持多种传输机制（StdioClientTransport、StreamableHTTPClientTransport 和 SSEClientTransport）
- 在客户端和服务器端使用 Zod 模式验证来验证参数
- 处理多种响应内容类型：文本、图像和资源引用
- 通过自动重启来管理服务器生命周期
- 提供“始终允许”机制以绕过受信任工具的批准
- 与配套的 `access_mcp_resource` 工具配合使用以检索资源
- 为失败的操作维护适当的错误跟踪和处理
- 支持可配置的超时（1-3600 秒，默认值：60 秒）
- 允许文件监视器自动检测和重新加载服务器更改

---

## 限制

- 依赖于外部 MCP 服务器的可用性和连接性
- 仅限于连接服务器提供的工具
- 不同 MCP 服务器之间的工具功能各不相同
- 网络问题可能会影响可靠性和性能
- 执行前需要用户批准（除非在“始终允许”列表中）
- 无法同时执行多个 MCP 工具操作

---

## 服务器配置

MCP 服务器可以在全局或项目级别进行配置：

- **全局配置**：通过 VS Code 中的 Roo Code 扩展设置进行管理。这些设置适用于所有项目，除非被覆盖。
- **项目级别配置**：在项目根目录中的 `.roo/mcp.json` 文件中定义。
 - 这允许进行项目特定的服务器设置。
 - 如果项目级别服务器与全局服务器同名，则项目级别服务器优先。
 - 由于 `.roo/mcp.json` 可以提交到版本控制中，因此可以简化与团队共享配置。

---

## 工作原理

调用 `use_mcp_tool` 工具时，它会遵循以下流程：

1. **初始化和验证**：
   - 系统验证 MCP 中心是否可用
   - 确认指定的服务器存在且已连接
   - 验证请求的工具在服务器上是否存在
   - 根据工具的模式定义验证参数
   - 从服务器配置中提取超时设置（默认值：60 秒）

2. **执行和通信**：
   - 系统选择适当的传输机制：
     - `StdioClientTransport`：用于通过标准 I/O 与本地进程通信
     - `SSEClientTransport`：用于通过服务器发送事件与 HTTP 服务器通信
     - `StreamableHTTPClientTransport`：用于通过可流式 HTTP 事件与 HTTP 服务器通信
   - 发送包含已验证服务器名称、工具名称和参数的请求
   - 通信使用 `@modelcontextprotocol/sdk` 库进行标准化交互
   - 请求执行会进行跟踪，并带有超时处理以防止挂起操作

3. **响应处理**：
   - 响应可以包含多种内容类型：
     - 文本内容：纯文本响应
     - 图像内容：带有 MIME 类型信息的二进制图像数据
     - 资源引用：访问服务器资源的 URI（与 `access_mcp_resource` 配合使用）
   - 系统检查 `isError` 标志以确定是否需要错误处理
   - 结果会被格式化以在 Roo 界面中显示

4. **资源和错误处理**：
   - 系统使用 WeakRef 模式来防止内存泄漏
   - 连续错误计数器跟踪和管理错误
   - 文件监视器监视服务器代码更改并触发自动重启
   - 安全模型要求在执行工具前进行批准，除非在“始终允许”列表中

---

## 安全和权限

MCP 架构提供了多种安全功能：

- 用户必须在执行前批准工具使用（默认情况下）
- 可以在“始终允许”列表中标记特定工具以进行自动批准
- 服务器配置使用 Zod 模式进行验证以确保完整性
- 可配置的超时可防止挂起操作（1-3600 秒）
- 可以通过 UI 启用或禁用服务器连接

---

## 使用示例

- 使用服务器端处理工具分析专业数据格式
- 通过托管在外部服务器上的 AI 模型生成图像或其他媒体
- 执行复杂的领域特定计算而无需本地实现
- 通过受控接口访问专有 API 或服务
- 从专业数据库或数据源检索数据

---

## 使用示例

请求带有文本响应的天气预报数据：
```
<use_mcp_tool>
<server_name>weather-server</server_name>
<tool_name>get_forecast</tool_name>
<arguments>
{
  "city": "San Francisco",
  "days": 5,
  "format": "text"
}
</arguments>
</use_mcp_tool>
```

使用返回 JSON 的专业工具分析源代码：
```
<use_mcp_tool>
<server_name>code-analysis</server_name>
<tool_name>complexity_metrics</tool_name>
<arguments>
{
  "language": "typescript",
  "file_path": "src/app.ts",
  "include_functions": true,
  "metrics": ["cyclomatic", "cognitive"]
}
</arguments>
</use_mcp_tool>
```

生成具有特定参数的图像：
```
<use_mcp_tool>
<server_name>image-generation</server_name>
<tool_name>create_image</tool_name>
<arguments>
{
  "prompt": "A futuristic city with flying cars",
  "style": "photorealistic",
  "dimensions": {
    "width": 1024,
    "height": 768
  },
  "format": "webp"
}
</arguments>
</use_mcp_tool>
```

通过返回资源引用的工具访问资源：
```
<use_mcp_tool>
<server_name>database-connector</server_name>
<tool_name>query_and_store</tool_name>
<arguments>
{
  "database": "users",
  "type": "select",
  "fields": ["name", "email", "last_login"],
  "where": {
    "status": "active"
  },
  "store_as": "active_users"
}
</arguments>
</use_mcp_tool>
```

Tool with no required arguments:
```
<use_mcp_tool>
<server_name>system-monitor</server_name>
<tool_name>get_current_status</tool_name>
<arguments>
{}
</arguments>
</use_mcp_tool>
```
