---
描述: 使用 Roo Code 的 insert_content 工具在现有文件的特定行号处插入新内容，而无需修改原始内容。
关键词:
  - insert_content
  - 文件插入
  - 添加内容
  - Roo Code 工具
  - 代码插入
  - 文件编辑
image: /img/social-share.jpg
---

# 插入内容

`insert_content` 工具将新行内容添加到现有文件中，而不会修改原始内容。它非常适合在特定位置插入代码块、配置条目或日志行。

---

## 参数

该工具接受以下参数:

- `path` (必需): 要插入内容的文件的相对路径 (从工作区根目录开始)。
- `line` (必需): 应在 *之前* 插入内容的基于 1 的行号。使用 `0` 将内容追加到文件末尾。
- `content` (必需): 要插入的文本内容。

---

## 功能

此工具读取目标文件，根据 `line` 参数标识指定的插入点，并在该位置插入提供的 `content`。如果 `line` 为 `0`，则将内容添加到末尾。更改将在用户批准之前以差异视图形式呈现。

---

## 使用场景

- 在文件开头添加新的导入语句时。
- 在现有代码中插入新函数或方法时。
- 在设置文件中添加配置块时。
- 追加日志条目或数据记录时。
- 添加任何多行文本块而不更改现有行时。

---

## 主要特性

- **目标插入**: 精确地在指定行号处添加内容或追加到末尾。
- **保留现有内容**: 不修改或删除原始文件行。
- **交互式批准**: 在差异视图中显示建议的插入，并需要明确的用户批准。
- **用户编辑支持**: 允许在最终批准之前直接在差异视图中编辑建议的内容。
- **处理行号**: 正确解释 `line` 参数 (基于 1 或 0 表示追加)。
- **上下文跟踪**: 记录文件编辑操作以进行上下文管理。
- **错误处理**: 检查缺少的参数、无效的行号和文件访问问题。

---

## 限制

- **仅插入**: 无法替换或删除现有内容。使用 `apply_diff` 或 `search_and_replace` 进行修改。
- **需要现有文件**: `path` 指定的目标文件必须存在。
- **审查开销**: 强制性的差异视图批准会增加交互步骤。

---

## 工作原理

调用 `insert_content` 工具时，它遵循以下过程:

1.  **参数验证**: 检查所需的 `path`、`line` 和 `content`。验证 `line` 是非负整数。
2.  **文件读取**: 读取 `path` 指定的目标文件的内容。
3.  **插入点计算**: 将基于 1 的 `line` 参数转换为内部处理的基于 0 的索引 (追加为 `-1`)。
4.  **内容插入**: 使用内部实用程序 (`insertGroups`) 将原始文件行与新 `content` 在计算出的索引处合并。
5.  **差异视图交互**:
    *   在差异视图中打开文件 (`cline.diffViewProvider.open`)。
    *   使用建议的内容更新差异视图 (`cline.diffViewProvider.update`)。
6.  **用户批准**: 通过 `askApproval` 呈现更改。如果被拒绝则回退。
7.  **保存更改**: 如果批准，则使用 `cline.diffViewProvider.saveChanges` 保存更改。
8.  **文件上下文跟踪**: 使用 `cline.getFileContextTracker().trackFileContext` 跟踪编辑。
9.  **处理用户编辑**: 如果用户在差异视图中编辑了内容，则报告最终合并的内容。
10. **结果报告**: 将成功 (包括用户编辑) 或失败报告回 AI 模型。

---

## 使用示例

在文件开头插入导入语句 (`line: 1`):

```xml
<insert_content>
<path>src/utils.ts</path>
<line>1</line>
<content>
// 在文件开头添加导入
import { sum } from './math';
import { parse } from 'date-fns';
</content>
</insert_content>
```

将内容追加到文件末尾 (`line: 0`):

```xml
<insert_content>
<path>config/routes.yaml</path>
<line>0</line>
<content>
- path: /new-feature
  component: NewFeatureComponent
  auth_required: true
</content>
</insert_content>
```

在第 50 行之前插入函数:

```xml
<insert_content>
<path>src/services/api.js</path>
<line>50</line>
<content>
async function fetchUserData(userId) {
  const response = await fetch(`/api/users/${userId}`);
  if (!response.ok) {
    throw new Error('Failed to fetch user data');
  }
  return response.json();
}
</content>
</insert_content>
```