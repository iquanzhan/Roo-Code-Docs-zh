---
description: 了解如何使用 .rooignore 文件控制 Roo Code 的文件访问、保护敏感信息以及管理 AI 可以读取或修改的文件。
keywords:
  - rooignore
  - 文件访问控制
  - 敏感数据保护
  - gitignore 语法
  - 文件权限
  - 安全性
image: /img/social-share.jpg
sidebar_label: .rooignore
---

# 使用 .rooignore 控制文件访问

`.rooignore` 文件是管理 Roo Code 与项目文件交互的关键功能。它允许您指定 Roo 不应访问或修改的文件和目录，类似于 `.gitignore` 对 Git 的作用。

---

## 什么是 `.rooignore`？

*   **目的**：保护敏感信息，防止意外更改构建产物或大型资产，并通常定义 Roo 在工作区内的操作范围。
*   **如何使用**：在 VS Code 工作区的根目录中创建一个名为 `.rooignore` 的文件。在此文件中列出模式，以告诉 Roo 忽略哪些文件和目录。
*   **范围**：`.rooignore` 影响 Roo 的工具和上下文提及（如 `@directory` 附件）。

Roo 会主动监控 `.rooignore` 文件。您所做的任何更改都会自动重新加载，确保 Roo 始终使用最新的规则。`.rooignore` 文件本身始终被隐式忽略，因此 Roo 无法更改自己的访问规则。

---

## 模式语法

`.rooignore` 的语法与 `.gitignore` 相同。以下是一些常见示例：

*   `node_modules/`：忽略整个 `node_modules` 目录。
*   `*.log`：忽略所有以 `.log` 结尾的文件。
*   `config/secrets.json`：忽略特定文件。
*   `!important.log`：例外；Roo 将*不会*忽略这个特定文件，即使存在像 `*.log` 这样的广泛模式。
*   `build/`：忽略 `build` 目录。
*   `docs/**/*.md`：忽略 `docs` 目录及其子目录中的所有 Markdown 文件。

有关语法的全面指南，请参阅 [官方 Git 文档中的 .gitignore](https://git-scm.com/docs/gitignore)。

---

## Roo 工具如何与 `.rooignore` 交互

`.rooignore` 规则在各种 Roo 工具中得到执行：

### 严格强制执行（读取和写入）

这些工具在任何文件操作之前直接检查 `.rooignore`。如果文件被忽略，则操作被阻止：

*   [`read_file`](/advanced-usage/available-tools/read-file)：不会读取被忽略的文件。
*   [`write_to_file`](/advanced-usage/available-tools/write-to-file)：不会写入或创建新的被忽略的文件。
*   [`apply_diff`](/advanced-usage/available-tools/apply-diff)：不会对被忽略的文件应用差异。
*   [`insert_content`](/advanced-usage/available-tools/insert-content)：不会写入被忽略的文件。
*   [`search_and_replace`](/advanced-usage/available-tools/search-and-replace)：不会在被忽略的文件中搜索和替换。
*   [`list_code_definition_names`](/advanced-usage/available-tools/list-code-definition-names)：不会解析被忽略的文件以获取代码符号。

### 文件发现和列出

*   **[`list_files`](/advanced-usage/available-tools/list-files) 工具和 `@directory` 附件**：当 Roo 列出文件或您使用 `@directory` 附件时，被忽略的文件会被省略或标记为 🔒 符号（请参阅下面的“用户体验”）。两者使用相同的过滤逻辑。
*   **环境详细信息**：提供给 Roo 的有关工作区的信息（如打开的标签页和项目结构）经过过滤，以排除或标记被忽略的项目。

### 上下文提及

*   **`@directory` 附件**：目录内容遵循 `.rooignore` 模式。被忽略的文件会被过滤掉或根据 `showRooIgnoredFiles` 设置标记为 `[🔒]` 前缀。
*   **单个文件提及**：被忽略的文件返回 "(File is ignored by .rooignore)" 而不是内容。

### 命令执行

*   **[`execute_command`](/advanced-usage/available-tools/execute-command) 工具**：此工具检查命令（来自预定义列表，如 `cat` 或 `grep`）是否针对被忽略的文件。如果是，则执行被阻止。

---

## 主要限制和范围

*   **以工作区为中心**：`.rooignore` 规则**仅适用于当前 VS Code 工作区根目录内的文件和目录**。此范围之外的文件不受影响。
*   **[`execute_command`](/advanced-usage/available-tools/execute-command) 特定性**：对 `execute_command` 的保护仅限于预定义的文件读取命令列表。自定义脚本或不常见的实用程序可能不会被捕获。
*   **不是完整的沙箱**：`.rooignore` 是通过其工具控制 Roo 文件访问的强大工具，但它不会创建系统级沙箱。

---

## 用户体验和通知

*   **视觉提示 (🔒)**：在文件列表和 `@directory` 附件中，被 `.rooignore` 忽略的文件可能会根据 `showRooIgnoredFiles` 设置标记为锁符号 (🔒)（默认为 `true`）。
*   **忽略消息**：单个文件提及返回 "(File is ignored by .rooignore)" 而不是内容。
*   **错误消息**：如果工具操作被阻止，Roo 会收到一个错误：`"Access to [file_path] is blocked by the .rooignore file settings. You must try to continue in the task without using this file, or ask the user to update the .rooignore file."`
*   **聊天通知**：当操作因 `.rooignore` 而被阻止时，您通常会在 Roo 聊天界面中看到通知。

本指南帮助您了解 `.rooignore` 功能、其功能和当前限制，以便您可以有效地管理 Roo 与代码库的交互。
