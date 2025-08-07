---
description: 在 Roo Code 中配置 OpenRouter，通过单一 API 访问来自各种提供商的 100 多种语言模型，并支持自动模型发现。
keywords:
  - roo code
  - openrouter
  - ai provider
  - language models
  - api configuration
  - model selection
  - prompt caching
  - byok
sidebar_label: OpenRouter
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 OpenRouter

OpenRouter 是一个 AI 平台，可通过单一 API 提供对来自不同提供商的各种语言模型的访问。这可以简化设置并让您轻松尝试不同的模型。

**网站:** [https://openrouter.ai/](https://openrouter.ai/)

---

## 获取 API 密钥

1.  **注册/登录:** 前往 [OpenRouter 网站](https://openrouter.ai/)。使用您的 Google 或 GitHub 账户登录。
2.  **获取 API 密钥:** 前往 [密钥页面](https://openrouter.ai/keys)。您应该会看到一个列出的 API 密钥。如果没有，请创建一个新密钥。
3.  **复制密钥:** 复制 API 密钥。

---

## 支持的模型

OpenRouter 支持大量且不断增长的模型。Roo Code 会自动获取可用模型列表。请参阅 [OpenRouter 模型页面](https://openrouter.ai/models) 以获取完整且最新的列表。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置:** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商:** 从 "API Provider" 下拉菜单中选择 "OpenRouter"。
3.  **输入 API 密钥:** 将您的 OpenRouter API 密钥粘贴到 "OpenRouter API Key" 字段中。
4.  **选择模型:** 从 "Model" 下拉菜单中选择您想要的模型。
5.  **(可选) 自定义基础 URL:** 如果您需要为 OpenRouter API 使用自定义基础 URL，请选中 "Use custom base URL" 并输入 URL。大多数用户应将其留空。

---

## 支持的转换

OpenRouter 提供了一个 [可选的 "middle-out" 消息转换](https://openrouter.ai/docs/features/message-transforms)，以帮助处理超出模型最大上下文大小的提示。您可以通过选中 "Compress prompts and message chains to the context size" 框来启用它。

---

## 提示和注意事项

* **模型选择:** OpenRouter 提供了广泛的模型。进行实验以找到最适合您需求的模型。
* **定价:**  OpenRouter 根据底层模型的定价进行收费。请参阅 [OpenRouter 模型页面](https://openrouter.ai/models) 了解详情。
*   **提示缓存:**
    *   OpenRouter 将缓存请求传递给支持它的底层模型。请查看 [OpenRouter 模型页面](https://openrouter.ai/models) 以了解哪些模型提供缓存。
    *   对于大多数模型，如果模型本身支持，缓存应该会自动激活（类似于 Requesty 的工作方式）。
    *   **通过 OpenRouter 使用 Gemini 模型的例外情况:** 由于通过 OpenRouter 访问时 Google 的缓存机制有时会出现响应延迟，因此需要手动激活步骤 *专门针对 Gemini 模型*。
    *   如果通过 OpenRouter 使用 **Gemini 模型**，您 **必须手动选中** 提供商设置中的 "Enable Prompt Caching" 框以激活该模型的缓存。此复选框作为临时解决方法。对于 OpenRouter 上的非 Gemini 模型，此复选框对于缓存不是必需的。
*   **自带密钥 (BYOK):** 如果您使用自己的底层服务密钥，OpenRouter 收取正常费用的 5%。Roo Code 会自动调整成本计算以反映这一点。
