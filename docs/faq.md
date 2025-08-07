---
description: 查找关于 Roo Code 的常见问题的答案，包括设置、使用、故障排除和高级功能。获取有关 API 密钥、模式等的帮助。
keywords:
  - Roo Code 常见问题
  - 常见问题
  - 故障排除
  - API 设置
  - 自定义模式
  - MCP
  - 本地模型
image: /img/social-share.jpg
---

import KangarooIcon from '@site/src/components/KangarooIcon';

# 常见问题

本页面回答了一些关于 Roo Code 的常见问题。

---

## 一般问题

### 什么是 Roo Code？

Roo Code 是一个基于 AI 的自主编码代理，它存在于您的编辑器中。

### Roo Code 是如何工作的？

Roo Code 使用大型语言模型 (LLMs) 来理解您的请求并将其转换为操作。它可以：

*   读取和写入项目中的文件。
*   在您的 VS Code 终端中执行命令。
*   执行网页浏览（如果启用）。
*   通过模型上下文协议 (MCP) 使用外部工具。

您通过聊天界面与 Roo Code 交互，在其中提供指令并审查/批准其提议的操作。

### Roo Code 能做什么？

Roo Code 可以帮助您完成各种编码任务，包括：

*   从自然语言描述生成代码。
*   重构现有代码。
*   修复错误。
*   编写文档。
*   解释代码。
*   回答有关您的代码库的问题。
*   自动化重复性任务。
*   创建新文件和项目。

### Roo Code 是免费使用的吗？

Roo Code 扩展本身是免费且开源的。但是，Roo Code 依赖外部 API 提供商（如 [Anthropic](providers/anthropic)、[OpenAI](providers/openai)、[OpenRouter](providers/openrouter)、[Requesty](providers/requesty) 等）来提供其 AI 功能。这些提供商通常根据处理的令牌数量收取 API 使用费。您需要创建一个账户并从您选择的提供商处获取 API 密钥。有关详细信息，请参见 [设置您的第一个 AI 提供商](getting-started/connecting-api-provider)。

### 使用 Roo Code 有什么风险？

Roo Code 是一个强大的工具，重要的是要负责任地使用它。以下是一些需要注意的事项：

*   **Roo Code 可能会犯错。** 在批准之前，请务必仔细审查 Roo Code 提议的更改。
*   **Roo Code 可以执行命令。** 在允许 Roo Code 运行命令时要非常谨慎，特别是如果您使用自动批准。
*   **Roo Code 可以访问互联网。** 如果您使用的提供商支持网页浏览，请注意 Roo Code 可能会访问敏感信息。

---

## 设置与安装

### 如何安装 Roo Code？

请参见 [安装指南](/getting-started/installing) 获取详细说明。

### 支持哪些 API 提供商？

Roo Code 支持广泛的 API 提供商，包括：
*   [Anthropic (Claude)](/providers/anthropic)
*   [OpenAI](/providers/openai)
*   [OpenRouter](/providers/openrouter)
*   [Google Gemini](/providers/gemini)
*   [Glama](/providers/glama)
*   [AWS Bedrock](/providers/bedrock)
*   [GCP Vertex AI](/providers/vertex)
*   [Ollama](/providers/ollama)
*   [LM Studio](/providers/lmstudio)
*   [DeepSeek](/providers/deepseek)
*   [Mistral](/providers/mistral)
*   [Unbound](/providers/unbound)
*   [Requesty](/providers/requesty)
*   [VS Code 语言模型 API](/providers/vscode-lm)

### 如何获取 API 密钥？
每个 API 提供商都有自己的获取 API 密钥的流程。请参见 [设置您的第一个 AI 提供商](/getting-started/connecting-api-provider) 获取每个提供商的相关文档链接。

### 我可以将 Roo Code 与本地模型一起使用吗？
是的，Roo Code 支持使用 [Ollama](/providers/ollama) 和 [LM Studio](/providers/lmstudio) 在本地运行模型。有关说明，请参见 [使用本地模型](/advanced-usage/local-models)。

---

## 使用

### 如何开始一个新任务？
打开 Roo Code 面板 (<KangarooIcon />) 并在聊天框中输入您的任务。请清楚具体地说明您希望 Roo Code 做什么。有关最佳实践，请参见 [输入您的请求](/basic-usage/typing-your-requests)。

### Roo Code 中的模式是什么？
[模式](/basic-usage/using-modes) 是 Roo Code 可以采用的不同角色，每个角色都有特定的关注点和能力集。内置模式包括：

*   **代码：** 用于通用编码任务。
*   **架构师：** 用于规划和技术领导。
*   **询问：** 用于回答问题和提供信息。
*   **调试：** 用于系统性问题诊断。
您还可以创建 [自定义模式](/features/custom-modes)。

### 如何在模式之间切换？

使用聊天输入区域的下拉菜单选择不同的模式，或使用 `/` 命令切换到特定模式。

### 什么是工具以及如何使用它们？
[工具](/basic-usage/how-tools-work) 是 Roo Code 与您的系统交互的方式。Roo Code 会自动选择并使用适当的工具来完成您的任务。您无需直接调用工具。系统会提示您批准或拒绝每次工具使用。

### 什么是上下文提及？
[上下文提及](/basic-usage/context-mentions) 是向 Roo Code 提供有关您的项目的特定信息的方式，例如文件、文件夹或问题。使用 "@" 符号后跟您想要提及的项目（例如，`@/src/file.ts`，`@problems`）。

### Roo Code 可以访问互联网吗？

是的，如果您使用的提供商支持网页浏览的模型。请注意允许此功能的安全影响。

### Roo Code 可以在我的终端中运行命令吗？

是的，Roo Code 可以在您的 VS Code 终端中执行命令。除非您为命令启用了自动批准，否则在执行每个命令之前都会提示您批准。在自动批准命令时要极其谨慎。如果您在终端命令方面遇到问题，请参见 [Shell 集成指南](/features/shell-integration) 进行故障排除。

### 如何向 Roo Code 提供反馈？

您可以通过批准或拒绝 Roo Code 提议的操作来提供反馈。您还可以使用反馈字段提供额外的反馈。

### 我可以自定义 Roo Code 的行为吗？

是的，您可以通过几种方式自定义 Roo Code：

*   **自定义指令：** 提供适用于所有模式的通用指令，或特定于模式的指令。
*   **自定义模式：** 创建您自己的模式，带有定制的提示和一些工具权限。
*   **`.roorules` 文件：** 在您的项目中创建 `.roorules` 文件以提供额外的指导。
*   **设置：** 调整各种设置，如自动批准、差异编辑等。

### Roo Code 有任何自动批准设置吗？
是的，Roo Code 有一些设置，启用后将自动批准操作。了解更多 [这里](/features/auto-approving-actions)。

---

## 高级功能

### 我可以离线使用 Roo 吗？
是的，如果您使用 [本地模型](/advanced-usage/local-models)。

### 什么是 MCP（模型上下文协议）？
[MCP](/features/mcp/overview) 是一种协议，允许 Roo Code 与外部服务器通信，通过自定义工具和资源扩展其功能。

### 我可以创建自己的 MCP 服务器吗？

是的，您可以创建自己的 MCP 服务器，以向 Roo Code 添加自定义功能。有关详细信息，请参见 [MCP 文档](https://github.com/modelcontextprotocol)。

### 什么是代码库索引？

[代码库索引](/features/codebase-indexing) 使用 AI 嵌入为您的项目创建语义搜索索引。这使 Roo Code 能够通过基于意义而不是仅仅基于关键字找到相关代码，从而更好地理解和导航大型代码库。

### 代码库索引的费用是多少？

代码库索引需要 OpenAI API 密钥来生成嵌入，以及 Qdrant 向量数据库进行存储。费用取决于您的项目大小和使用的嵌入模型。初始索引是最昂贵的部分；后续更新是增量的，便宜得多。

---

## 故障排除

### Roo Code 没有响应。我该怎么办？

*   确保您的 API 密钥正确且未过期。
*   检查您的互联网连接。
*   检查您选择的 API 提供商的状态。
*   暂时禁用与 markdown 相关的扩展以测试它们是否导致问题
*   在进行这些更改后重新启动 VS Code

### 如何报告错误或建议功能？

请在 Roo Code [问题页面](https://github.com/RooCodeInc/Roo-Code/issues) 和 [功能请求页面](https://github.com/RooCodeInc/Roo-Code/discussions/categories/feature-requests?discussions_q=is%3Aopen+category%3A%22Feature+Requests%22+sort%3Atop) 上报告错误或建议功能。
*   如果问题仍然存在，请在 [GitHub](https://github.com/RooCodeInc/Roo-Code/issues) 或 [Discord](https://discord.gg/roocode) 上报告问题。

### 我看到一个错误消息。这是什么意思？

错误消息应该提供一些关于问题的信息。如果您不确定如何解决，请在 [Discord](https://discord.gg/roocode) 上寻求帮助。

### Roo Code 做了我不想要的更改。如何撤销它们？

Roo Code 使用 VS Code 的内置文件编辑功能。您可以使用标准的 "撤销" 命令 (Ctrl/Cmd + Z) 来撤销更改。此外，如果启用了实验性检查点，Roo 可以撤销对文件的更改。

### Roo Code 无法写入 markdown 文件。这是什么问题？

如果 Roo Code 无法写入 `.md` 文件并出现 "无法打开差异编辑器" 或 "write_to_file 工具失败" 等错误，这通常是由干扰文件编辑的 VS Code 扩展或设置引起的：

**常见原因：**
- 具有 "保存时格式化" 功能的扩展
- 默认情况下在预览模式下打开 markdown 文件的 VS Code 设置
- Markdown 预览扩展或类似的 markdown 处理扩展

**解决方案：**
- 禁用任何在保存时自动格式化文件的扩展
- 从您的 VS Code `settings.json` 中删除这些设置：
  ```json
  "markdown.preview.openMarkdownLinks": "inPreview",
  "workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
  }
  ```
  ```
