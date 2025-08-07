---
sidebar_label: MCP 概述
description: 了解 Roo Code 中的模型上下文协议 (MCP)。探索如何通过自定义工具、资源和服务器集成来扩展 AI 功能。
keywords:
  - MCP
  - 模型上下文协议
  - Roo Code 扩展
  - 自定义工具
  - MCP 服务器
  - AI 集成
image: /img/social-share.jpg
---

# 模型上下文协议 (MCP)

模型上下文协议 (MCP) 是一种通过连接到外部工具和服务来扩展 Roo Code 功能的标准。MCP 服务器提供额外的工具和资源，帮助 Roo 完成超出其内置功能的任务，例如访问数据库、自定义 API 和专门功能。

---

## MCP 文档

本文档分为几个部分：

* [**在 Roo Code 中使用 MCP**](/features/mcp/using-mcp-in-roo) - 关于配置、启用和管理 Roo Code 中的 MCP 服务器的综合指南。包括服务器设置、工具批准和故障排除。

* [**什么是 MCP？**](/features/mcp/what-is-mcp) - 清晰解释模型上下文协议、其客户端-服务器架构以及它如何使 AI 系统能够与外部工具交互。

* [**STDIO、可流式 HTTP 和 SSE 传输**](/features/mcp/server-transports) - 本地 (STDIO) 和远程 (可流式 HTTP 和旧版 SSE) 传输机制的详细比较，以及每种方法的部署考虑因素。

* [**MCP 与 API**](/features/mcp/mcp-vs-api) - 分析 MCP 和 REST API 之间的根本区别，解释它们如何在不同抽象层上为 AI 系统运行。

* [**推荐的 MCP 服务器**](/features/mcp/recommended-mcp-servers) - 为 Roo Code 测试和推荐的 MCP 服务器列表，包括 Context7 的设置指南。