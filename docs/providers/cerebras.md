---
sidebar_label: Cerebras
description: 在 Roo Code 中配置 Cerebras AI 的超快推理模型。访问免费和付费层级，速度高达每秒 2600 个 token，适用于编码和推理任务。
keywords:
  - cerebras
  - cerebras ai
  - roo code
  - api provider
  - fast inference
  - qwen coder
  - llama models
  - free tier
  - high speed ai
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Cerebras

Cerebras AI 专注于极快的推理速度（高达每秒 2600 个 token），并具有竞争力的价格，包括免费层级。其模型针对编码、通用智能和推理任务进行了优化。

**网站：** [https://cloud.cerebras.ai/](https://cloud.cerebras.ai/)

---

## 获取 API 密钥

1. **注册/登录：** 前往 [Cerebras Cloud](https://cloud.cerebras.ai?utm_source=roocode)。创建账户或登录。
2. **导航到 API 密钥：** 在您的仪表板中访问 API 密钥部分。
3. **创建密钥：** 生成新的 API 密钥。给它一个描述性名称（例如，“Roo Code”）。
4. **复制密钥：** **重要：** 立即复制 API 密钥。安全地存储它。

---

## 支持的模型

Roo Code 支持以下 Cerebras 模型：

* `qwen-3-coder-480b-free` (默认)
* `qwen-3-coder-480b`
* `qwen-3-235b-a22b-instruct-2507`
* `llama-3.3-70b`
* `qwen-3-32b`
* `qwen-3-235b-a22b-thinking-2507`

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从“API 提供商”下拉菜单中选择“Cerebras”。
3. **输入 API 密钥：** 将您的 Cerebras API 密钥粘贴到“Cerebras API 密钥”字段中。
4. **选择模型：** 从“模型”下拉菜单中选择您想要的模型。

---

## 提示和注意事项

* **性能：** Cerebras 专注于极快的推理速度，使其成为实时编码辅助的理想选择。
* **免费层级：** `qwen-3-coder-480b-free` 模型提供对高性能推理的免费访问，但有速率限制。
* **上下文窗口：** 模型支持 64K 到 128K token 的上下文窗口。
* **定价：** 请参阅 [Cerebras Cloud](https://cloud.cerebras.ai?utm_source=roocode) 仪表板获取最新的定价信息。