---
sidebar_label: LM Studio
description: 了解如何设置和使用 LM Studio 与 Roo Code 一起运行支持 OpenAI 兼容 API 的本地语言模型。
keywords:
  - LM Studio
  - 本地模型
  - Roo Code
  - AI 集成
  - GGUF 模型
  - CodeLlama
  - Mistral
  - DeepSeek
  - 本地推理
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 LM Studio

Roo Code 支持使用 LM Studio 在本地运行模型。LM Studio 提供了一个用户友好的界面，用于下载、配置和运行本地语言模型。它还包括一个内置的本地推理服务器，该服务器模拟 OpenAI API，使其易于与 Roo Code 集成。

**网站:** [https://lmstudio.ai/](https://lmstudio.ai/)

---

## 设置 LM Studio

1.  **下载并安装 LM Studio:** 从 [LM Studio 网站](https://lmstudio.ai/) 下载 LM Studio。
2.  **下载模型:** 使用 LM Studio 界面搜索并下载模型。一些推荐的模型包括：
    *   CodeLlama 模型 (例如, `codellama:7b-code`, `codellama:13b-code`, `codellama:34b-code`)
    *   Mistral 模型 (例如, `mistralai/Mistral-7B-Instruct-v0.1`)
    *   DeepSeek Coder 模型 (例如, `deepseek-coder:6.7b-base`)
    * 任何其他受 Roo 支持的模型，或您可以设置上下文窗口的模型。

    寻找 GGUF 格式的模型。LM Studio 提供了一个搜索界面来查找和下载模型。
3.  **启动本地服务器:** 
    *   打开 LM Studio。
    *   点击 **"本地服务器"** 标签 (图标看起来像 `<->`)。
    *   选择您下载的模型。
    *   点击 **"启动服务器"**。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置:** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商:** 从 "API 提供商" 下拉菜单中选择 "LM Studio"。
3.  **输入模型 ID:** 输入您在 LM Studio 中加载的模型的 *文件名* (例如, `codellama-7b.Q4_0.gguf`)。您可以在 LM Studio 的 "本地服务器" 标签中找到它。
4.  **(可选) 基础 URL:** 默认情况下，Roo Code 将在 `http://localhost:1234` 连接到 LM Studio。如果您已将 LM Studio 配置为使用不同的地址或端口，请在此处输入完整 URL。

---

## 提示和注意事项

*   **资源要求:** 在本地运行大型语言模型可能会消耗大量资源。请确保您的计算机满足您选择的模型的最低要求。
*   **模型选择:** LM Studio 提供了广泛的模型。通过实验找到最适合您需求的模型。
*   **本地服务器:** LM Studio 本地服务器必须正在运行，Roo Code 才能连接到它。
*   **LM Studio 文档:** 有关更多信息，请参阅 [LM Studio 文档](https://lmstudio.ai/docs)。
*   **故障排除:** 如果您看到 "Please check the LM Studio developer logs to debug what went wrong" 错误，您可能需要调整 LM Studio 中的上下文长度设置。
*   **令牌跟踪:** Roo Code 跟踪通过 LM Studio 运行的模型的令牌使用情况，帮助您监控消耗。
*   **推理支持:** 对于支持它的模型，Roo Code 可以解析 LM Studio 响应中的 "think" 标签或类似的推理指示器，提供更多关于模型过程的见解。
