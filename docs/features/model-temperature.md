---
description: 了解 Roo Code 中的模型温度设置如何控制 AI 输出的随机性和创造性，包括调整方法和最佳实践。
keywords:
  - 模型温度
  - AI 随机性
  - 输出控制
  - 创造性
image: /img/social-share.jpg
---

# 模型温度

模型温度设置控制 AI 输出的随机性和创造性。通过调整温度值，您可以影响 AI 生成内容的多样性和可预测性。

## 温度定义

温度是一个介于 0.0 到 2.0 之间的数值，用于控制 AI 输出的随机性：

- **低温度 (0.0-0.5)**：输出更加确定性和可预测
- **中等温度 (0.6-1.0)**：平衡创造性和一致性
- **高温度 (1.1-2.0)**：输出更加随机和创造性

## Roo Code 默认值

Roo Code 为不同模型设置了不同的默认温度值：

- **大多数模型**：0.0（最确定性输出）
- **部分推理模型**：0.6（平衡创造性和一致性）

## 调整方法

您可以通过以下两种方式调整模型温度：

1. **通过设置面板滑块**：在 Roo Code 设置面板中使用滑块调整温度值
2. **通过 API 配置文件**：在 API 配置文件中设置温度参数

## 技术实现细节

模型温度通过影响 AI 模型的概率分布来控制输出：

- **低温度**：模型更倾向于选择高概率的下一个词
- **高温度**：模型更倾向于选择低概率的下一个词

## 实验建议

建议根据具体任务调整温度值：

- **代码生成**：使用低温度以确保代码的准确性和一致性
- **创意写作**：使用中等或高温度以增加内容的多样性
- **问题解答**：使用低温度以确保答案的准确性

<img src="/img/model-temperature/model-temperature.gif" alt="Animation showing temperature slider adjustment" width="100%" />

---

## 什么是 Temperature？

Temperature（温度）是一个设置（通常在 0.0 到 2.0 之间），用于控制 AI 输出的随机性或可预测性。找到合适的平衡点是关键：较低的值会使输出更集中和一致，而较高的值则会鼓励更多的创造力和变化。对于许多编码任务，适中的温度（大约在 0.3 到 0.7 之间）通常效果很好，但最佳设置取决于你想要实现的目标。

:::info Temperature 与代码：常见误解
Temperature 控制输出的随机性，而不是直接控制代码质量和准确性。关键点包括：

*   **低 Temperature（接近 0.0）：** 产生可预测且一致的代码。适用于简单任务，但可能会重复且缺乏创造性。它不能保证 *更好的* 代码。
*   **高 Temperature：** 增加随机性，可能带来创造性的解决方案，但也可能导致更多错误或无意义的代码。它不能保证 *更高质量* 的代码。
*   **准确性：** 代码的准确性取决于模型的训练和提示的清晰度，而非 Temperature。
*   **Temperature 0.0：** 适用于一致性，但会限制解决复杂问题所需的探索。
:::

---

## Roo Code 中的默认值

Roo Code 对大多数模型使用 0.0 的默认 Temperature，以优化代码生成的最大确定性和精确性。这适用于 OpenAI 模型、Anthropic 模型（非思考变体）、LM Studio 模型以及大多数其他提供商。

某些模型使用更高的默认 Temperature - DeepSeek R1 模型和某些推理导向模型默认为 0.6，以在确定性和创造性探索之间取得平衡。

具有思考能力的模型（AI 显示其推理过程）需要固定的 Temperature 1.0，此设置无法更改，因为它确保了思考机制的最佳性能。这适用于任何启用了 ":thinking" 标志的模型。

一些专门的模型根本不支持 Temperature 调整，在这种情况下，Roo Code 会自动遵守这些限制。

---

## 何时调整 Temperature

以下是一些适用于不同任务的 Temperature 设置示例：

*   **代码模式 (0.0-0.3)：** 用于编写精确、正确的代码，结果一致且具有确定性
*   **架构模式 (0.4-0.7)：** 用于头脑风暴架构或设计解决方案，兼具创造力和结构
*   **询问模式 (0.7-1.0)：** 用于解释或需要多样化和深刻见解的开放式问题
*   **调试模式 (0.0-0.3)：** 用于以一致的精确度排除错误

这些只是起点 – 重要的是要 [尝试不同的设置](#experimentation) 以找到最适合你特定需求和偏好的配置。

---

## 如何调整 Temperature

1.  **打开 Roo Code 面板：** 点击 VS Code 活动栏中的 Roo Code 图标
2.  **打开设置：** 点击右上角的 <Codicon name="gear" /> 图标
3.  **找到 Temperature 控制：** 导航到 Providers 部分
4.  **启用自定义 Temperature：** 勾选 "Use custom temperature" 复选框
5.  **设置你的值：** 调整滑块到你喜欢的值

    <img src="/img/model-temperature/model-temperature.png" alt="Roo Code 设置面板中的 Temperature 设置" width="550" />
    *Roo Code 设置面板中的 Temperature 滑块*

---

## 使用 API 配置文件设置 Temperature

创建多个具有不同 Temperature 设置的 [API 配置文件](/features/api-configuration-profiles)：

**如何设置特定任务的 Temperature 配置文件：**

1. 创建专门的配置文件，如 "Code - Low Temp" (0.1) 和 "Ask - High Temp" (0.8)
2. 为每个配置文件配置适当的 Temperature 设置
3. 使用设置或聊天界面中的下拉菜单在配置文件之间切换
4. 为每种模式设置不同的默认配置文件，以便在切换模式时自动切换

这种方法可以在不手动调整的情况下优化模型行为以适应特定任务。

---

## 技术实现

Roo Code 在实现 Temperature 处理时考虑了以下因素：

*   用户定义的设置优先于默认值
*   尊重提供商特定的行为
*   强制执行模型特定的限制：
    *   启用思考的模型需要固定的 Temperature 1.0
    *   某些模型不支持 Temperature 调整

---

## 实验

尝试不同的 Temperature 设置是发现最适合你特定需求的最佳方法：

### 有效的 Temperature 测试

1. **从默认值开始** - 以 Roo Code 的预设值（大多数任务为 0.0）作为基线
2. **进行小幅调整** - 以小步长（±0.1）更改值以观察细微差异
3. **一致测试** - 在不同 Temperature 设置下使用相同提示进行有效比较
4. **记录结果** - 记录哪些值对特定类型的任务产生最佳结果
5. **创建配置文件** - 将有效的设置保存为 [API 配置文件](/features/api-configuration-profiles) 以便快速访问

请记住，不同的模型对相同的 Temperature 值可能有不同的响应，而启用思考的模型无论你的设置如何，始终使用固定的 Temperature 1.0。

---

## 相关功能

- 适用于 Roo Code 支持的所有 [API 提供商](/providers/openai)
- 与 [自定义指令](/features/custom-instructions) 配合使用以微调响应
- Works alongside [custom modes](/features/custom-modes) you create