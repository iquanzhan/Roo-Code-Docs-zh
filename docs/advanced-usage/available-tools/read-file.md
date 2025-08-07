
---
描述: 探索 read_file 工具检查文件内容的功能，支持行范围、PDF/DOCX 提取、图像读取和实验性多文件并发读取。
关键词:
  - read_file
  - Roo Code 工具
  - 文件读取
  - 并发读取
  - 行号
  - PDF 提取
  - DOCX 支持
  - 图像支持
  - OCR 工作流
  - 代码分析
  - VS Code AI
image: /img/social-share.jpg
---

# 读取文件

`read_file` 工具检查项目中文件的内容。它允许 Roo 了解代码、配置文件、文档，现在还包括图像，以提供更好的帮助。

:::info 多文件支持
当 `maxConcurrentFileReads` 设置大于 1 时，`read_file` 工具可以同时读取多个文件。这显著提高了需要分析多个相关文件的任务的效率。

**注意:** 读取文件时 (即使是单个文件)，LLM 将看到一条鼓励多文件读取的消息: "一次读取多个文件对 LLM 来说更有效率。如果其他文件与您当前的任务相关，请同时读取它们。"
:::

---

## 参数

该工具根据您的配置接受两种格式的参数:

### 标准格式 (单个文件)

- `path` (必需): 要读取的文件的路径，相对于当前工作目录
- `start_line` (可选): 要从中读取的起始行号 (基于 1 的索引)
- `end_line` (可选): 要读取到的结束行号 (基于 1，包含)

:::note 旧格式
虽然单文件参数 (`path`, `start_line`, `end_line`) 仍受支持以实现向后兼容性，但我们建议使用较新的 `args` 格式以确保一致性和未来兼容性。
:::

### 增强格式 (多文件)

当 `maxConcurrentFileReads` 设置为大于 1 的值时 (在 设置 > 上下文 > "并发文件读取限制" 中找到)，该工具接受包含多个文件条目的 `args` 参数:

- `args` (必需): 多个文件规范的容器
  - `file` (必需): 单个文件规范
    - `path` (必需): 要读取的文件的路径
    - `line_range` (可选): 行范围规范 (例如，"1-50" 或 "100-150")。每个文件可以指定多个 `line_range` 元素。

---

## 功能

此工具读取指定文件的内容，并返回带有行号的内容，以便于参考。它可以读取整个文件或特定部分，从 PDF 和 Word 文档中提取文本，并以各种格式显示图像。

---

## 使用场景

- 当 Roo 需要了解现有代码结构时
- 当 Roo 需要分析配置文件时
- 当 Roo 需要从文本文件中提取信息时
- 当 Roo 在建议更改之前需要查看代码时
- 当需要在讨论中引用特定行号时

---

## 主要特性

- 显示带有行号的文件内容，便于参考
- 可以通过指定行范围来读取文件的特定部分
- 从 PDF 和 DOCX 文件中提取可读文本
- **图像支持**: 以多种格式 (PNG, JPG, JPEG, GIF, WebP, SVG, BMP, ICO, TIFF) 显示图像
- 当未指定行范围时，自动截断大文本文件，显示文件的开头
- 为截断的大型代码文件提供带有行范围的方法摘要
- 仅高效流式传输请求的行范围，以获得更好的性能
- 通过行号轻松讨论代码的特定部分
- **多文件支持**: 使用批量批准同时读取多个文件 (当 `maxConcurrentFileReads` > 1 时)

---

## 多文件功能

当 `maxConcurrentFileReads` 设置大于 1 时，`read_file` 工具获得增强功能:

### 配置
- **位置**: 设置 > 上下文 > "并发文件读取限制"
- **描述**: "'read_file' 工具可以并发处理的最大文件数。较高的值可能会加快读取多个小文件的速度，但会增加内存使用量。"
- **范围**: 1-100 (滑块控制)
- **默认值**: 5

### 批处理
- 在单个请求中读取最多 100 个文件 (可配置，默认 5 个)
- 并行处理以提高性能
- 用于用户同意的批量批准界面

### 增强用户体验
- 多个文件的单个批准对话框
- 单个文件覆盖选项
- 清晰可见将要访问的文件
- 优雅处理混合成功/失败场景

### 提高效率
- 减少来自多个批准对话框的中断
- 通过并行文件读取加快处理速度
- 智能批处理相关文件
- 可配置的并发限制以匹配系统功能

---

## 限制

- 在不使用行范围参数的情况下，可能无法高效处理极大型文件
- 对于二进制文件 (PDF、DOCX 和支持的图像格式除外)，可能会返回非人类可读的内容
- **多文件模式**: 需要在设置中将 `maxConcurrentFileReads` > 1
- **图像文件**: 返回 base64 编码的数据 URL，对于高分辨率图像可能很大
  - 默认单个图像最大大小: 20MB
  - 默认总图像最大大小: 20MB

---

## 工作原理

调用 `read_file` 工具时，它遵循以下过程:

1. **参数验证**: 验证必需的 `path` 参数和可选参数
2. **路径解析**: 将相对路径解析为绝对路径
3. **读取策略选择**:
   - 该工具使用严格的优先级层次结构 (如下所述)
   - 它在范围读取、自动截断或完整文件读取之间进行选择
4. **内容处理**:
   - 将行号添加到内容中 (例如，"1 | const x = 13")，其中 `1 |` 是行号。
   - 对于截断的文件，添加截断通知和方法定义
   - 对于特殊格式 (PDF, DOCX)，提取可读文本
   - 对于图像格式，返回带有 MIME 类型的 base64 编码数据 URL

---

## 读取策略优先级

该工具使用明确的决策层次结构来确定如何读取文件:

1. **第一优先级: 显式行范围**
   - 如果提供了 `start_line` 或 `end_line`，该工具总是执行范围读取
   - 该实现仅高效流式传输请求的行，使其适合处理大型文件
   - 这优先于所有其他选项

2. **第二优先级: 大型文本文件的自动截断**
   - 这仅在满足 **所有** 以下条件时应用:
     - 未指定 `start_line` 和 `end_line`。
     - 文件被识别为基于文本的文件 (不是像 PDF/DOCX 这样的二进制文件)。
     - 文件的总行数超过 `maxReadFileLine` 设置 (默认: 500 行)。
   - 当发生自动截断时:
     - 该工具仅读取 *前* `maxReadFileLine` 行。
     - 它附加一个指示截断的通知 (例如，`[仅显示 500 行，总共 1200 行...]`)。
     - 对于代码文件，它还可能附加一个摘要，总结截断部分中找到的源代码定义。
   - **特殊情况 - 仅定义模式**: 当 `maxReadFileLine` 设置为 `0` 时，该工具仅返回源代码定义而不返回文件内容。

3. **默认行为: 读取整个文件**
    - 如果未给出显式范围且不适用自动截断 (例如，文件在行限制内，或者它是受支持的二进制类型)，该工具读取整个内容。
    - 对于受支持的格式如 PDF 和 DOCX，它尝试提取完整的文本内容。
    - 对于图像格式，它返回一个可以在聊天界面中显示的 base64 编码数据 URL。

---

## 使用示例

以下是一些场景，演示了如何使用 `read_file` 工具以及您可能收到的典型输出。

### 读取整个文件

要读取文件的完整内容:

**输入:**
```xml
<read_file>
<path>src/app.js</path>
</read_file>
```

**模拟输出 (对于像 `example_small.txt` 这样的小文件):
```
1 | 这是第一行。
2 | 这是第二行。
3 | 这是第三行。
```
*(输出将根据实际文件内容而有所不同)*

### 读取特定行

要仅读取特定行范围 (例如，46-68):

**输入:**
```xml
<read_file>
<path>src/app.js</path>
<start_line>46</start_line>
<end_line>68</end_line>
</read_file>
```

**模拟输出 (对于 `example_five_lines.txt` 的第 2-3 行):**
```
2 | 第二行的内容。
3 | 第三行的内容。
```
*(输出仅显示请求的行及其原始行号)*

### 读取大型文本文件 (自动截断)

在不指定行范围的情况下读取大型文本文件时，如果内容超过内部行限制 (例如，500 行)，该工具会自动截断内容。

**输入:**
```xml
<read_file>
<path>logs/large_app.log</path>
</read_file>
```

**模拟输出 (对于一个 1500 行的日志文件，行限制为 500 行):**
```
1 | 日志条目 1...
2 | 日志条目 2...
...
500 | 日志条目 500...

[仅显示 500 行，总共 1500 行。使用 start_line 和 end_line 读取特定范围。]
// 可选: 对于代码文件，此处可能会出现源代码定义摘要
```
*(输出显示开头的行，直到 `maxReadFileLine` 限制，加上截断通知。使用行范围获取完整访问权限。)*

### 仅读取定义

当在用户设置中将 `maxReadFileLine` 设置为 `0` 时，该工具仅返回源代码定义而不返回文件内容:

**输入:**
```xml
<!-- 假设在用户设置中将 maxReadFileLine 设置为 0 -->
<read_file>
<path>src/services/auth.service.ts</path>
</read_file>
```

**模拟输出:**
```xml
<file>
  <path>src/services/auth.service.ts</path>
  <list_code_definition_names>
    class AuthService
      method validateUser
      method generateToken
  </list_code_definition_names>
  <notice>仅显示 0 行，总共 150 行。如果需要读取更多行，请使用 line_range</notice>
</file>
```
*(此模式在不读取内容的情况下快速概览文件结构。)*

### 尝试读取不存在的文件

如果指定的文件不存在:

**输入:**
```xml
<read_file>
<path>non_existent_file.txt</path>
</read_file>
```

**模拟输出 (错误):**
```
错误: 在路径 'non_existent_file.txt' 找不到文件。
```

### 尝试读取被阻止的文件

如果文件被 `.rooignore` 文件中的规则排除:

**输入:**
```xml
<read_file>
<path>.env</path>
</read_file>
```

**模拟输出 (错误):**
```xml
<file>
  <path>.env</path>
  <error>被 .rooignore 规则拒绝访问</error>
</file>
```

---

## 图像读取示例

`read_file` 工具现在支持直接在聊天界面中读取和显示图像。这使得强大的视觉分析工作流成为可能。

### 读取单个图像

**输入:**
```xml
<read_file>
<path>assets/logo.png</path>
</read_file>
```

**输出:**
```xml
<image_content>
<path>assets/logo.png</path>
<mime_type>image/png</mime_type>
<dimensions>width: 512, height: 512</dimensions>
<data_url>data:image/png;base64,iVBORw0KGgoAAAANS...</data_url>
</image_content>
```

图像将直接显示在聊天界面中，允许 Roo 分析视觉内容。

### OCR 工作流示例

从文件夹中读取多个图像以进行文本提取:

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>screenshots/page1.png</path>
  </file>
  <file>
    <path>screenshots/page2.png</path>
  </file>
  <file>
    <path>screenshots/page3.png</path>
  </file>
</args>
</read_file>
```

**用法:**
```
请从这些截图图像中提取所有文本，并将它们编译成一个单一的 markdown 文档。
```

### 设计审查工作流

分析多个设计模型:

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>designs/homepage-v1.jpg</path>
  </file>
  <file>
    <path>designs/homepage-v2.jpg</path>
  </file>
  <file>
    <path>designs/mobile-view.png</path>
  </file>
</args>
</read_file>
```

**用法:**
```
比较这些设计模型并提供反馈:
1. 视觉一致性
2. 移动端响应性
3. 可访问性问题
4. UI/UX 改进建议
```

### 支持的图像格式

该工具支持以下图像格式:
- **PNG** - 带尺寸提取
- **JPG/JPEG** - 标准和渐进式
- **GIF** - 静态和动画
- **WebP** - 现代网络格式
- **SVG** - 可缩放矢量图形
- **BMP** - 位图图像
- **ICO** - 图标文件
- **TIFF** - 标记图像格式

### 图像分析使用场景

1. **文档截图**: 从 UI 截图中提取文本并创建文档
2. **错误调试**: 分析错误截图以了解问题
3. **设计审查**: 比较模型并提供视觉反馈
4. **图表分析**: 理解架构图和流程图
5. **代码截图**: 在文本不可用时从图像中提取代码
6. **UI 测试**: 验证视觉元素和布局

---

## 多文件示例

当 `maxConcurrentFileReads` 设置为大于 1 的值时，您可以使用增强的 XML 格式同时读取多个文件。

### 读取多个完整文件

要一次读取几个完整文件:

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
  </file>
  <file>
    <path>src/utils.ts</path>
  </file>
  <file>
    <path>src/config.json</path>
  </file>
</args>
</read_file>
```

**模拟输出:**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | import { Utils } from './utils'
      3 | // ... 文件其余内容
    </content>
  </file>
  <file>
    <path>src/utils.ts</path>
    <content>
      1 | export class Utils {
      2 |   static formatDate(date: Date): string {
      3 |     // ... 实用函数
    </content>
  </file>
  <file>
    <path>src/config.json</path>
    <content>
      1 | {
      2 |   "apiUrl": "https://api.example.com",
      3 |   "timeout": 5000
      4 | }
    </content>
  </file>
</files>
```

### 从多个文件中读取特定行范围

要从多个文件中读取特定部分:

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
    <line_range>1-20</line_range>
    <line_range>45-60</line_range>
  </file>
  <file>
    <path>src/utils.ts</path>
    <line_range>10-25</line_range>
  </file>
</args>
</read_file>
```

**模拟输出:**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | import { Utils } from './utils'
      ...
      20 | const App = () => {
      
      45 |   const handleSubmit = () => {
      46 |     // 处理表单提交
      ...
      60 |   }
    </content>
  </file>
  <file>
    <path>src/utils.ts</path>
    <content>
      10 |   static formatDate(date: Date): string {
      11 |     return date.toISOString().split('T')[0]
      ...
      25 |   }
    </content>
  </file>
</files>
```

### 处理混合结果 (某些文件被拒绝/阻止)

当某些文件被批准而其他文件被拒绝或阻止时:

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
  </file>
  <file>
    <path>.env</path>
  </file>
  <file>
    <path>src/secret-config.ts</path>
  </file>
</args>
</read_file>
```

**模拟输出:**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | // ... 文件内容成功读取
    </content>
  </file>
  <file>
    <path>.env</path>
    <error>被 .rooignore 规则拒绝访问</error>
  </file>
  <file>
    <path>src/secret-config.ts</path>
    <error>用户拒绝访问文件</error>
  </file>
</files>
```

### 批量批准界面

当请求多个文件时，您将看到一个批量批准界面，允许您:

- **全部批准**: 授予对所有请求文件的访问权限
- **全部拒绝**: 拒绝对所有请求文件的访问权限
- **单独控制**: 覆盖特定文件的决定
- **文件预览**: 点击文件头在编辑器中打开它们

该界面清晰地显示每个文件路径，使您在授予权限之前轻松了解 Roo 想要访问的内容。

### 混合内容类型

您可以在单个请求中读取不同类型的文件:

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>README.md</path>
  </file>
  <file>
    <path>architecture-diagram.png</path>
  </file>
  <file>
    <path>config.json</path>
  </file>
  <file>
    <path>requirements.pdf</path>
  </file>
</args>
</read_file>
```

这允许 Roo 在一个上下文中分析文档、视觉图表、配置和规范。

