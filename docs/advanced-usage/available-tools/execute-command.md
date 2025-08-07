---
描述: 描述
关键词:
  - execute_command
  - CLI 命令
  - 终端
  - 系统操作
  - Roo Code 工具
  - 命令执行
  - shell 集成
image: /img/social-share.jpg
---

# 执行命令

`execute_command` 工具在用户的系统上运行 CLI 命令。它允许 Roo 执行系统操作、安装依赖、构建项目、启动服务器以及执行其他基于终端的任务，以实现用户目标。

---

## 参数

该工具接受以下参数:

- `command` (必需): 要执行的 CLI 命令。必须对用户的操作系统有效。
- `cwd` (可选): 执行命令的工作目录。如果未提供，则使用当前工作目录。

---

## 功能

此工具直接在用户的系统上执行终端命令，支持从文件操作到运行开发服务器的广泛操作。命令在受管理的终端实例中运行，实时捕获输出，并与 VS Code 的终端系统集成，以实现最佳性能和安全性。

---

## 使用场景

- 安装项目依赖时 (npm install, pip install 等)
- 构建或编译代码时 (make, npm run build 等)
- 启动开发服务器或运行应用程序时
- 初始化新项目时 (git init, npm init 等)
- 执行其他工具无法提供的文件操作时
- 运行测试或 linting 操作时
- 需要为特定技术执行专门命令时

---

## 主要特性

- 与 VS Code shell API 集成，实现可靠的终端执行
- 通过注册表系统在可能时重用终端实例
- 实时反馈，逐行捕获命令输出
- 支持在后台继续运行的长命令
- 允许指定自定义工作目录
- 跨命令执行维护终端历史和状态
- 处理适合用户 shell 的复杂命令链
- 提供详细的命令完成状态和退出代码解释
- 支持带有用户反馈循环的交互式终端应用程序
- 执行期间显示终端以提高透明度
- 使用 shell-quote 解析验证命令安全性
- 阻止潜在危险的子 shell 执行模式
- 与 RooIgnore 系统集成以进行文件访问控制
- 处理终端转义序列以获得清晰的输出

---

## 限制

- 命令访问可能受 RooIgnore 规则和安全验证的限制
- 需要提升权限的命令可能需要用户配置
- 某些命令在不同操作系统上的行为可能有所不同
- 非常长的运行命令可能需要特殊处理
- 文件路径应根据操作系统 shell 规则正确转义
- 并非所有终端功能都适用于远程开发场景

---

## 工作原理

调用 `execute_command` 工具时，它遵循以下过程:

1. **命令验证和安全检查**:
   - 使用 shell-quote 解析命令以识别组件
   - 验证安全限制 (子 shell 使用、受限文件)
   - 检查 RooIgnore 规则以获取文件访问权限
   - 确保命令符合系统安全要求

2. **终端管理**:
   - 通过 TerminalRegistry 获取或创建终端
   - 设置工作目录上下文
   - 准备事件监听器以捕获输出
   - 显示终端以供用户查看

3. **命令执行和监控**:
   - 通过 VS Code 的 shellIntegration API 执行
   - 捕获带有转义序列处理的输出
   - 以 100ms 间隔限制输出处理
   - 监控命令完成或错误
   - 检测编译器等 "热" 进程以进行特殊处理

4. **结果处理**:
   - 去除 ANSI/VS Code 转义序列以获得清晰输出
   - 解释带有详细信号信息的退出代码
   - 如果命令更改了工作目录，则更新工作目录跟踪
   - 提供带有适当上下文的命令状态

---

## 终端实现细节

该工具使用复杂的终端管理系统:

1. **第一优先级: 终端重用**
   - TerminalRegistry 尝试在可能时重用现有终端
   - 这减少了终端实例的激增并提高了性能
   - 跨命令保留终端状态 (工作目录、历史)

2. **第二优先级: 安全验证**
   - 使用 shell-quote 解析命令以进行组件分析
   - 阻止危险模式如 `$(...)` 和反引号
   - 根据 RooIgnore 规则检查命令以进行文件访问控制
   - 基于前缀的允许列表系统验证命令模式

3. **性能优化**
   - 以 100ms 限制间隔处理输出以防止 UI 过载
   - 零拷贝缓冲区管理使用基于索引的跟踪以提高效率
   - 对编译和 "热" 进程进行特殊处理
   - 针对 Windows PowerShell 的平台特定优化

4. **错误和信号处理**
   - 将退出代码映射到详细的信号信息 (SIGTERM, SIGKILL 等)
   - 检测关键故障的核心转储
   - 自动跟踪和处理工作目录更改
   - 从终端断开连接场景中干净恢复

---

## 使用示例

- 设置新项目时，Roo 运行初始化命令如 `npm init -y`，然后安装依赖。
- 构建 Web 应用程序时，Roo 执行构建命令如 `npm run build` 来编译资产。
- 部署代码时，Roo 运行 git 命令将更改提交并推送到仓库。
- 故障排除时，Roo 执行诊断命令以收集系统信息。
- 启动开发服务器时，Roo 启动适当的服务器命令 (例如，`npm start`)。
- 运行测试时，Roo 为项目的测试框架执行测试运行器命令。

---

## 使用示例

在当前目录运行简单命令:
```
<execute_command>
<command>npm run dev</command>
</execute_command>
```

为项目安装依赖:
```
<execute_command>
<command>npm install express mongodb mongoose dotenv</command>
</execute_command>
```

按顺序运行多个命令:
```
<execute_command>
<command>mkdir -p src/components && touch src/components/App.js</command>
</execute_command>
```

在特定目录执行命令:
```
<execute_command>
<command>git status</command>
<cwd>./my-project</cwd>
</execute_command>
```

构建然后启动项目:
```
<execute_command>
<command>npm run build && npm start</command>
</execute_command>
```
