---
sidebar_label: Google Gemini
description: 通过 Roo Code 使用 Google 的 Gemini AI 模型。为您的开发工作流程配置 Gemini Flash、Pro 和实验性模型。
keywords:
  - google gemini
  - gemini ai
  - roo code
  - api provider
  - gemini flash
  - gemini pro
  - google ai
  - gemini models
  - ai studio
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Google Gemini

Roo Code 通过 Google AI Gemini API 支持 Google 的 Gemini 系列模型。

**网站：** [https://ai.google.dev/](https://ai.google.dev/)

---

## 获取 API 密钥

1.  **前往 Google AI Studio：** 导航至 [https://ai.google.dev/](https://ai.google.dev/)。
2.  **登录：** 使用您的 Google 账户登录。
3.  **创建 API 密钥：** 点击左侧菜单中的“Create API key”。
4.  **复制 API 密钥：** 复制生成的 API 密钥。

---

## 支持的模型

Roo Code 支持以下 Gemini 模型：

### 标准模型
* `gemini-2.5-flash-preview-05-20`
* `gemini-2.5-flash-preview-04-17`
* `gemini-2.5-flash-lite-preview-06-17`
* `gemini-2.5-pro-exp-03-25`
* `gemini-2.0-flash-001`
* `gemini-2.0-flash-lite-preview-02-05`
* `gemini-2.0-pro-exp-02-05`
* `gemini-2.0-flash-exp`
* `gemini-1.5-flash-002`
* `gemini-1.5-flash-exp-0827`
* `gemini-1.5-flash-8b-exp-0827`
* `gemini-1.5-pro-002`
* `gemini-1.5-pro-exp-0827`
* `gemini-exp-1206`

### 思维模型
这些模型需要在 Roo Code 设置中启用推理预算：
* `gemini-2.5-flash-preview-05-20:thinking`
* `gemini-2.5-flash-preview-04-17:thinking`
* `gemini-2.0-flash-thinking-exp-01-21`
* `gemini-2.0-flash-thinking-exp-1219`

:::info
**思维模型：** 带有 `:thinking` 后缀或名称中包含 "thinking" 的模型是混合推理模型，提供逐步推理能力。要使用这些模型，您必须在 Roo Code 设置中启用推理预算功能。
:::

有关每个模型的更多详细信息，请参阅 [Gemini 文档](https://ai.google.dev/models/gemini)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Google Gemini”。
3.  **输入 API 密钥：** 将您的 Gemini API 密钥粘贴到“Gemini API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的 Gemini 模型。

---

## 高级功能

### URL 上下文

Gemini 模型现在可以通过 URL 上下文直接访问和分析网络内容。此功能允许 Roo：

- 实时读取和理解网页
- 分析来自 URL 的文档
- 审查在线代码仓库
- 访问网站上的最新信息

#### 启用 URL 上下文

1. 打开 Roo Code 设置
2. 导航到 Gemini 提供商设置
3. 启用“URL 上下文”选项
4. 保存您的设置

#### 使用示例

```
请分析 https://example.com/api-docs 上的文档，并根据 API 规范创建一个 TypeScript 客户端库。
```

### Google 搜索接地

启用 Google 搜索接地以通过实时搜索结果增强 Gemini 的响应。这提供了：

- 来自网络搜索的最新信息
- 事实核查能力
- 当前事件意识
- 增强的技术查询准确性

#### 启用搜索接地

1. 打开 Roo Code 设置
2. 导航到 Gemini 提供商设置
3. 启用“Google 搜索接地”选项
4. 保存您的设置

#### 使用示例

```
2025 年 React Server Components 的最新最佳实践是什么？请搜索最新的信息。
```

### 组合使用

这两个功能可以一起使用以实现强大的工作流程：

```
搜索最新的 Node.js 安全漏洞，然后分析我的 package.json 文件以查看我是否受到影响。同时检查官方 Node.js 安全页面以获取建议。
```

---

## 提示和注意事项

*   **定价：** Gemini API 使用量根据输入和输出 token 定价。URL 上下文和搜索接地可能会产生额外费用。一些实验性模型可免费使用。有关详细信息，请参阅 [Gemini 定价页面](https://ai.google.dev/pricing)。
*   **模型选择：** 根据您的需求选择模型：
    - **Flash 模型：** 更快且更具成本效益，适用于大多数任务
    - **Pro 模型：** 更适合复杂推理和分析
    - **思维模型：** 最适合需要逐步推理的任务（需要推理预算）
    - **实验性模型：** 最新功能，可能免费但稳定性较差
*   **上下文窗口：** 大多数 Gemini 模型支持高达 1,048,576 个 token 的大上下文窗口，允许进行广泛的代码分析和文档处理。
*   **速率限制：** URL 上下文和搜索接地功能可能有单独的速率限制。监控您的使用情况以避免达到限制。
*   **隐私：** 使用 URL 上下文时，请注意访问私有或敏感 URL。确保您有权分析内容。
*   **搜索质量：** Google 搜索接地在特定、格式良好的查询中效果最佳。明确说明您需要什么信息。
