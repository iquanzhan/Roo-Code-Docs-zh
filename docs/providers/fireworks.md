---
sidebar_label: Fireworks AI
description: 通过 Roo Code 使用 Fireworks AI 访问 Kimi K2、Qwen3 和 DeepSeek 等最先进的开源模型，上下文窗口最大可达 256K token。
keywords:
  - fireworks ai
  - fireworks
  - kimi k2
  - qwen3
  - deepseek
  - roo code
  - api provider
  - open source models
  - ai models
  - openai compatible
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Fireworks AI

Fireworks AI 通过其优化的基础设施提供对最先进的开源语言模型的访问。该提供商提供了具有成本效益的专有 AI 服务替代方案，上下文窗口最大可达 256,000 个 token。

**网站：** [https://fireworks.ai/](https://fireworks.ai/)

---

## 获取 API 密钥

1. **注册/登录：** 前往 [Fireworks AI](https://fireworks.ai/)。创建账户或登录。
2. **导航到仪表板：** 访问您的账户仪表板。
3. **生成 API 密钥：** 从仪表板创建新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全存储。

---

## 支持的模型

Fireworks AI 提供了几种高性能模型：

### Kimi K2
* `accounts/fireworks/models/kimi-k2-instruct` (默认)
  - 总计 1 万亿参数，激活参数 32B
  - 128K 上下文窗口
  - 针对代理能力进行了优化
  - $0.60/M 输入，$2.50/M 输出

### Qwen3 系列
* `accounts/fireworks/models/qwen3-235b-a22b-instruct-2507`
  - 256K 上下文窗口
  - 与闭源模型具有竞争力
  - $0.22/M 输入，$0.88/M 输出

* `accounts/fireworks/models/qwen3-coder-480b-a35b-instruct`
  - 256K 上下文窗口
  - 专门用于编码任务
  - $0.45/M 输入，$1.80/M 输出

### DeepSeek 系列
* `accounts/fireworks/models/deepseek-r1-0528`
  - 160K 上下文窗口
  - 先进的推理能力，减少幻觉
  - 支持函数调用
  - $3.00/M 输入，$8.00/M 输出

* `accounts/fireworks/models/deepseek-v3`
  - 128K 上下文窗口
  - 总计 671B 参数，激活参数 37B
  - $0.90/M 输入，$0.90/M 输出

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从“API 提供商”下拉菜单中选择“Fireworks AI”。
3. **输入 API 密钥：** 将您的 Fireworks API 密钥粘贴到“Fireworks API 密钥”字段中。
4. **模型选择：** 默认模型 (Kimi K2) 会自动选择。如果需要，您可以从模型下拉菜单中更改它。

---

## 模型选择指南

根据您的需求选择模型：

| 模型 | 最佳用途 | 上下文 | 价格 |
|-------|----------|---------|-------|
| **Kimi K2** | 通用任务，平衡性能 | 128K | 中等 |
| **Qwen3 235B** | 具有成本效益的通用用途 | 256K | 预算友好 |
| **Qwen3 Coder** | 代码生成和调试 | 256K | 中等 |
| **DeepSeek R1** | 复杂推理，函数调用 | 160K | 高级 |
| **DeepSeek V3** | 强大的通用性能 | 128K | 平衡 |

---

## 提示和注意事项

* **成本效益：** Fireworks AI 提供了显著低于专有模型的价格，同时保持了有竞争力的性能。
* **大上下文窗口：** 大多数模型支持 128K-256K token，适用于处理大型文档和维持长时间对话。
* **OpenAI 兼容性：** 该提供商使用与 OpenAI 兼容的 API 格式，支持流式传输和使用情况跟踪。
* **纯文本：** 所有模型都是纯文本的，不支持图像或提示缓存功能。
* **默认温度：** 默认使用 0.5 的温度以平衡创造力和一致性。
* **API 密钥：** 为了安全起见，存储在您的本地机器上。
* **定价：** 有关当前费率，请参阅 [Fireworks AI 定价页面](https://fireworks.ai/pricing)。显示的价格为每百万 token 的价格。