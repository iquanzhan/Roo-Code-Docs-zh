---
description: 掌握 search_and_replace 工具，用于在文件中查找和替换文本或正则表达式模式，支持行范围和交互式差异审批。
keywords:
  - search_and_replace
  - Roo Code 工具
  - 查找替换
  - 正则表达式模式
  - 文本替换
  - 代码重构
  - 差异视图
  - 行范围
  - VS Code AI
image: /img/social-share.jpg
---

# 搜索并替换

`search_and_replace` 工具用于在文件中查找和替换文本，支持文字字符串和正则表达式模式。它允许在多个位置进行有针对性的替换，可选择在特定行范围内进行。

---

## 参数

### 必需参数

- `path`：要修改的文件的相对路径（从工作区根目录开始）。
- `search`：要查找的文本字符串或正则表达式模式。
- `replace`：用于替换匹配项的文本。

### 可选参数

- `start_line`：搜索范围开始的基于 1 的行号。
- `end_line`：搜索范围结束的基于 1 的行号（包含）。
- `use_regex`：设置为 `"true"` 以将 `search` 参数视为正则表达式模式（默认为 `false`）。
- `ignore_case`：设置为 `"true"` 以执行不区分大小写的搜索（默认为 `false`）。

---

## 功能

此工具读取指定的文件，并根据提供的参数执行搜索和替换操作。它可以对整个文件进行操作，或限制在特定行范围内。在保存之前，更改会以差异视图的形式呈现给用户进行审查和批准。

---

## 使用场景

- 在文件中重命名变量、函数或类时。
- 需要一致地更新特定文本字符串或值时。
- 使用正则表达式应用模式化更改时。
- 重构代码需要替换特定模式时。
- 在文件的定义部分进行有针对性的更改时。

---

## 主要特性

- **灵活搜索**：支持文字文本和正则表达式模式。
- **大小写控制**：可选择在搜索时忽略大小写。
- **范围替换**：可以将替换限制在特定行范围内（`start_line`，`end_line`）。
- **全局替换**：默认情况下在整个文件（或指定范围）中执行替换。
- **交互式审批**：在差异视图中显示建议的更改，供用户审查和批准。
- **用户编辑支持**：允许直接在差异视图中编辑建议的内容。
- **上下文跟踪**：记录文件编辑操作。
- **错误处理**：检查缺失的参数、文件访问问题和无效的行号。

---

## 限制

- **单文件操作**：一次只能对一个文件进行操作。首先使用 `search_files` 在多个文件中查找模式。
- **审查开销**：强制性的差异视图审批增加了交互步骤。
- **正则表达式复杂性**：复杂的正则表达式模式可能需要仔细构建和测试。

---

## 工作原理

当调用 `search_and_replace` 工具时，它会遵循以下过程：

1. **参数验证**：检查必需的 `path`、`search`、`replace` 参数，并验证可选参数如行号和布尔标志。
2. **文件读取**：读取由 `path` 指定的目标文件的内容。
3. **正则表达式构建**：
   * 如果 `use_regex` 为 `false`，则对 `search` 字符串进行转义以将其视为文字文本。
   * 创建一个带有 `g`（全局）标志和可选的 `i`（忽略大小写）标志的 `RegExp` 对象。
4. **替换执行**：
   * 如果提供了 `start_line` 或 `end_line`，则将文件内容拆分为行，隔离相关部分，在该部分执行替换，并重新构建文件内容。
   * 如果未指定行范围，则在整个文件内容字符串上执行替换。
5. **差异视图交互**：
   * 在差异视图中打开文件，显示原始内容与建议内容。
   * 使用替换结果更新差异视图。
6. **用户审批**：通过 `askApproval` 呈现更改。如果被拒绝则回滚。
7. **保存更改**：如果获得批准，则保存更改（包括在差异视图中所做的任何用户编辑）。
8. **文件上下文跟踪**：使用 `cline.getFileContextTracker().trackFileContext` 跟踪编辑。
9. **结果报告**：将成功（包括用户编辑）或失败报告回 AI 模型。

---

## 使用示例

在整个文件中进行简单文本替换：

```xml
<search_and_replace>
<path>src/config.js</path>
<search>API_KEY_OLD</search>
<replace>API_KEY_NEW</replace>
</search_and_replace>
```

不区分大小写的正则表达式替换以更新函数调用：

```xml
<search_and_replace>
<path>src/app.ts</path>
<search>processData\((.*?)\)</search>
<replace>handleData($1)</replace>
<use_regex>true</use_regex>
<ignore_case>true</ignore_case>
</search_and_replace>
```

仅在第 10 到 20 行之间替换文本：

```xml
<search_and_replace>
<path>README.md</path>
<search>Draft</search>
<replace>Final</replace>
<start_line>10</start_line>
<end_line>20</end_line>
</search_and_replace>
```