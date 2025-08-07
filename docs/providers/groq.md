---
sidebar_label: Groq
description: 在 Roo Code 中配置 Groq 的高速 LPU 推理。访问 Llama、Mixtral 和其他模型，响应速度显著更快。
keywords:
  - groq
  - groq cloud
  - roo code
  - api provider
  - lpu
  - fast inference
  - llama models
  - mixtral
  - high speed ai
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Groq

Groq 专注于为大型语言模型提供超高速推理，利用其定制的 Language Processing Units (LPU)。这可以显著加快支持模型的响应时间。

**网站：** [https://groq.com/](https://groq.com/)

---

## 获取 API 密钥

要将 Groq 与 Roo Code 一起使用，您需要从 [GroqCloud 控制台](https://console.groq.com/) 获取 API 密钥。注册或登录后，导航到仪表板的 API 密钥部分以创建并复制您的密钥。

---

## 支持的模型

Roo Code 将尝试从 Groq API 获取可用模型列表。通过 Groq 提供的一些常见模型包括：

*   `llama3-8b-8192`
*   `llama3-70b-8192`
*   `mixtral-8x7b-32768`
*   `gemma-7b-it`

有关支持模型及其功能的最新列表，请参阅 [Groq 文档](https://console.groq.com/docs/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Groq”。
3.  **输入 API 密钥：** 将您的 Groq API 密钥粘贴到“Groq API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的模型。
