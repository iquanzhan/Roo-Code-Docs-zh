---
sidebar_label: SambaNova
description: 在 Roo Code 中配置 SambaNova 的高速 AI 模型。体验具有竞争力的性能和多样化模型选择的企业级推理。
keywords:
  - sambanova
  - sambanova ai
  - roo code
  - api provider
  - high-speed inference
  - enterprise ai
  - llm provider
  - fast inference
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 SambaNova

SambaNova 专注于为大型语言模型提供高速推理，通过其 SambaCloud 门户利用其可重构数据流单元 (RDUs)。这为支持的模型提供了快速的响应时间。

**网站:** [https://cloud.sambanova.ai/](https://cloud.sambanova.ai/)

---

## 获取 API 密钥

要在 Roo Code 中使用 SambaNova，您需要从 [SambaCloud](https://cloud.sambanova.ai?utm_source=roocode&utm_medium=external&utm_campaign=cloud_signup) 获取 API 密钥。注册后，导航到左侧面板中的 API 密钥部分以创建并复制您的 SambaCloud API 密钥。

---

## 支持的模型

Roo Code 将尝试从 SambaNova API 获取可用模型列表。通过 SambaCloud 常见的模型包括：

*   `DeepSeek-R1`
*   `DeepSeek-V3-0324`
*   `DeepSeek-R1-Distill-Llama-70B`
*   `Meta-Llama-3.3-70B-Instruct`
*   `Meta-Llama-3.1-8B-Instruct`
*   `Llama-4-Maverick-17B-128E-Instruct`
*   `Qwen3-32B`
*   `Llama-3.3-Swallow-70B-Instruct-v0.4`

请参阅 [SambaCloud 文档](https://docs.sambanova.ai/cloud/docs/get-started/supported-models) 以获取最新的支持模型列表及其功能。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从 "API 提供商" 下拉列表中选择 "SambaNova"。
3. **输入 API 密钥：** 将您的 SambaNova API 密钥粘贴到 "SambaNova API 密钥" 字段中。
4. **选择模型：** 从 "模型" 下拉列表中选择您想要的模型。
5. **(可选) 自定义基础 URL：** 如果使用私有部署，请勾选 "使用自定义基础 URL" 并输入您的端点 URL。