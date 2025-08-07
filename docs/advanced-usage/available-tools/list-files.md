---
描述: 了解 list_files 工具如何帮助 Roo Code 探索项目结构、列出目录并使用递归和过滤列表功能导航代码库。
关键词:
  - list_files
  - Roo Code 工具
  - 目录列表
  - 文件探索
  - 项目结构
  - 递归列表
  - 代码库导航
  - VS Code AI
image: /img/social-share.jpg
---

# 列出文件

`list_files` 工具显示指定位置内的文件和目录。它帮助 Roo 了解您的项目结构并有效地导航您的代码库。

---

## 参数

该工具接受以下参数:

- `path` (必需): 要列出内容的目录路径，相对于当前工作目录
- `recursive` (可选): 是否递归列出文件。使用 `true` 进行递归列表，使用 `false` 或省略以仅列出顶层。

---

## 功能

此工具列出指定位置的所有文件和目录，提供项目结构的清晰概览。它可以仅显示顶层内容或递归探索子目录。

---

## 使用场景

- 当 Roo 需要了解您的项目结构时
- 当 Roo 在阅读特定文件之前探索可用文件时
- 当 Roo 映射代码库以更好地了解其组织时
- 在使用更针对性的工具（如 `read_file` 或 `search_files`）之前
- 当 Roo 需要检查项目中特定文件类型（如配置文件）时

---

## 主要特性

- 列出文件和目录，并清楚地标记目录
- 提供递归和非递归列表模式
- 在递归模式下智能忽略常见的大型目录，如 `node_modules` 和 `.git`
- 在递归模式下遵守 `.gitignore` 规则
- 当启用 `showRooIgnoredFiles` 时，用锁符号 (🔒) 标记被 `.rooignore` 忽略的文件
- 通过利用 `ripgrep` 工具优化文件列表性能。
- 对结果进行排序，以在内容之前显示目录，保持逻辑层次结构
- 以干净、有组织的格式呈现结果
- 自动创建项目结构的心理地图

---

## 限制

- 默认情况下，文件列表上限约为 200 个文件，以防止性能问题
- 底层的 `ripgrep` 文件列表过程有 10 秒超时；如果超时，可能会返回部分结果。
- 当达到文件限制时，会添加一条建议在特定子目录上使用 `list_files` 的注释
- 不适用于确认您刚刚创建的文件的存在
- 在非常大的目录结构中可能性能降低
- 出于安全原因，无法列出根目录或主目录中的文件

---

## 工作原理

调用 `list_files` 工具时，它遵循以下过程:

1. **参数验证**: 验证必需的 `path` 参数和可选的 `recursive` 参数
2. **路径解析**: 将相对路径解析为绝对路径
3. **安全检查**: 防止列出根目录或主目录等敏感位置的文件
4. **目录/文件扫描**:
   - 使用 `ripgrep` 工具高效地列出文件，并应用 10 秒超时。
   - 使用 Node.js `fs` 模块列出目录。
   - 为递归和非递归模式应用不同的过滤逻辑。
5. **结果过滤**:
   - 在递归模式下，跳过常见的大型目录，如 `node_modules`、`.git` 等。
   - 在递归模式下遵守 `.gitignore` 规则
   - 处理 `.rooignore` 模式，要么隐藏文件，要么用锁符号标记它们
6. **格式化**:
   - 用尾部斜杠 (`/`) 标记目录
   - 对结果进行排序，以在内容之前显示目录，保持逻辑层次结构
   - 当启用 `showRooIgnoredFiles` 时，用锁符号 (🔒) 标记被忽略的文件
   - 默认情况下将结果上限设为 200 个文件，并附上关于使用子目录的注释
   - 为可读性组织结果

---

## 文件列表格式

文件列表结果包括:

- 每个文件路径显示在单独的行上
- 目录用尾部斜杠 (`/`) 标记
- 当启用 `showRooIgnoredFiles` 时，被 `.rooignore` 忽略的文件用锁符号 (🔒) 标记
- 结果按逻辑排序，目录出现在其内容之前
- 当达到文件限制时，会出现一条消息，建议在特定子目录上使用 `list_files`

示例输出格式:
```
src/
src/components/
src/components/Button.tsx
src/components/Header.tsx
src/utils/
src/utils/helpers.ts
src/index.ts
...
文件列表已截断（显示 200 个文件中的 543 个）。请在特定子目录上使用 list_files 以获取更多详细信息。
```

当使用 `.rooignore` 文件且启用 `showRooIgnoredFiles` 时:
```
src/
src/components/
src/components/Button.tsx
src/components/Header.tsx
🔒 src/secrets.json
src/utils/
src/utils/helpers.ts
src/index.ts
```

---

## 使用示例

- 当开始新任务时，Roo 可能会列出项目文件以了解其结构，然后再深入特定代码。
- 当被要求查找特定类型的文件（如所有 JavaScript 文件）时，Roo 首先列出目录以知道在哪里查找。
- 当提供代码组织建议时，Roo 首先检查当前项目结构。
- 当设置新功能时，Roo 列出相关目录以了解项目约定。

---

## 使用示例

列出当前目录中的顶层文件:
```
<list_files>
<path>.</path>
</list_files>
```

递归列出源目录中的所有文件:
```
<list_files>
<path>src</path>
<recursive>true</recursive>
</list_files>
```

检查特定项目子目录:
```
<list_files>
<path>src/components</path>
<recursive>false</recursive>
</list_files>
```
