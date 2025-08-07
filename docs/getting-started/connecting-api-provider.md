---
sidebar_label: 连接 AI 提供商
description: 学习如何将 Roo Code 连接到 Anthropic Claude、OpenAI 和 OpenRouter 等 AI 提供商。API 密钥设置和配置的分步指南。
keywords:
  - Roo Code API 密钥
  - Claude API
  - OpenAI API
  - OpenRouter
  - Anthropic API
  - AI 提供商设置
  - API 配置
image: /img/social-share.jpg
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 连接您的第一个 AI 提供商

Roo Code 需要来自 AI 模型提供商的 API 密钥才能运行。我们推荐以下选项来访问强大的 **Claude 3.7 Sonnet** 模型：

- **OpenRouter（推荐）：** 通过单个 API 密钥提供对多个 AI 模型的访问。非常适合快速开始，设置简单。[查看定价](https://openrouter.ai/models?order=pricing-low-to-high)。
- **Anthropic：** 直接访问 Claude 模型。需要 API 访问批准，并且可能有[根据您的层级的速率限制](https://docs.anthropic.com/en/api/rate-limits#requirements-to-advance-tier)。详情请参阅 [Anthropic 的定价页面](https://www.anthropic.com/pricing#anthropic-api)。

---

## 获取您的 API 密钥

### 选项 1：LLM 路由器

LLM 路由器让您可以使用一个 API 密钥访问多个 AI 模型，简化成本管理和模型切换。与直接提供商相比，它们通常提供[有竞争力的定价](https://openrouter.ai/models?order=pricing-low-to-high)。

#### OpenRouter

1. 访问 [openrouter.ai](https://openrouter.ai/)
2. 使用您的 Google 或 GitHub 账户登录
3. 导航到 [API 密钥页面](https://openrouter.ai/keys) 并创建新密钥
4. 复制您的 API 密钥 - 您在设置 Roo Code 时需要用到它

<img src="/img/connecting-api-provider/connecting-api-provider-4.png" alt="OpenRouter API keys page" width="600" />

*OpenRouter 仪表板中的 "创建密钥" 按钮。为您的密钥命名并在创建后复制它。*

#### Requesty

1. 访问 [requesty.ai](https://requesty.ai/)
2. 使用您的 Google 账户或邮箱登录
3. 导航到 [API 管理页面](https://app.requesty.ai/api-keys) 并创建新密钥
4. **重要：** 立即复制您的 API 密钥，因为它不会再次显示

<img src="/img/connecting-api-provider/connecting-api-provider-7.png" alt="Requesty API management page" width="600" />

*Requesty API 管理页面，带有 "Create API Key" 按钮。请立即复制您的密钥 - 它只会显示一次。*

### 选项 2: 直接提供商

直接从其原始提供商访问特定模型，完全访问其功能和特性：

#### Anthropic

1. 访问 [console.anthropic.com](https://console.anthropic.com/)
2. 注册账户或登录
3. 导航到 [API 密钥部分](https://console.anthropic.com/settings/keys) 并创建新密钥
4. **重要提示：** 立即复制您的 API 密钥，因为它不会再显示

<img src="/img/connecting-api-provider/connecting-api-provider-5.png" alt="Anthropic 控制台 API 密钥部分" width="600" />

*Anthropic 控制台 API 密钥部分，带有 "Create key" 按钮。为您的密钥命名，设置过期时间，并立即复制。*

#### OpenAI

1. 访问 [platform.openai.com](https://platform.openai.com/)
2. 注册账户或登录
3. 导航到 [API 密钥部分](https://platform.openai.com/api-keys) 并创建新密钥
4. **重要提示：** 立即复制您的 API 密钥，因为它不会再显示

<img src="/img/connecting-api-provider/connecting-api-provider-6.png" alt="OpenAI API 密钥页面" width="600" />

*OpenAI 平台，带有 "Create new secret key" 按钮。为您的密钥命名，并在创建后立即复制。*

---

## 在 VS Code 中配置 Roo Code

获取 API 密钥后：

1. 通过点击 VS Code 活动栏中的 Roo Code 图标 (<KangarooIcon />) 打开 Roo Code 侧边栏
2. 在欢迎屏幕上，从下拉菜单中选择您的 API 提供商
3. 将您的 API 密钥粘贴到相应字段中
4. 选择您的模型：
   - 对于 **OpenRouter**：选择 `anthropic/claude-3.7-sonnet` ([模型详情](https://openrouter.ai/anthropic/claude-3.7-sonnet))
   - 对于 **Anthropic**：选择 `claude-3-7-sonnet-20250219` ([模型详情](https://www.anthropic.com/pricing#anthropic-api))

:::info 模型选择建议
我们强烈推荐 **Claude 3.7 Sonnet** 以获得最佳体验——它通常开箱即用。Roo Code 已针对该模型的功能和指令遵循行为进行了广泛优化。

选择替代模型是一项高级功能，会引入复杂性。不同模型在遵循工具指令、解析格式以及通过多步骤操作保持上下文方面存在显著差异。如果您尝试使用其他模型，请选择专门设计用于结构化推理和工具使用的模型。
:::

5. 点击 "Let's go!" 保存设置并开始使用 Roo Code
