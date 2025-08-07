---
sidebar_label: 您的第一个任务
description: 学习如何开始您的第一个 Roo Code AI 助手任务。初学者了解审批工作流程和迭代过程的分步指南。
keywords:
  - Roo Code 教程
  - 第一个任务
  - 入门指南
  - AI 编程助手教程
  - 审批工作流程
image: /img/social-share.jpg
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 开始您的第一个 Roo Code 任务

现在您已经 [配置了您的 AI 提供商和模型](/getting-started/connecting-api-provider)，您已准备好开始使用 Roo Code！本指南将引导您完成第一次交互。

---

## 步骤 1：打开 Roo Code 面板

点击 VS Code 活动栏（窗口侧面的垂直栏）中的 Roo Code 图标 (<KangarooIcon />) 以打开聊天界面。如果您没有看到该图标，请验证扩展是否已安装并启用。

<img src="/img/your-first-task/your-first-task.png" alt="Roo Code 图标在 VS Code 活动栏中" width="800" />

*活动栏中的 Roo Code 图标打开聊天界面。*

---

## 步骤 2：输入您的任务

在面板底部的聊天框中输入您希望 Roo Code 执行的清晰、简洁的描述。有效的任务示例：

* "创建一个名为 `hello.txt` 的文件，内容为 'Hello, world!'。"
* "编写一个将两个数字相加的 Python 函数。"
* "为一个标题为 'Roo test' 的简单网站创建一个 HTML 文件"

无需特殊命令或语法——只需使用纯英文。

<img src="/img/your-first-task/your-first-task-6.png" alt="在 Roo Code 聊天界面中输入任务" width="500" />
*用自然语言输入您的任务 - 无需特殊语法。*

---

## 步骤 3：发送您的任务

按 Enter 键或点击输入框右侧的发送图标 (<Codicon name="send" />)。

---

## 步骤 4：审查和批准操作

Roo Code 分析您的请求并提出具体操作。这些可能包括：

* **读取文件：** 显示需要访问的文件内容
* **写入文件：** 显示带有建议更改的差异（添加的行用绿色显示，删除的行用红色显示）
* **执行命令：** 显示要在您的终端中运行的确切命令
* **使用浏览器：** 概述浏览器操作（点击、输入等）
* **提出问题：** 在需要时请求澄清以继续进行

<img src="/img/your-first-task/your-first-task-7.png" alt="审查建议的文件创建操作" width="800" />
*Roo Code 显示它想要执行的确切操作并等待您的批准。*

**每个操作都需要您的明确批准**（除非启用了自动批准）：

* **批准：** 点击“批准”按钮以执行建议的操作
* **拒绝：** 点击“拒绝”按钮并在需要时提供反馈

---

## 步骤 5：迭代

Roo Code 以迭代方式工作。在每个操作之后，它会等待您的反馈，然后才提出下一步。继续这种审查-批准的循环，直到您的任务完成。

<img src="/img/your-first-task/your-first-task-8.png" alt="显示迭代过程的已完成任务的最终结果" width="500" />
*完成任务后，Roo Code 显示最终结果并等待您的下一个指令。*

---

## 结论

您现在已经完成了您的第一个 Roo Code 任务！通过这个过程，您已经学会了：

* 如何使用自然语言与 Roo Code 交互
* 基于批准的工作流程，让您保持控制
* Roo Code 用于逐步解决问题的迭代方法

这种迭代的、基于批准的工作流程是 Roo Code 工作方式的核心——让 AI 处理编码的繁琐部分，同时您保持完全的监督。现在您已经了解了基础知识，您可以开始处理更复杂的任务，探索不同的 [模式](/basic-usage/using-modes) 以获得专业的工作流程，或尝试 [自动批准功能](/features/auto-approving-actions) 以加快重复性任务。
