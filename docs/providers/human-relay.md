---
sidebar_label: 人工中继
description: 在 Roo Code 中使用 ChatGPT、Claude 或其他基于 Web 的 AI 模型，无需 API 密钥。在 Roo Code 和 Web 界面之间手动中继消息。
keywords:
  - human relay
  - roo code
  - no api key
  - chatgpt web
  - claude web
  - manual relay
  - web ai models
  - free ai access
image: /img/social-share.jpg
---

# 人工中继提供商

人工中继提供商允许您在没有 API 密钥的情况下，将 Roo Code 与基于 Web 的 AI 模型（如 ChatGPT 或 Claude）一起使用。它依赖于您在 Roo Code 和 AI 的 Web 界面之间手动中继消息。

---

## 工作原理

1.  **选择人工中继**：在 Roo Code 的设置中选择“Human Relay”作为您的 API 提供商。无需 API 密钥。
2.  **发起请求**：像往常一样开始与 Roo Code 的聊天或任务。
3.  **对话框提示**：在 VS Code 中会出现一个对话框。您的 AI 消息会自动复制到剪贴板。
4.  **粘贴到 Web AI**：前往您选择的 AI 的 Web 界面（例如，chat.openai.com，claude.ai），并将剪贴板中的消息粘贴到聊天输入框中。
5.  **复制 AI 响应**：AI 响应后，复制其完整的响应文本。
6.  **粘贴回 Roo Code**：返回 VS Code 中的对话框，将 AI 的响应粘贴到指定字段中，然后点击“Confirm”。
7.  **继续**：Roo Code 会像直接从 API 获得响应一样处理该响应。

---

## 使用场景

如果您满足以下条件，此提供商会很有用：

*   您想使用不提供直接 API 访问的模型。
*   您不想管理 API 密钥。
*   您需要利用某些 AI 模型的 Web UI 中独有的特定功能或上下文。

---

## 限制

*   **手动操作**：需要在 VS Code 和浏览器之间不断复制粘贴。
*   **交互较慢**：来回过程比直接 API 集成慢得多。
*   **可能出现错误**：手动复制和粘贴可能会引入错误或遗漏。

当使用特定 Web AI 的好处大于手动中继过程的不便时，请选择此提供商。