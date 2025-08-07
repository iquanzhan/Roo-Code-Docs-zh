---
description: 了解 Roo Code 中的建议回复如何通过预设选项帮助您快速回答后续问题，从而加快工作流程。
keywords:
  - 建议回复
  - 后续问题
  - 快速回答
  - 工作流程优化
  - ask_followup_question 工具
image: /img/social-share.jpg
sidebar_label: 建议回复
---

import Codicon from '@site/src/components/Codicon';

# 建议回复

当 Roo 需要更多信息来完成任务时，它会使用 [`ask_followup_question` 工具](/advanced-usage/available-tools/ask-followup-question)。为了使回复更容易和更快，Roo 经常在问题旁边提供建议答案。

---

## 概述

建议回复在聊天界面中 Roo 的问题下方直接显示为可点击按钮。它们提供与问题相关的预设答案，帮助您快速提供输入。

<img src="/img/suggested-responses/suggested-responses.png" alt="Roo 提出问题并在其下方显示建议回复按钮的示例" width="500" />

---

## 工作原理

1.  **问题出现**：Roo 使用 `ask_followup_question` 工具提出问题。
2.  **显示建议**：如果 Roo 提供了建议，它们会显示在问题下方的按钮中。
3.  **交互**：您可以通过两种方式与这些建议进行交互。

---

## 与建议交互

您有三种使用建议回复的选项：

1.  **直接选择**：
    *   **操作**：只需点击包含您想要提供的答案的按钮。
    *   **结果**：所选答案会立即发送回 Roo 作为您的回复。如果其中一个建议完全符合您的意图，这是最快的回复方式。

2.  **键盘快捷键**：
    *   **操作**：使用 `roo.acceptInput` 命令和您配置的键盘快捷键。
    *   **结果**：主（第一个）建议按钮会自动选择。
    *   **注意**：有关设置详细信息，请参见 [键盘快捷键](/features/keyboard-shortcuts)。

3.  **发送前编辑**：
    *   **操作**：
        *   按住 `Shift` 并点击建议按钮。
        *   *或者*，将鼠标悬停在建议按钮上并点击出现的铅笔图标 (<Codicon name="edit" />)。
    *   **结果**：建议的文本会被复制到聊天输入框中。然后您可以根据需要修改文本，然后按 Enter 发送您的自定义回复。当建议接近但需要微调时，这很有用。

<img src="/img/suggested-responses/suggested-responses-1.png" alt="聊天输入框显示从建议回复复制的文本，准备进行编辑" width="600" />

---

## 优势

*   **速度**：无需输入完整答案即可快速回复。
*   **清晰度**：建议通常会澄清 Roo 需要的信息类型。
*   **灵活性**：编辑建议以在需要时提供精确、自定义的答案。

此功能简化了 Roo 需要澄清时的交互，使您能够以最少的努力有效指导任务。