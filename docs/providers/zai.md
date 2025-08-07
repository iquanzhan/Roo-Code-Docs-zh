---
sidebar_label: Z AI
description: 在 Roo Code 中配置 Z AI 模型。通过区域感知路由访问面向国际和中国大陆用户的 GLM-4.5 系列模型。
keywords:
  - z ai
  - zai
  - zhipu ai
  - glm-4.5
  - roo code
  - api provider
  - china ai
  - international ai
  - openai compatible
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Z AI

Z AI（智谱 AI）提供基于 GLM-4.5 系列的先进语言模型。该提供商通过区域感知路由为国际用户和中国大陆用户提供不同的接入点。

**网站:** [https://www.z.ai/](https://www.z.ai/) (国际) | [https://open.bigmodel.cn/](https://open.bigmodel.cn/) (中国)

---

## 获取 API 密钥

### 国际用户

1. **注册/登录：** 访问 [https://www.z.ai/](https://www.z.ai/)。创建账户或登录。
2. **导航到 API 密钥：** 访问您的账户仪表板并找到 API 密钥部分。
3. **创建密钥：** 为您的应用程序生成一个新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全存储。

### 中国大陆用户

1. **注册/登录：** 访问 [https://open.bigmodel.cn/](https://open.bigmodel.cn/)。创建账户或登录。
2. **导航到 API 密钥：** 访问您的账户仪表板并找到 API 密钥部分。
3. **创建密钥：** 为您的应用程序生成一个新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全存储。

---

## 支持的模型

Z AI 根据您选择的区域提供不同的模型目录：

### 国际模型
* GLM-4.5 系列模型
* GLM-4.5-Air 系列模型

### 中国大陆模型
* GLM-4.5 系列模型
* GLM-4.5-Air 系列模型

特定模型的可用性可能因区域而异。选择区域后，相应的模型将在下拉列表中显示。

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 在 "API 提供商" 下拉菜单中选择 "Z AI"。
3. **选择区域：** 选择您的区域：
   - "International" 用于全球访问
   - "China" 用于中国大陆访问
4. **输入 API 密钥：** 将您的 Z AI API 密钥粘贴到 "Z AI API 密钥" 字段中。
5. **选择模型：** 从 "模型" 下拉菜单中选择您想要的模型。可用模型取决于您选择的区域。

---

## 提示和注意事项

* **区域选择：** 区域设置决定了 API 端点和可用模型：
  - 国际：使用 `https://api.z.ai/api/paas/v4`
  - 中国：使用 `https://open.bigmodel.cn/api/paas/v4`
* **OpenAI 兼容性：** Z AI 使用与 OpenAI 兼容的 API，提供流式响应和使用情况报告。
* **模型选择：** 模型会根据您选择的区域自动过滤，以确保兼容性。
* **需要 API 密钥：** 所有请求都需要有效的 API 密钥。请确保您已从相应的区域平台获取。
* **定价：** 请查看相应区域网站获取当前定价信息。