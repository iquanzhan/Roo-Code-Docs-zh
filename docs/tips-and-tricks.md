---
description: 发现有效使用 Roo Code 的专家提示和技巧。学习最佳实践、生产力技巧和高级技术。
keywords:
  - Roo Code 提示
  - 生产力提示
  - 最佳实践
  - AI 编程提示
  - 高级技术
image: /img/social-share.jpg
---

# 提示与技巧

一系列快速提示，帮助您充分利用 Roo Code。

- 将 Roo Code 拖拽到[辅助侧边栏](https://code.visualstudio.com/api/ux-guidelines/sidebars#secondary-sidebar)，这样您就可以看到资源管理器、搜索、源代码管理等。
<img src="/img/right-column-roo.gif" alt="将 Roo 放在右侧列" width="900" />
- 一旦您将 Roo Code 放在与文件资源管理器分开的侧边栏中，您可以将文件从资源管理器拖拽到聊天窗口（甚至可以一次拖拽多个）。只需确保在开始拖拽文件后按住 Shift 键。
- 如果您没有使用 [MCP](/features/mcp/overview)，请在 <Codicon name="server" /> MCP 服务器选项卡中将其关闭，以显著减少系统提示的大小。
- 为了使您的[自定义模式](/features/custom-modes)保持正轨，请限制它们允许编辑的文件类型。
- 如果您遇到了令人头疼的 `input length and max tokens exceed context limit` 错误，您可以通过删除消息、回滚到之前的检查点或切换到具有长上下文窗口的模型（如 Gemini）来恢复。
- 通常，请仔细考虑用于思考模型的 `Max Tokens` 设置。您分配给它的每个令牌都会从可用于存储对话历史记录的空间中扣除。考虑仅在架构师和调试等模式下使用高 `Max Tokens` / `Max Thinking Tokens` 设置，并将代码模式保持在 16k 最大令牌或更少。
- 如果有某个您希望自定义模式执行的真实世界职位发布，请尝试要求代码模式 `根据@[url]的职位发布创建一个自定义模式`
- 如果您想真正加速，请检查您的存储库的多个副本，并并行运行 Roo Code（使用 git 解决任何冲突，就像与人类开发者一样）。
- 在使用调试模式时，请要求 Roo "在调试模式下启动一个新任务，并包含解决 X 所需的所有必要上下文"，以便调试过程使用其自己的上下文窗口，而不会污染主任务
- 通过点击下方的"编辑此页面"添加您自己的提示！
- 为了管理大文件并减少上下文/资源使用，请调整 `File read auto-truncate threshold` 设置。此设置控制从文件中一次读取的行数。较低的值可以在处理非常大的文件时提高性能，但可能需要更多的读取操作。您可以在 Roo Code 设置下的 'Advanced Settings' 中找到此设置。
- 为 [`roo.acceptInput` 命令](/features/keyboard-shortcuts) 设置键盘快捷键，以便在不使用鼠标的情况下接受建议或提交文本输入。非常适合以键盘为中心的工作流程并减少手部疲劳。
- 使用**固定模型**为不同模式分配专门的 AI 模型（用于规划的推理模型，用于编码的非推理模型）。Roo 会自动切换到每种模式上次使用的模型，而无需手动选择。
- 如果您发现对于您的领域/用例，它会忘记特定内容，请自定义[上下文缩减提示](/features/intelligent-context-condensing#customizing-the-context-condensing-prompt)。您可以指示它保留对您的工作流程至关重要的特定类型的信息。
