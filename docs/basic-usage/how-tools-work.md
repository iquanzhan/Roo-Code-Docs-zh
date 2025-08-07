---
description: 了解 Roo Code 工具的工作原理，包括它们的分类、执行方式以及如何使用它们来增强您的开发工作流程。
keywords:
  - "Roo Code 工具"
  - "工具分类"
  - "工具执行"
  - "开发工作流程"
image: /img/social-share.jpg
---

# 工具工作原理

Roo Code 工具是扩展其功能的核心组件。它们分为五个主要类别：

1. **Read（读取）**：这些工具用于从文件或系统中检索信息，例如读取文件内容或获取系统状态。
2. **Edit（编辑）**：这些工具用于修改文件内容，例如更新、重命名或删除文件。
3. **Execute（执行）**：这些工具用于运行命令或脚本，例如构建项目或运行测试。
4. **Browser（浏览器）**：这些工具用于与网页交互，例如抓取网页内容或模拟用户操作。
5. **Workflow（工作流）**：这些工具用于自动化复杂任务，例如部署应用程序或执行多步骤操作。

## 示例

以下是一个简单的示例，展示了如何使用 Roo Code 工具：

```bash
# 使用 Read 工具读取文件内容
roo read /path/to/file.txt

# 使用 Edit 工具更新文件内容
roo edit /path/to/file.txt --content "新的文件内容"

# 使用 Execute 工具运行命令
roo execute "npm run build"

# 使用 Browser 工具抓取网页内容
roo browser https://example.com

# 使用 Workflow 工具执行多步骤操作
roo workflow deploy
```

## 核心工具参考

| 工具名称 | 类别 | 描述 | 使用示例 |
|----------|------|------|--------|
| `read` | Read | 读取文件内容 | `roo read /path/to/file.txt` |
| `edit` | Edit | 编辑文件内容 | `roo edit /path/to/file.txt --content "新内容"` |
| `execute` | Execute | 执行命令 | `roo execute "npm run build"` |
| `browser` | Browser | 与网页交互 | `roo browser https://example.com` |
| `workflow` | Workflow | 执行工作流 | `roo workflow deploy` |
