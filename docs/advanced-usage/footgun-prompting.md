---
sidebar_label: '危险提示'
description: 高级指南，介绍如何在 Roo Code 中覆盖系统提示。了解如何谨慎使用系统提示覆盖来自定义 AI 行为。
keywords:
  - 危险提示
  - 系统提示覆盖
  - 高级自定义
  - Roo Code 配置
  - 自定义提示
image: /img/social-share.jpg
---

# 危险提示：覆盖系统提示

危险提示（系统提示覆盖）允许您替换特定 Roo Code 模式的默认系统提示。这提供了精细的控制，但绕过了内置的安全措施。请谨慎使用。

<img src="/img/footgun-prompting/footgun-prompting-1.png" alt="活动系统提示覆盖的警告指示器" width="600" />
**警告指示器：** 当当前模式的系统提示覆盖处于活动状态时，Roo Code 将在聊天输入区域显示一个警告图标，以提醒您默认行为已被修改。


:::info **危险** _(名词)_

1.  _(编程俚语，幽默，贬义)_ 任何可能导致程序员自伤的功能。

> 系统提示覆盖被认为是危险的，因为如果不深入了解就修改核心指令，可能导致意外或损坏的行为，特别是在工具使用和响应一致性方面。

:::

---

## 工作原理

1.  **覆盖文件：** 在您的工作区根目录中创建一个名为 `.roo/system-prompt-{mode-slug}` 的文件（例如，`.roo/system-prompt-code` 用于代码模式）。
2.  **内容：** 该文件的内容成为该特定模式的新系统提示。
3.  **激活：** Roo Code 会自动检测到该文件。当文件存在时，它会替换大部分标准系统提示部分。
4.  **保留部分：** 只有核心 `roleDefinition` 和您为该模式设置的任何 `customInstructions` 会与您的覆盖内容一起保留。标准部分如工具描述、规则和功能会被绕过。
5.  **构建：** 发送给模型的最终提示如下所示：

    ```
    ${roleDefinition}

    ${content_of_your_override_file}

    ${customInstructions}
    ```

---

## 访问功能

在 Roo Code UI 中找到该选项和说明：

1.  点击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标。
2.  展开 **"高级：覆盖系统提示"** 部分。
3.  点击说明中的文件路径链接将在 VS Code 中为当前选择的模式打开或创建正确的覆盖文件。

<img src="/img/footgun-prompting/footgun-prompting.png" alt="显示高级：覆盖系统提示部分的 UI" width="500" />

---

## 使用上下文变量

在创建自定义系统提示文件时，您可以使用 Roo Code 将自动替换为当前环境相关信息的特殊变量（占位符）。这使您能够使提示更具动态性和上下文感知能力。

以下是可用的变量：

- `{{mode}}`：当前使用的 Roo Code 模式的 slug（短名称）（例如，`code`，`chat-mode`）。
- `{{language}}`：VS Code 中配置的显示语言（例如，`en`，`es`）。
- `{{shell}}`：VS Code 中配置的默认终端 shell（例如，`/bin/bash`，`powershell.exe`）。
- `{{operatingSystem}}`：您的计算机运行的操作系统类型（例如，`Linux`，`Darwin` 代表 macOS，`Windows_NT`）。
- `{{workspace}}`：当前项目工作区根目录的文件路径。

**使用示例：**

您可以直接在提示文件内容中包含这些变量，如下所示：

```
您正在 '{{mode}}' 模式下协助用户。
他们的操作系统是 {{operatingSystem}}，默认 shell 是 {{shell}}。
项目位于：{{workspace}}。
请用 {{language}} 回复。
```

Roo Code 在将提示发送到模型之前替换这些占位符。

---

## 关键注意事项和警告

- **目标受众：** 最适合对 Roo Code 的提示系统和修改核心指令的影响有深入了解的用户。
- **对功能的影响：** 自定义提示会覆盖标准指令，包括工具使用和响应一致性指令。如果管理不当，这可能导致意外行为或错误。
- **模式特定：** 每个覆盖文件仅适用于其文件名中指定的模式 (`{mode-slug}`)。
- **无文件，无覆盖：** 如果 `.roo/system-prompt-{mode-slug}` 文件不存在，Roo Code 将为该模式使用标准系统提示生成过程。
- **空文件被忽略：** 如果覆盖文件存在但为空（空白），它将被忽略，并使用默认系统提示。
- **目录创建：** Roo Code 确保 `.roo` 目录在尝试读取或创建覆盖文件之前存在。
请谨慎使用此功能。不正确的实现可能会显著降低 Roo Code 在受影响模式下的性能和可靠性。