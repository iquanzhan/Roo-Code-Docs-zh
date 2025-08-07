---
sidebar_label: LiteLLM
description: 通过 LiteLLM 的统一 OpenAI 兼容 API 在 Roo Code 中访问超过 100 个 LLM。简化多模型管理并降低成本。
keywords:
  - litellm
  - roo code
  - api 提供商
  - 统一 api
  - openai 兼容
  - 多模型
  - llm 代理
  - 本地部署
  - 成本管理
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 LiteLLM

LiteLLM 是一个多功能工具，通过提供 OpenAI 兼容的 API，为超过 100 个大型语言模型 (LLM) 提供统一接口。这使您可以运行一个本地服务器，将请求代理到各种模型提供商或提供本地模型，所有这些都可以通过一致的 API 端点访问。

**网站:** [https://litellm.ai/](https://litellm.ai/) (主项目) & [https://docs.litellm.ai/](https://docs.litellm.ai/) (文档)

---

## 主要优势

*   **统一 API:** 通过单一的、与 OpenAI 兼容的 API 访问广泛的 LLM（来自 OpenAI、Anthropic、Cohere、HuggingFace 等）。
*   **本地部署:** 在本地运行您自己的 LiteLLM 服务器，让您对模型访问有更多控制，并可能降低延迟。
*   **简化配置:** 在一个地方（您的 LiteLLM 服务器）管理凭证和模型配置，让 Roo Code 连接到它。
*   **成本管理:** LiteLLM 提供跨不同模型和提供商跟踪成本的功能。

---

## 设置您的 LiteLLM 服务器

要在 Roo Code 中使用 LiteLLM，您首先需要设置并运行一个 LiteLLM 服务器。

### 安装

1. 安装支持代理的 LiteLLM：
   ```bash
   pip install 'litellm[proxy]'
   ```

### 配置

2. 创建一个配置文件 (`config.yaml`) 来定义您的模型和提供商：
   ```yaml
   model_list:
     # 配置 Anthropic 模型
     - model_name: claude-3-7-sonnet
       litellm_params:
         model: anthropic/claude-3-7-sonnet-20250219
         api_key: os.environ/ANTHROPIC_API_KEY
     
     # 配置 OpenAI 模型
     - model_name: gpt-4o
       litellm_params:
         model: openai/gpt-4o
         api_key: os.environ/OPENAI_API_KEY
     
     # 配置 Azure OpenAI
     - model_name: azure-gpt-4
       litellm_params:
         model: azure/my-deployment-name
         api_base: https://your-resource.openai.azure.com/
         api_version: "2023-05-15"
         api_key: os.environ/AZURE_API_KEY
   ```

### 启动服务器

3. 启动 LiteLLM 代理服务器：
   ```bash
   # 使用配置文件（推荐）
   litellm --config config.yaml
   
   # 或者使用单个模型快速启动
   export ANTHROPIC_API_KEY=your-anthropic-key
   litellm --model claude-3-7-sonnet-20250219
   ```

4. 代理默认在 `http://0.0.0.0:4000` 运行（可作为 `http://localhost:4000` 访问）。
   *   您还可以为您的 LiteLLM 服务器配置 API 密钥以增加安全性。

有关高级服务器配置和功能的详细说明，请参阅 [LiteLLM 文档](https://docs.litellm.ai/docs/)。

---

## 在 Roo Code 中配置

一旦您的 LiteLLM 服务器运行起来，您有两种选择来在 Roo Code 中配置它：

### 选项 1：使用 LiteLLM 提供商（推荐）

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从 "API 提供商" 下拉菜单中选择 "LiteLLM"。
3.  **输入基础 URL：**
    *   输入您的 LiteLLM 服务器的 URL。
    *   如果留空，默认为 `http://localhost:4000`。
4.  **输入 API 密钥（可选）：**
    *   如果您已为 LiteLLM 服务器配置了 API 密钥，请在此处输入。
    *   如果您的 LiteLLM 服务器不需要 API 密钥，Roo Code 将使用默认的虚拟密钥 (`"dummy-key"`)，这应该可以正常工作。
5.  **选择模型：**
    *   Roo Code 将尝试通过查询 `${baseUrl}/v1/model/info` 端点从您的 LiteLLM 服务器获取可用模型列表。
    *   下拉菜单中显示的模型来源于此端点。
    *   使用刷新按钮更新模型列表，如果您已将新模型添加到 LiteLLM 服务器。
    *   如果未选择模型，Roo Code 默认为 `anthropic/claude-3-7-sonnet-20250219`（这是 `litellmDefaultModelId`）。确保此模型（或您想要的默认模型）已在您的 LiteLLM 服务器上配置并可用。

### 选项 2：使用 OpenAI 兼容提供商

或者，您可以使用 "OpenAI 兼容" 提供商来配置 LiteLLM：

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从 "API 提供商" 下拉菜单中选择 "OpenAI 兼容"。
3.  **输入基础 URL：** 输入您的 LiteLLM 代理 URL（例如，`http://localhost:4000`）。
4.  **输入 API 密钥：** 使用任何字符串作为 API 密钥（例如，`"sk-1234"`），因为 LiteLLM 处理实际的提供商身份验证。
5.  **选择模型：** 选择您在 `config.yaml` 文件中配置的模型名称。

<img src="/img/litellm/litellm.png" alt="Roo Code LiteLLM 提供商设置" width="600" />

---

## Roo Code 如何获取和解释模型信息

当您配置 LiteLLM 提供商时，Roo Code 会与您的 LiteLLM 服务器交互以获取有关可用模型的详细信息：

*   **模型发现：** Roo Code 向您的 LiteLLM 服务器发出 GET 请求 `${baseUrl}/v1/model/info`。如果在 Roo Code 的设置中提供了 API 密钥，它将包含在 `Authorization: Bearer ${apiKey}` 标头中。
*   **模型属性：** 对于您的 LiteLLM 服务器报告的每个模型，Roo Code 提取并解释以下内容：
    *   `model_name`: 模型的标识符。
    *   `maxTokens`: 最大输出令牌数。如果 LiteLLM 未指定，则默认为 `8192`。
    *   `contextWindow`: 最大上下文令牌数。如果 LiteLLM 未指定，则默认为 `200000`。
    *   `supportsImages`: 由 LiteLLM 提供的 `model_info.supports_vision` 确定。
    *   `supportsPromptCache`: 由 LiteLLM 提供的 `model_info.supports_prompt_caching` 确定。
    *   `inputPrice` / `outputPrice`: 由 LiteLLM 的 `model_info.input_cost_per_token` 和 `model_info.output_cost_per_token` 计算得出。
    *   `supportsComputerUse`: 如果底层模型标识符（来自 `litellm_params.model`，例如 `openrouter/anthropic/claude-3.5-sonnet`）与 Roo Code 中预定义为适合 "计算机使用" 的 Anthropic 模型之一匹配，则此标志设置为 `true`（请参阅技术细节中的 `COMPUTER_USE_MODELS`）。

如果您的 LiteLLM 服务器的 `/model/info` 端点未为给定模型明确提供这些属性中的某些，Roo Code 将使用默认值。默认值为：
*   `maxTokens`: 8192
*   `contextWindow`: 200,000
*   `supportsImages`: `true`
*   `supportsComputerUse`: `true`（对于默认模型 ID）
*   `supportsPromptCache`: `true`
*   `inputPrice`: 3.0 (µUSD 每 1k 令牌)
*   `outputPrice`: 15.0 (µUSD 每 1k 令牌)

---

## 提示和注意事项

*   **LiteLLM 服务器是关键：** 模型的主要配置、下游提供商（如 OpenAI、Anthropic）的 API 密钥以及其他高级功能都在您的 LiteLLM 服务器上管理。Roo Code 充当此服务器的客户端。
*   **配置选项：** 您可以使用专用的 "LiteLLM" 提供商（推荐）进行自动模型发现，或使用 "OpenAI 兼容" 提供商进行简单的手动配置。
*   **模型可用性：** Roo Code 的 "模型" 下拉菜单中可用的模型完全取决于您的 LiteLLM 服务器通过其 `/v1/model/info` 端点公开的内容。
*   **网络可访问性：** 确保您的 LiteLLM 服务器正在运行并且可以从运行 VS Code 和 Roo Code 的机器访问（例如，如果不是在 `localhost` 上，请检查防火墙规则）。
*   **故障排除：** 如果模型未出现或请求失败：
    *   验证您的 LiteLLM 服务器是否正在运行并正确配置。
    *   检查 LiteLLM 服务器日志中的错误。
    *   确保 Roo Code 设置中的基础 URL 与您的 LiteLLM 服务器地址匹配。
    *   确认您的 LiteLLM 服务器所需的任何 API 密钥已正确输入到 Roo Code 中。
*   **计算机使用模型：** Roo Code 中的 `supportsComputerUse` 标志主要与某些已知在工具使用和函数调用任务中表现良好的 Anthropic 模型相关。如果您通过 LiteLLM 路由其他模型，则除非底层模型 ID 与 Roo Code 识别的特定 Anthropic 模型匹配，否则可能不会自动设置此标志。

通过利用 LiteLLM，您可以显著扩展 Roo Code 可访问的模型范围，同时集中管理它们。