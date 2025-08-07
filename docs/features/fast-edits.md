---
description: 了解 Roo Code 的快速编辑功能如何使用差异（diffs）来实现更快、更安全的文件修改。学习匹配精度和配置选项。
keywords:
  - 快速编辑
  - 差异编辑
  - 文件修改
  - 应用差异
  - 匹配精度
  - 编辑效率
  - 防止截断
image: /img/social-share.jpg
---

# 差异/快速编辑

:::info 默认设置
在 Roo Code 中，默认启用快速编辑（使用“通过差异启用编辑”设置）。除非遇到特定问题或想尝试不同的差异策略，否则通常不需要更改这些设置。
:::

Roo Code 提供了一个高级设置，可以改变它编辑文件的方式，使用差异（differences）而不是重写整个文件。启用此功能可带来显著的好处。

:::note 每个提供商的设置
差异编辑配置是按 [API 配置档案](/features/api-configuration-profiles) 设置的，允许您为不同的提供商和模型自定义编辑行为。
:::

---

## 通过差异启用编辑

通过点击齿轮图标 <Codicon name="gear" /> 打开 Roo Code 面板设置。`Providers` 部分将可见。选择您想要配置的特定 [API 配置档案](/features/api-configuration-profiles)。

当 **启用通过差异编辑** 被选中时：

    <img src="/img/fast-edits/fast-edits-2.png" alt="Roo Code 设置显示启用通过差异编辑" width="500" />
1.  **更快的文件编辑**：Roo 通过仅应用必要的更改来更快地修改文件。
2.  **防止截断写入**：系统会自动检测并拒绝 AI 尝试写入不完整文件内容的尝试，这在大文件或复杂指令时可能发生。这有助于防止文件损坏。

:::note 禁用快速编辑
如果您取消选中 **启用通过差异编辑**，Roo 将恢复为使用 [`write_to_file`](/advanced-usage/available-tools/write-to-file) 工具为每次编辑重写整个文件内容，而不是使用 [`apply_diff`](/advanced-usage/available-tools/apply-diff) 应用有针对性的更改。这种全写入方法通常在修改现有文件时较慢，并导致更高的令牌使用量。
:::

---

## 匹配精度

此滑块控制 AI 识别的代码段在应用更改之前必须与文件中的实际代码匹配的程度。

    <img src="/img/fast-edits/fast-edits-4.png" alt="Roo Code 设置显示启用通过差异编辑复选框和匹配精度滑块" width="500" />

*   **100%（默认）**：需要完全匹配。这是最安全的选项，最小化了错误更改的风险。
*   **较低值（80%-99%）**：允许“模糊”匹配。即使代码段与 AI 预期的有细微差异，Roo 也可以应用更改。如果文件已被轻微修改，这可能很有用，但 **增加了** 在错误位置应用更改的风险。

**请极度谨慎地使用低于 100% 的值。** 较低的精度偶尔可能是必要的，但始终要仔细审查建议的更改。

在内部，此设置调整使用 Levenshtein 距离等算法比较代码相似性的 `fuzzyMatchThreshold`。