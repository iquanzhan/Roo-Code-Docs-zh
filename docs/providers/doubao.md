---
sidebar_label: Doubao
description: 在 Roo Code 中配置字节跳动的 Doubao AI 模型。访问具有完全集成和国际化支持的有竞争力的语言模型。
keywords:
  - doubao
  - bytedance
  - bytedance ai
  - roo code
  - api provider
  - doubao models
  - chinese ai
  - language models
image: /img/social-share.jpg
---

# 在 Roo Code 中使用 Doubao

Doubao 是字节跳动的中文 AI 服务，为各种开发任务提供有竞争力的语言模型。该提供商包括与嵌入支持和国际化提示的完整 API 集成。

**网站：** [https://www.volcengine.com/](https://www.volcengine.com/)

---

## 获取 API 密钥

1. **注册/登录：** 访问 [火山引擎控制台](https://console.volcengine.com/)。创建账户或登录。
2. **导航到模型服务：** 在控制台中访问 AI 模型服务部分。
3. **创建 API 密钥：** 为 Doubao 服务生成新的 API 密钥。
4. **复制密钥：** **重要：** 立即复制 API 密钥并安全存储。您可能无法再次查看它。

---

## 支持的模型

Roo Code 支持以下 Doubao 模型：

* `doubao-seed-1-6-250615` (默认) - 通用
* `doubao-seed-1-6-thinking-250715` - 增强推理
* `doubao-seed-1-6-flash-250715` - 速度优化

所有模型都支持：
- 128,000 token 上下文窗口
- 32,768 最大输出 token
- 图像输入
- 提示缓存，缓存读取享受 80% 折扣

---

## 在 Roo Code 中配置

1. **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2. **选择提供商：** 从“API 提供商”下拉菜单中选择“Doubao”。
3. **输入 API 密钥：** 将您的 Doubao API 密钥粘贴到“Doubao API 密钥”字段中。
4. **选择模型：** 从“模型”下拉菜单中选择您想要的模型。

**注意：** Doubao 使用基础 URL `https://ark.cn-beijing.volces.com/api/v3`，服务器位于中国北京。