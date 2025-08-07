---
sidebar_label: Ollama
description: 使用 Ollama 与 Roo Code 一起设置，以在本地运行开源语言模型，实现隐私、离线访问和经济高效的 AI 编码。
keywords:
  - Ollama
  - 本地模型
  - Roo Code
  - 开源 AI
  - CodeLlama
  - Qwen
  - 离线 AI
  - 隐私
  - 上下文窗口配置
image: /img/social-share.jpg
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 在 Roo Code 中使用 Ollama

Roo Code 支持使用 Ollama 在本地运行模型。这提供了隐私、离线访问和潜在的更低成本，但需要更多的设置和一台功能强大的计算机。

**网站:** [https://ollama.com/](https://ollama.com/)

---

## 设置 Ollama

1.  **下载并安装 Ollama:** 从 [Ollama 网站](https://ollama.com/) 为您的操作系统下载 Ollama 安装程序。按照安装说明操作。确保 Ollama 正在运行

    ```bash
    ollama serve
    ```

2.  **下载模型:** Ollama 支持许多不同的模型。您可以在 [Ollama 网站](https://ollama.com/library) 上找到可用模型的列表。一些推荐的用于编码任务的模型包括：

    *   `codellama:7b-code` (良好的起点，较小)
    *   `codellama:13b-code` (更好的质量，较大)
    *   `codellama:34b-code` (更好的质量，非常大)
    *   `qwen2.5-coder:32b`
    *   `mistralai/Mistral-7B-Instruct-v0.1` (良好的通用模型)
    *   `deepseek-coder:6.7b-base` (适用于编码任务)
    *   `llama3:8b-instruct-q5_1` (适用于通用任务)

    要下载模型，请打开您的终端并运行：

    ```bash
    ollama pull <model_name>
    ```

    例如：

    ```bash
    ollama pull qwen2.5-coder:32b
    ```

3. **配置模型：** 默认情况下，Ollama 使用 2048 个令牌的上下文窗口大小，这对于 Roo Code 请求来说太小了。您至少需要 12k 才能获得不错的结果，理想情况下是 32k。要配置模型，您实际上需要设置其参数并保存一个副本。

   加载模型（我们将使用 `qwen2.5-coder:32b` 作为示例）：
   
    ```bash
    ollama run qwen2.5-coder:32b
    ```

   更改上下文大小参数：

    ```bash
    /set parameter num_ctx 32768
    ```

    用新名称保存模型：

    ```bash
    /save your_model_name
    ```

4.  **配置 Roo Code：**
    *   打开 Roo Code 侧边栏 (<KangarooIcon /> 图标)。
    *   点击设置齿轮图标 (<Codicon name="gear" />)。
    *   选择 "ollama" 作为 API 提供商。
    *   输入上一步中的模型名称（例如，`your_model_name`）。
    *   (可选) 如果您在不同的机器上运行 Ollama，您可以配置基础 URL。默认值为 `http://localhost:11434`。
    *   (可选) 在高级设置中配置模型上下文大小，以便 Roo Code 知道如何管理其滑动窗口。

---

## 提示和注意事项

*   **资源要求:** 在本地运行大型语言模型可能会消耗大量资源。请确保您的计算机满足您选择的模型的最低要求。
*   **模型选择:** 尝试不同的模型以找到最适合您需求的模型。
*   **离线使用:** 下载模型后，您可以使用 Roo Code 离线使用该模型。
*   **令牌跟踪:** Roo Code 跟踪通过 Ollama 运行的模型的令牌使用情况，帮助您监控消耗。
*   **Ollama 文档:** 有关安装、配置和使用 Ollama 的更多信息，请参阅 [Ollama 文档](https://ollama.com/docs)。
