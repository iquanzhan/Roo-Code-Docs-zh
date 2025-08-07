---
sidebar_label: Hugging Face
description: 将 Roo Code 连接到 Hugging Face 的推理路由器以访问开源 LLM。从多个推理提供商和模型（如 Llama、Mistral 等）中进行选择。
keywords:
  - hugging face
  - huggingface
  - roo code
  - api provider
  - open source models
  - llama
  - mistral
  - inference router
  - ai models
  - inference providers
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Hugging Face

Roo Code 与 Hugging Face 路由器集成，以提供对为代码辅助优化的精选开源模型集合的访问。该集成允许您从多个推理提供商中进行选择，并自动选择最佳可用选项。

**网站：** [https://huggingface.co/](https://huggingface.co/)

---

## 获取 API 密钥

1. **注册/登录：** 前往 [Hugging Face](https://huggingface.co/) 并创建账户或登录。
2. **导航到设置：** 点击您的个人资料图片并选择“Settings”。
3. **访问令牌：** 在您的设置中转到“Access Tokens”部分。
4. **创建令牌：** 点击“New token”并为其指定一个描述性名称（例如，“Roo Code”）。
5. **设置权限：** 选择“Read”权限（这对 Roo Code 来说已足够）。
6. **复制令牌：** **重要：** 立即复制令牌。安全地存储它。

---

## 支持的模型

Roo Code 显示 Hugging Face 上 'roocode' 集合中的模型，其中包括为代码辅助优化的精选开源模型。如果未选择模型，则默认模型为 `meta-llama/Llama-3.3-70B-Instruct`。

可用模型是从 Hugging Face API 动态检索的。模型的确切列表可能因可用性而异。模型和提供商下拉列表都是可搜索的，允许您快速找到特定选项。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从“API 提供商”下拉菜单中选择“Hugging Face”。
3. **输入 API 密钥：** 将您的 Hugging Face API 令牌粘贴到“Hugging Face API Key”字段中。
4. **选择模型：** 从“模型”下拉菜单中选择您想要的模型。下拉列表显示模型数量并且是可搜索的。
5. **选择推理提供商（可选）：** 从下拉列表中选择特定的推理提供商，或将其保留为“Auto”（默认）以自动选择最佳可用提供商。

---

## 推理提供商选择

Hugging Face 的路由器连接到多个推理提供商。您可以：

- **自动模式（默认）：** 根据模型可用性和性能自动选择最佳可用提供商
- **手动选择：** 从下拉列表中选择特定提供商

下拉列表显示每个提供商的状态：
- `live` - 提供商正在运行且可用
- `staging` - 提供商处于测试阶段
- `error` - 提供商当前遇到问题

提供商名称在 UI 中进行了格式化以提高可读性（例如，“sambanova”显示为“SambaNova”）。

当您选择特定提供商时，模型功能（最大令牌数、定价）将更新以反映该提供商的特定配置。定价信息仅在选择特定提供商时显示，而在自动模式下不显示。

---

## 模型信息显示

对于每个选定的模型，Roo Code 显示：

- **最大输出：** 模型可以生成的最大令牌数（因提供商而异）
- **定价：** 每百万输入和输出令牌的成本（仅在选择特定提供商时显示）
- **图像支持：** 目前，所有模型都显示为纯文本。这是 Roo Code 实现的限制，而不是 Hugging Face API 的限制。

---

## 可用提供商

可用提供商列表是动态的，从 Hugging Face API 检索。常见提供商包括：

- **Together AI** - 高性能推理平台
- **Fireworks AI** - 快速且可扩展的模型服务
- **DeepInfra** - 具有成本效益的 GPU 基础设施
- **Hyperbolic** - 优化的推理服务
- **Cerebras** - 硬件加速推理

*注意：上面显示的提供商是常见可用选项的示例。实际列表可能会有所不同。*

---

## 提示和注意事项

- **提供商故障转移：** 使用自动模式时，如果所选提供商失败，Hugging Face 的基础设施将自动尝试替代提供商
- **速率限制：** 不同的提供商可能有不同的速率限制和可用性
- **定价可变性：** 同一模型在不同提供商之间的成本可能差异很大
- **模型更新：** roocode 集合会定期更新新的和改进的模型