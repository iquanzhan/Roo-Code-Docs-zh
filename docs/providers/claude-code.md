---
sidebar_label: Claude Code
description: 通过 Roo Code 中的官方 CLI 访问 Claude AI 模型。无需 API 密钥，支持高级推理和透明的成本跟踪。
keywords:
  - claude code
  - claude cli
  - roo code
  - api provider
  - claude max
  - no api key
  - claude reasoning
  - claude thinking mode
image: /img/social-share.jpg
---

# Claude Code 提供商

Claude Code 提供商允许您通过官方 CLI（命令行界面）而非 Web API 来使用 Anthropic 的 Claude 模型。这使您能够直接从 Roo Code 访问 Claude Max 订阅。

:::info 设置说明
在使用 Claude Code 提供商之前，请确保您已完成以下步骤：

1.  **安装 Claude CLI**：从 [Anthropic 的文档](https://docs.anthropic.com/en/docs/claude-code/setup) 下载并安装官方命令行工具。
2.  **身份验证**：在终端中运行 `claude` 以启动应用程序。应用程序运行后，输入 `/login` 登录您的 Anthropic 账户。此步骤是授予 Roo Code 访问您的 Claude 订阅所必需的。
3.  **验证设置**：通过运行 `claude --version` 确认 CLI 正常工作。这确保 Roo Code 能够找到并使用该可执行文件。
4.  **在 Roo Code 中配置**：
    *   转到 Roo Code 设置并将 **"Claude Code"** 选为您的 API 提供商。
    *   如果您将 CLI 安装在自定义位置，请将 **"Claude Code 路径"** 设置为完整可执行文件路径（例如，`/usr/local/bin/claude`）。否则，您可以将其留空。
    *   从可用选项列表中选择您想要的模型。

配置完成后，Roo Code 将使用您本地的 Claude CLI 安装与 Anthropic 的模型进行交互，并利用您现有的订阅。
:::


:::warning 环境变量使用
`claude` 命令行工具与其他 Anthropic SDK 一样，可以使用 `ANTHROPIC_API_KEY` 环境变量进行身份验证。这是在非交互式环境中授权 CLI 工具的常见方法。

如果此环境变量在您的系统上已设置，`claude` 工具可能会使用它进行身份验证，而不是交互式的 `/login` 方法。当 Roo Code 执行该工具时，它将准确反映正在使用 API 密钥，因为这是 `claude` CLI 本身的底层行为。
:::

**网站：** [https://docs.anthropic.com/en/docs/claude-code/setup](https://docs.anthropic.com/en/docs/claude-code/setup)

---

## 主要功能
- **直接 CLI 访问**：使用 Anthropic 的官方 Claude CLI 工具进行模型交互。
- **高级推理**：完全支持 Claude 的思考模式和推理能力。
- **成本透明**：显示 CLI 报告的确切使用成本。
- **灵活配置**：与您现有的 Claude CLI 设置配合使用。

---

## 为什么使用此提供商

- **无需 API 密钥**：使用您现有的 Claude CLI 身份验证。
- **成本效益**：利用 CLI 订阅费率和透明的成本报告。
- **最新功能**：在 CLI 中发布新 Claude 功能时即可访问。
- **高级推理**：完全支持 Claude 的思考模式。

## 工作原理

Claude Code 提供商通过以下方式工作：

1. **运行命令**：执行带有您的提示的 `claude` CLI 命令。
2. **处理输出**：使用高级解析处理 CLI 的 JSON 输出块。
3. **处理推理**：捕获并显示 Claude 的思考过程（如果可用）。
4. **跟踪使用情况**：报告 CLI 提供的 token 使用量和成本。

该提供商与 Roo Code 的界面集成，为您提供与其他提供商相同的体验，同时在后台使用 Claude CLI。

---

## 配置

### **Claude Code 路径**
- **设置**：`claudeCodePath`
- **描述**：指向您的 Claude CLI 可执行文件的路径。
- **默认值**：`claude`（假设它在您的系统 PATH 中）。
- **何时更改**：如果您将 Claude CLI 安装在自定义位置。

**自定义路径示例：**
- macOS/Linux：`/usr/local/bin/claude` 或 `~/bin/claude`

### **最大输出 Token 数**
- **默认值**：16,384 个 token（16k）- 从前一个 8k 默认值增加
- **环境变量**：`CLAUDE_CODE_MAX_OUTPUT_TOKENS`
- **描述**：控制 Claude 在单个响应中可以生成的最大 token 数。
- **何时更改**：如果您需要更长的响应，或者出于成本/性能原因想要限制输出长度。

**配置示例：**
```bash
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=32768  # 设置为 32k token
```

---

## 支持的模型

Claude Code 提供商支持以下 Claude 模型：

- **Claude Opus 4.1**（功能最强）
- **Claude Opus 4** 
- **Claude Sonnet 4**（最新，推荐）
- **Claude 3.7 Sonnet**
- **Claude 3.5 Sonnet**
- **Claude 3.5 Haiku**（快速响应）

具体可用的模型取决于您的 Claude CLI 订阅和计划。


---

## 输出 Token 限制

Claude Code 提供商现在默认为 16,384（16k）最大输出 token，允许更长和更完整的响应。这对于以下情况特别有用：
- 生成大型代码文件
- 详细解释和文档
- 复杂的重构操作
- 多文件更改

如果您需要针对您的用例设置不同的限制，可以使用 `CLAUDE_CODE_MAX_OUTPUT_TOKENS` 环境变量自定义此限制。

---

## 常见问题

**“我需要为此提供商提供 Claude API 密钥吗？”**
- 通常不需要。您可以使用 `claude` 应用程序中的 `/login` 命令进行交互式身份验证。
- 但是，如果设置了 `ANTHROPIC_API_KEY` 环境变量，Claude CLI 可能会使用它进行身份验证。有关详细信息，请参见上面的警告。

**“如何安装 Claude CLI？”**
- 访问 [Anthropic 的 CLI 文档](https://docs.anthropic.com/en/docs/claude-code/setup) 获取安装说明
- CLI 会处理自己的身份验证和设置

**“为什么我要使用这个而不是常规的 Anthropic 提供商？”**
- 根据您的订阅，可能具有成本效益

**“如果 CLI 不在我的 PATH 中怎么办？”**
- 在 Claude Code 路径设置中设置自定义路径
- 指向您安装 CLI 的完整路径

