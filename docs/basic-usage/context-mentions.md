---
description: 了解如何在 Roo Code 中使用上下文提及 (@) 来引用文件、文件夹、问题、终端输出和 Git 提交，以获得更准确的 AI 辅助。
keywords:
  - "Roo Code 上下文提及"
  - "@ 提及"
  - "文件引用"
  - "文件夹提及"
  - "问题面板"
  - "终端提及"
  - "Git 集成"
image: /img/social-share.jpg
---

# 上下文提及

上下文提及是向 Roo Code 提供项目特定信息的强大方式，使其能够更准确高效地执行任务。您可以使用提及相关文件、文件夹、问题和 Git 提交。上下文提及以 `@` 符号开头。

<img src="/img/context-mentions/context-mentions.png" alt="上下文提及概述 - 显示聊天界面中的 @ 符号下拉菜单" width="600" />

*上下文提及概述，显示聊天界面中的 @ 符号下拉菜单。*

---

## 提及类型

<img src="/img/context-mentions/context-mentions-1.png" alt="文件提及示例，显示用 @ 引用的文件及其内容出现在对话中" width="600" />

*文件提及相关代码内容直接出现在对话中，便于参考和分析。*

| 提及类型 | 格式 | 描述 | 使用示例 |
|----------|------|------|--------|
| **文件** | `@/path/to/file.ts` | 在请求上下文中包含文件内容 | "解释 @/src/utils.ts 中的函数" |
| **文件夹** | `@/path/to/folder` | 包含文件夹中所有文件的内容（非递归） | "分析 @/src/components 中的代码" |
| **问题** | `@problems` | 包含 VS Code 问题面板诊断信息 | "@problems 修复我代码中的所有错误" |
| **终端** | `@terminal` | 包含最近的终端命令和输出 | "修复 @terminal 中显示的错误" |
| **Git 提交** | `@a1b2c3d` | 通过哈希引用特定提交 | "提交 @a1b2c3d 中更改了什么？" |
| **Git 更改** | `@git-changes` | 显示未提交的更改 | "为 @git-changes 建议消息" |
| **URL** | `@https://example.com` | 导入网站内容 | "总结 @https://docusaurus.io/" |

### 文件提及

<img src="/img/context-mentions/context-mentions-1.png" alt="文件提及示例，显示用 @ 引用的文件及其内容出现在对话中" width="600" />

*文件提及包含源代码和行号，便于精确引用。*

| 功能 | 详情 |
|------|------|
| **格式** | `@/path/to/file.ts` (始终从工作区根目录开始用 `/`) |
| **提供** | 完整的文件内容和行号 |
| **支持** | 文本文件、PDF 和 DOCX 文件（带文本提取） |
| **适用于** | 初始请求、反馈响应和后续消息 |
| **限制** | 非常大的文件可能会被截断；不支持二进制文件 |

### 文件夹提及

<img src="/img/context-mentions/context-mentions-2.png" alt="文件夹提及示例，显示目录内容在聊天中被引用" width="600" />

*文件夹提及相关目录中所有文件的内容。*

| 功能 | 详情 |
|------|------|
| **格式** | `@/path/to/folder` (无尾部斜杠) |
| **提供** | 目录中所有文件的完整内容 |
| **包括** | 文件夹中非二进制文本文件的内容（非递归） |
| **最佳用途** | 为目录中的多个文件提供上下文 |
| **提示** | 提及大型目录时注意上下文窗口限制 |

### 问题提及

<img src="/img/context-mentions/context-mentions-3.png" alt="问题提及示例，显示用 @problems 引用的 VS Code 问题面板" width="600" />

*问题提及相关 VS Code 问题面板的诊断信息。*

| 功能 | 详情 |
|------|------|
| **格式** | `@problems` |
| **提供** | VS Code 问题面板中的所有错误和警告 |
| **包括** | 文件路径、行号和诊断消息 |
| **分组** | 按文件组织的问题，更清晰 |
| **最佳用途** | 无需手动复制即可修复错误 |

有关 Roo Code 如何与 VSCode 诊断系统集成的详细信息，请参阅 [诊断集成](/features/diagnostics-integration)。

### 终端提及

<img src="/img/context-mentions/context-mentions-4.png" alt="终端提及示例，显示终端输出包含在 Roo 的上下文中" width="600" />

*终端提及相关最近命令输出，用于调试和分析。*

| 功能 | 详情 |
|------|------|
| **格式** | `@terminal` |
| **捕获** | 最后命令及其完整输出 |
| **保留** | 终端状态（不清除终端） |
| **限制** | 仅限可见终端缓冲区内容 |
| **最佳用途** | 调试构建错误或分析命令输出 |

### Git 提及

<img src="/img/context-mentions/context-mentions-5.png" alt="Git 提交提及示例，显示 Roo 分析的提交详情" width="600" />

*Git 提及相关提交详情和差异，用于上下文感知的版本分析。*

| 类型 | 格式 | 提供 | 限制 |
|------|------|------|------|
| **提交** | `@a1b2c3d` | 提交消息、作者、日期和完整差异 | 仅在 Git 仓库中工作 |
| **工作更改** | `@git-changes` | `git status` 输出和未提交更改的差异 | 仅在 Git 仓库中工作 |

### URL 提及

<img src="/img/context-mentions/context-mentions-6.png" alt="URL 提及示例，显示网站内容转换为聊天中的 Markdown" width="600" />

*URL 提及相关外部网页内容并转换为可读的 Markdown 格式。*

| 功能 | 详情 |
|------|------|
| **格式** | `@https://example.com` |
| **处理** | 使用无头浏览器获取内容 |
| **清理** | 移除脚本、样式和导航元素 |
| **输出** | 将内容转换为 Markdown 以提高可读性 |
| **限制** | 复杂页面可能无法完美转换 |

---

## 如何使用提及

1. 在聊天输入中键入 `@` 以触发建议下拉菜单
2. 继续键入以筛选建议或使用箭头键导航
3. 按 Enter 键或鼠标点击选择
4. 在请求中组合多个提及："修复 @problems 中 @/src/component.ts 的问题"

下拉菜单会自动建议：
- 最近打开的文件
- 可见文件夹
- 最近的 Git 提交
- 特殊关键字（`problems`, `terminal`, `git-changes`）
- **所有当前打开的文件**（无论忽略设置或目录过滤器如何）

下拉菜单会自动过滤掉常见目录如 `node_modules`、`.git`、`dist` 和 `out` 以减少干扰，即使它们的内容可以通过手动键入包含。

---

## 重要行为

### 忽略文件交互

| 行为 | 描述 |
|------|------|
| **`.rooignore` 绕过** | 文件和文件夹 `@mentions` 在获取上下文内容时绕过 `.rooignore` 检查。如果直接提及，忽略文件的内容将被包含。 |
| **`.gitignore` 绕过** | 同样，文件和文件夹 `@mentions` 在获取内容时不遵守 `.gitignore` 规则。 |
| **Git 命令尊重** | Git 相关提及（`@git-changes`, `@commit-hash`）由于依赖 Git 命令而尊重 `.gitignore`。 |

---

## 相关功能

- [诊断集成](/features/diagnostics-integration) - 了解自动错误检测和智能严重性过滤
- [代码操作](/features/code-actions) - 发现编辑器中的快速修复和 AI 辅助
- [Shell 集成](/features/shell-integration) - 了解终端提及如何与 shell 集成

