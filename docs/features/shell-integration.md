---
description: 了解 Roo Code 如何与您的 shell 集成以执行命令。终端问题和 shell 配置的故障排除指南。
keywords:
  - shell 集成
  - 终端命令
  - 命令执行
  - shell 配置
  - 故障排除
image: /img/social-share.jpg
---

# 终端 Shell 集成

终端 Shell 集成是一项关键功能，使 Roo Code 能够在您的终端中执行命令并智能处理其输出。这种 AI 与您的开发环境之间的双向通信释放了强大的自动化能力。

---

## 什么是 Shell 集成？

Shell 集成在 Roo Code 中自动启用，并直接连接到您的终端命令执行生命周期，无需您进行任何设置。这个内置功能允许 Roo：

- 通过 [`execute_command`](/advanced-usage/available-tools/execute-command) 工具代表您执行命令
- 实时读取命令输出，无需手动复制粘贴
- 自动检测和修复运行中的应用程序错误
- 观察命令退出代码以确定成功或失败
- 跟踪您在项目中导航时的工作目录变化
- 无需用户干预即可智能响应终端输出
- 使用出现在命令执行消息旁边的停止按钮直接从聊天界面停止运行中的命令。

<img src="/img/v3.15/v3.15.png" alt="聊天界面中的停止命令按钮" width="600" />

当您要求 Roo 执行安装依赖、启动开发服务器或分析构建错误等任务时，shell 集成会在后台工作，使这些交互变得流畅有效。

---

## Shell 集成故障排除

Shell 集成内置于 Roo Code 中，在大多数情况下会自动工作。如果您看到 "Shell 集成不可用" 消息或遇到命令执行问题，请尝试以下解决方案：

1. **将 VSCode/Cursor 更新到最新版本**（需要 VSCode 1.93+）
2. **确保选择了兼容的 shell**：命令面板 (`Ctrl+Shift+P` 或 `Cmd+Shift+P`) → "Terminal: Select Default Profile" → 选择 bash、zsh、PowerShell 或 fish
3. **Windows PowerShell 用户**：运行 `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` 然后重启 VSCode
4. **WSL 用户**：将 `. "$(code --locate-shell-integration-path bash)"` 添加到您的 `~/.bashrc`

---

## 命令执行回退

Roo Code 具有执行命令的回退机制。如果您选择使用 VS Code 的终端集成（通过取消选中 [`禁用终端 shell 集成`](#disable-terminal-shell-integration) 设置）而该集成失败，则此机制最为相关。

- **工作原理**：如果 Roo Code 配置为使用 VS Code 的终端集成但无法连接或遇到问题，它可能会自动尝试使用后台进程直接执行命令。这是一种回退机制，以确保命令仍会尝试运行。
- **通知**：如果使用此回退机制，您可能会在聊天中看到通知，表明命令正在运行，但没有 Roo 的内联终端或 VS Code 的 shell 集成的全部功能（例如，实时输出流或精确的退出代码检测可能受到限制）。
<img src="/img/v3.15.0/v3.15.0.png" alt="命令执行回退通知示例" width="600" />

- **解决方案**：如果您遇到此回退机制，通常表明您的 VS Code shell 集成设置存在问题。请查看本文档中的故障排除步骤，或考虑使用 Roo Code 推荐的内联终端，确保 [`禁用终端 shell 集成`](#disable-terminal-shell-integration) 设置已选中。

<img src="/img/shell-integration/shell-integration-12.png" alt="Roo Code 推荐的内联终端运行中" width="600" />
*Roo Code 推荐的内联终端示例。*


---

## 终端集成设置

Roo Code 提供设置以微调其与终端的交互方式。要访问这些设置：
1. 单击 Roo Code 侧边栏右上角的 <Codicon name="gear" /> 图标。
2. 在打开的设置窗格中，从左侧菜单中选择 "Terminal" 组。

### 基本设置

#### 终端输出限制
<img src="/img/shell-integration/shell-integration.png" alt="终端输出限制滑块设置为 500" width="600" />
此设置控制 Roo Code 从您的命令中捕获多少输出。如果您担心令牌使用或 Roo 处理非常长的输出时似乎很慢（您仍会得到开头和结尾），请考虑降低此值。如果您经常需要直接在 Roo 上下文中获取长命令的更多中间内容，请考虑增加此值，但要注意潜在的令牌成本。默认值：500 行。

#### 压缩进度条输出
<img src="/img/shell-integration/shell-integration-10.png" alt="压缩进度条输出复选框" width="600" />
保持此选项启用（默认）以获得更清晰的输出和令牌节省。它使 Roo Code 处理进度条或旋转器等动态输出更像真实终端，仅显示最终状态。仅在极少数情况下，如果您特别需要调试进度条或类似动态显示的中间原始输出时才禁用此选项。

### 高级设置

:::info 重要
**这些设置需要重启终端**

对高级终端设置的更改仅在重启终端后生效。要重启终端：

1. 单击终端面板中的垃圾桶图标以关闭当前终端
2. 通过 Terminal → New Terminal 或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（反引号）打开新终端

更改任何这些设置后，请始终重启所有打开的终端。
:::

#### 继承环境变量
<img src="/img/shell-integration/shell-integration-11.png" alt="继承环境变量复选框" width="600" />
此设置控制 Roo Code 的终端会话是否使用与您的主 VSCode/Cursor 环境相同的环境变量（如 `PATH`、API 密钥等）。它直接镜像 VSCode 全局设置 [`terminal.integrated.inheritEnv`](https://code.visualstudio.com/docs/editor/integrated-terminal#_inherit-environment-variables)。如果您希望 Roo 命令在您的常规 VSCode 终端中使用相同的上下文和工具，请保持此选项启用（VSCode 默认）。仅在您需要为 Roo 的终端任务提供完全干净、隔离的环境或正在排除复杂的环境变量冲突时才考虑禁用它。

### 运行时环境
在 macOS（可能还有其他操作系统）上，提供给 VSCode 的环境，以及随之而来的 Roo Code，可能会因 VSCode 的启动方式而有所不同。
如果从命令行 `vscode` 命令启动，VSCode 和 Roo Code 将从启动它的 shell 继承环境，一切（通常）都会正常。
如果从 Finder、Dock 或 Spotlight 启动，从 `.zshrc` 或 `.zprofile` 导出的环境可能会缺失。如果您在这些文件之一中设置了环境变量，并且在运行 VSCode 时发现它们缺失，请将它们移动到 .zshenv，并注销再重新登录，以便窗口管理器获取新的环境设置。

#### 禁用终端 shell 集成
<img src="/img/shell-integration/shell-integration-9.png" alt="禁用终端 shell 集成复选框" width="600" />
此设置决定 Roo Code 如何执行终端命令。
-   **保持此复选框选中（推荐）：** Roo Code 将使用其内置的内联终端执行命令，直接在聊天界面中显示输出。此方法通常很稳健，提供清晰的输出，是大多数用户通过 Roo Code 与终端命令交互的首选方式。它确保命令在 Roo Code 管理的一致环境中运行。

    <img src="/img/shell-integration/shell-integration-12.png" alt="'禁用终端 shell 集成'选中时的 Roo Code 内联终端" width="600" />
    *Roo Code 的内联终端，在 "禁用终端 shell 集成" 选中时处于活动状态。*

-   **取消选中此复选框（使用 VS Code 的终端集成）：** Roo Code 将尝试直接在您的活动 VS Code 终端面板中运行命令。这种替代方法可能对特定边缘情况有用，如果您明确需要命令在您完全自定义的 VS Code shell 环境中运行，或需要与 VS Code 终端的特定功能交互。然而，这可能有时不太可靠，具体取决于您的 shell 设置和 VS Code 版本。

以下设置是高级选项，**仅在您取消选中 '禁用终端 shell 集成'**（选择使用 VS Code 的终端集成而不是 Roo Code 推荐的内联终端）时适用：

##### 终端 shell 集成超时
<img src="/img/shell-integration/shell-integration-1.png" alt="终端 shell 集成超时滑块设置为 15s" width="600" />
如果启用了 shell 集成但您仍然看到 'Shell 集成不可用'，特别是在复杂的 shell 设置下（例如，带有许多插件的 Zsh，或加载缓慢的企业环境），您的 shell 可能需要太长时间来初始化。增加此值以给您的 shell 更多时间向 Roo Code 发出就绪信号。尝试增加 5-10 秒。默认值：15s（如 UI 中所示）。

##### 终端命令延迟
<img src="/img/shell-integration/shell-integration-2.png" alt="终端命令延迟滑块设置为 0ms" width="600" />
如果命令输出显示不完整或 Roo 似乎错过了命令输出的结尾（即使启用了 shell 集成），小延迟可能会有帮助。引入小延迟（例如，50ms 或 100ms）。这给终端更多时间在 Roo Code 认为命令完成之前刷新所有输出。这是针对 VSCode 终端或某些 shell 中潜在时序问题的解决方法（参见 VSCode 错误 [#237208](https://github.com/microsoft/vscode/issues/237208)）。默认值：0ms。

##### 启用 PowerShell 计数器解决方法
<img src="/img/shell-integration/shell-integration-3.png" alt="启用 PowerShell 计数器解决方法复选框" width="600" />
特定于 PowerShell 用户。如果您发现 Roo Code 在*连续多次运行完全相同的 PowerShell 命令*时遇到困难，或 PowerShell 命令的输出捕获不可靠，请启用此选项。这会为命令添加唯一计数器以帮助 PowerShell 区分它们。

##### 清除 ZSH EOL 标记
<img src="/img/shell-integration/shell-integration-4.png" alt="清除 ZSH EOL 标记复选框" width="600" />
特定于 Zsh 用户。如果 Zsh 在行尾不以换行符结尾，有时会添加特殊字符（通常是 `%`）。如果 Roo Code 似乎误解或混淆了 Zsh 命令的输出，特别是如果输出的最后一行似乎包含意外字符，请启用此选项。这会尝试移除该标记 (`PROMPT_EOL_MARK=''`)。

##### 启用 Oh My Zsh 集成
<img src="/img/shell-integration/shell-integration-5.png" alt="启用 Oh My Zsh 集成复选框" width="600" />
适用于使用流行的 Oh My Zsh 框架的 Zsh 用户。如果您使用 Oh My Zsh 并遇到其他设置无法解决的终端命令执行或输出渲染的一般问题，请启用此选项。这通过设置 `ITERM_SHELL_INTEGRATION_INSTALLED=Yes` 帮助 Roo Code 与 Oh My Zsh 的特定 shell 集成机制对齐。可能需要重启 IDE。

##### 启用 Powerlevel10k 集成
<img src="/img/shell-integration/shell-integration-6.png" alt="启用 Powerlevel10k 集成复选框" width="600" />
适用于使用 Powerlevel10k 主题的 Zsh 用户。如果您的 Powerlevel10k 提示（可能相当复杂）似乎干扰了 Roo Code 正确检测命令边界、解析输出或跟踪当前工作目录的能力，请启用此选项。这会设置 `POWERLEVEL9K_TERM_SHELL_INTEGRATION=true`。

##### 启用 ZDOTDIR 处理
<img src="/img/shell-integration/shell-integration-7.png" alt="启用 ZDOTDIR 处理复选框" width="600" />
针对具有自定义 Zsh 启动文件位置的 Zsh 用户的高级选项。如果您使用 `ZDOTDIR` 指定 Zsh 配置文件（如 `.zshrc`）的自定义目录，请启用此选项。此设置通过为 Roo Code 自己的集成脚本创建隔离的临时 `ZDOTDIR` 来帮助 Roo Code 正确处理此类设置，防止与您的个人 Zsh 环境发生冲突。

---

## Shell 集成工作原理

Shell 集成实时将 Roo 连接到您的终端命令执行过程：

1. **连接**：当您打开终端时，VS Code 会与您的 shell 建立特殊连接。

2. **命令跟踪**：VS Code 通过检测以下内容来监控您的终端活动：
   - 新提示何时出现
   - 您何时输入命令
   - 命令何时开始运行
   - 命令何时完成（以及是否成功或失败）
   - 您当前所在的目录

3. **不同 Shell，相同结果**：每种 shell 类型（Bash、Zsh、PowerShell、Fish）在幕后实现方式略有不同，但它们都为 Roo 提供相同的功能。

4. **信息收集**：Roo 可以看到正在运行的命令、它们运行的位置、运行时间、是否成功以及它们的完整输出 - 所有这些都无需您手动复制粘贴。

---

## Shell 集成故障排除

### PowerShell 执行策略（Windows）

PowerShell 默认限制脚本执行。要配置：

1. 以管理员身份打开 PowerShell
2. 检查当前策略：`Get-ExecutionPolicy`
3. 设置适当策略：`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`

常见策略：
- `Restricted`：不允许脚本（默认）
- `RemoteSigned`：本地脚本可以运行；下载的脚本需要签名
- `Unrestricted`：所有脚本都运行但有警告
- `AllSigned`：所有脚本都必须签名

### 手动 Shell 集成安装

如果自动集成失败，请将适当的行添加到您的 shell 配置中：

**Bash** (`~/.bashrc`)：
```bash
[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path bash)"
```

**Zsh** (`~/.zshrc`)：
```bash
[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path zsh)"
```

**PowerShell** (`$Profile`)：
```powershell
if ($env:TERM_PROGRAM -eq "vscode") { . "$(code --locate-shell-integration-path pwsh)" }
```

**Fish** (`~/.config/fish/config.fish`)：
```fish
string match -q "$TERM_PROGRAM" "vscode"; and . (code --locate-shell-integration-path fish)
```

### 终端自定义问题

如果您使用终端自定义工具：

**Powerlevel10k**:
```bash
# 在 ~/.zshrc 中引用 powerlevel10k 之前添加
typeset -g POWERLEVEL9K_TERM_SHELL_INTEGRATION=true
```

**替代方法**：在 Roo Code 中启用 Powerlevel10k 集成设置。

### 验证 Shell 集成状态

使用以下命令确认 shell 集成是否处于活动状态：

**Bash**:
```bash
set | grep -i '[16]33;'
echo "$PROMPT_COMMAND" | grep vsc
trap -p DEBUG | grep vsc
```

**Zsh**:
```zsh
functions | grep -i vsc
typeset -p precmd_functions preexec_functions
```

**PowerShell**:
```powershell
Get-Command -Name "*VSC*" -CommandType Function
Get-Content Function:\Prompt | Select-String "VSCode"
```

**Fish**:
```fish
functions | grep -i vsc
functions fish_prompt | grep -i vsc
```

Shell 集成处于活动状态的视觉指示器：
1. 终端标题栏中的 Shell 集成指示器
2. 命令检测高亮显示
3. 终端标题中的工作目录更新
4. 命令持续时间和退出代码报告

---

## WSL 终端集成方法

在使用 Windows Subsystem for Linux (WSL) 时，有两种不同的方法可以在 VSCode 中使用 WSL，每种方法对 shell 集成有不同的影响：

### 方法 1：VSCode Windows 与 WSL 终端

在此设置中：
- VSCode 在 Windows 中原生运行
- 您使用 VSCode 中的 WSL 终端集成功能
- Shell 命令通过 WSL 桥执行
- 由于 Windows-WSL 通信可能会遇到额外延迟
- Shell 集成标记可能会受到 WSL-Windows 边界的影响：您必须确保在 WSL 环境中为您的 shell 加载了 `source "$(code --locate-shell-integration-path <shell>)"`，因为它可能不会自动加载；请参见上文。

### 方法 2：VSCode 在 WSL 内运行

在此设置中：
- 您直接从 WSL 内部使用 `code .` 启动 VSCode
- VSCode 服务器在 Linux 环境中原生运行
- 直接访问 Linux 文件系统和工具
- 更好的性能和可靠性用于 shell 集成
- 由于 VSCode 在 Linux 环境中原生运行，因此会自动加载 shell 集成
- 推荐用于 WSL 开发的方法

为了在 WSL 中获得最佳的 shell 集成，我们建议：
1. 打开您的 WSL 发行版
2. 导航到您的项目目录
3. 使用 `code .` 启动 VSCode
4. 在 VSCode 中使用集成终端

---

## 已知问题与解决方法

### Cygwin (bash, zsh)

Cygwin 在 Windows 系统上提供了一个类 Unix 环境。要在 VS Code 中将 Cygwin 配置为您的终端：

1. 从 [https://www.cygwin.com/](https://www.cygwin.com/) 安装 Cygwin

2. 打开 VS Code 设置：
   - 选择 文件 > 首选项 > 设置
   - 点击右上角的 "打开设置 (JSON)" 图标
   
3. 将以下配置添加到您的 `settings.json`（在顶级大括号 `{}` 内）：
   ```json
   {
     "terminal.integrated.profiles.windows": {
       "Cygwin": {
         "path": "C:\\cygwin64\\bin\\bash.exe",
         "args": ["--login"],
         "env": {"CHERE_INVOKING": "1"}
       }
     },
     "terminal.integrated.defaultProfile.windows": "Cygwin"
   }
   ```

   > 注意：如果您安装了 32 位 Cygwin，请使用 `"C:\\cygwin\\bin\\bash.exe"` 作为路径。

4. 了解配置：
   - `path`：指向您 Cygwin 安装中的 Bash 可执行文件
   - `args`：`--login` 标志确保 shell 读取配置文件
   - `env`：`CHERE_INVOKING` 环境变量告诉 Cygwin 使用当前目录作为工作目录
   - `terminal.integrated.defaultProfile.windows`：将 Cygwin 设置为默认终端配置文件

5. 打开新的 Cygwin 终端：
   - 按 Ctrl+Shift+` 打开新的终端，或
   - 按 `F1`，输入 "Terminal: Create New Terminal (with Profile)"，然后选择 "Cygwin"

虽然我们的测试表明这种方法可以开箱即用，但如果您在 Cygwin 中遇到 shell 集成问题，请确保您已在 Cygwin bash 配置文件中添加了适当的 shell 集成钩子，如 "手动 Shell 集成安装" 部分所述。

### VS Code Shell 集成用于 Fish + Cygwin on Windows

对于在 Cygwin 环境中运行 Fish 终端的 Windows 用户，以下是 VS Code 的 shell 集成工作方式：

1.  **(可选) 定位 Shell 集成脚本：**
    在 *VS Code 中* 打开您的 Fish 终端并运行以下命令：
    ```bash
    code --locate-shell-integration-path fish
    ```
    这将输出 `shellIntegration.fish` 脚本的路径。记下此路径。

2.  **更新您的 Fish 配置：**
    编辑您的 `config.fish` 文件（通常位于您的 Cygwin 主目录中的 `~/.config/fish/config.fish`）。添加以下行，最好在 `if status is-interactive` 块内或文件末尾：

    ```fish
    # 示例 config.fish 结构
    if status is-interactive
        # 您的其他交互式 shell 配置...
        # 自动定位集成脚本：
        string match -q "$TERM_PROGRAM" "vscode"; and . (code --locate-shell-integration-path fish)

        # 或者如果上述方法对您不起作用：
        # 引用 VS Code shell 集成脚本
        # 重要：将下面的示例路径替换为您在步骤 1 中找到的实际路径。
        # 确保路径是 Cygwin 可以理解的格式（例如，使用 /cygdrive/c/...）。
        # source "/cygdrive/c/Users/YourUser/.vscode/extensions/..../shellIntegration.fish"
    end
    ```
    *请记住将示例路径替换为您在步骤 1 中找到的实际路径，并正确格式化为 Cygwin 格式。*

3.  **配置 VS Code 终端配置文件：**
    打开您的 VS Code `settings.json` 文件 (Ctrl+Shift+P -> "Preferences: Open User Settings (JSON)")。在 `terminal.integrated.profiles.windows` 下更新或添加 Fish 配置文件，如下所示：

    ```json
    {
      // ... 其他设置 ...

      "terminal.integrated.profiles.windows": {
        // ... 其他配置文件 ...

        // 推荐：使用 bash.exe 作为登录 shell 启动 fish
        "fish": {
          "path": "C:\\cygwin64\\bin\\bash.exe", // 或您的 Cygwin bash 路径
          "args": [
            "--login", // 确保运行登录脚本（对 Cygwin 环境很重要）
            "-i",      // 确保 bash 以交互方式运行
            "-c",
            "exec fish" // 用 fish 替换 bash 进程
          ],
          "icon": "terminal-bash" // 可选：使用可识别的图标
        }
        // 替代方法（如果上述方法失败）：直接启动 fish
        "fish-direct": {
          "path": "C:\\cygwin64\\bin\\fish.exe", // 确保这在您的 Windows PATH 中或提供完整路径
          // 在这里使用 'options' 而不是 'args'；否则，您可能会遇到 "terminal process terminated exit code 1" 错误。
          "options": ["-l", "-c"], // 示例：登录和交互标志。
          "icon": "terminal-fish" // 可选：使用 fish 图标
        }
      },

      // 可选：如果需要，将 fish 设置为默认值
---

## 已知问题与解决方法
      // "terminal.integrated.defaultProfile.windows": "fish", // 或 "fish-direct" 取决于您使用的内容

      // ... 其他设置 ...
    }
    ```
    *注意：在 Cygwin 环境中，使用 `bash.exe --login -i -c "exec fish"` 通常更可靠，因为它确保在 `fish` 启动之前正确设置环境。然而，如果这种方法不起作用，请尝试 `fish-direct` 配置文件配置。*

4.  **重启 VS Code：**
    完全关闭并重新打开 Visual Studio Code 以应用更改。

5.  **验证：**
    在 VS Code 中打开一个新的 Fish 终端。Shell 集成功能（如命令装饰、更好的命令历史导航等）现在应该处于活动状态。您可以通过运行简单的命令如 `echo "Hello from integrated Fish!"` 来测试基本功能。 <img src="/img/shell-integration/shell-integration-8.png" alt="Fish Cygwin 集成示例" width="600" />

此设置在使用 Cygwin、Fish 和 Starship 提示符的 Windows 系统上可靠运行，并应帮助具有类似配置的用户。


### VSCode 1.98 之后的 Shell 集成失败

**问题**：在 VSCode 更新到 1.98 版本之后，Shell 集成可能会失败，并显示错误 "VSCE output start escape sequence (]633;C or ]133;C) not received"。

**解决方案**：
1. **设置终端命令延迟**：
   - 在 Roo Code 设置中将终端命令延迟设置为 50ms
   - 更改此设置后重启所有终端
   - 这匹配了旧的默认行为，可能会解决问题，但一些用户报告说 0ms 的值效果更好。这是对上游 VSCode 问题的解决方法。

2. **回滚 VSCode 版本**：
   - 从 [VSCode Updates](https://code.visualstudio.com/updates/v1_98) 下载 VSCode v1.98
   - 替换您当前的 VSCode 安装
   - 无需备份 Roo 设置

3. **WSL 特定的解决方法**：
   - 如果使用 WSL，请确保从 WSL 内部使用 `code .` 启动 VSCode

4. **ZSH 用户**：
   - 尝试在 Roo 设置中启用一些或所有与 ZSH 相关的解决方法
   - 这些设置无论您的操作系统如何都可以提供帮助


### Ctrl+C 行为

**问题**：如果在 Roo 尝试运行命令时终端中已经输入了文本，Roo 将首先按 Ctrl+C 清除行，这可能会中断正在运行的进程。

**解决方法**：在要求 Roo 执行终端命令之前，请确保您的终端提示符为空（没有部分命令输入）。

### 多行命令问题

**问题**：跨多行的命令可能会混淆 Roo，并可能将先前命令的输出与当前输出混合。

**解决方法**：不要使用多行命令，而是使用 `&&` 进行命令链接，将所有内容保持在一行上（例如，`echo a && echo b` 而不是将每个命令输入到单独的行上）。

### PowerShell 特定问题

1. **过早完成**：PowerShell 有时会在显示所有输出之前告诉 Roo 命令已完成。
2. **重复命令**：PowerShell 可能会拒绝连续运行相同的命令两次。

**解决方法**：启用 "PowerShell 计数器解决方法" 设置，并在设置中将终端命令延迟设置为 150ms，以给命令更多时间完成。

### 终端输出不完整

**问题**：有时 VS Code 不会显示或捕获命令的所有输出。

**解决方法**：如果您注意到输出缺失，请尝试关闭并重新打开终端选项卡，然后再次运行命令。这会刷新终端连接。

### Python 虚拟环境 (venv) 问题

**问题**：禁用 shell 集成将禁用 venv；venv 由 VSCode 管理，Roo 对此一无所知，因为禁用 shell 集成使用了完全不同的机制来运行命令 (execa)。

**解决方法**：如果您需要在 Roo Code 中使用 Python 虚拟环境，您可以尝试：

```bash
killall code # 关闭所有 vscode 窗口！
. venv/bin/activate
code
```

这样环境在 code 启动之前就已配置，因此 Roo 应该继承它。

---

## 故障排除资源

### 检查调试日志
当发生 shell 集成问题时，请检查调试日志：
1. 打开 帮助 → 切换开发人员工具 → 控制台
2. 将 "显示所有级别" 设置为查看所有日志消息
3. 查找包含 `[Terminal Process]` 的消息
4. 检查错误消息中的 `preOutput` 内容：
   - 空的 preOutput (`''`) 表示 VSCode 没有发送数据
   - 这表明可能存在 VSCode shell 集成问题，或者超出我们控制范围的上游错误
   - 缺少 shell 集成标记可能需要调整设置以解决可能的上游错误或与 shell 初始化和 VSCode 加载特殊 shell 集成钩子相关的本地工作站配置问题

### 使用 VSCode 终端集成测试扩展
[VSCode 终端集成测试扩展](https://github.com/KJ7LNW/vsce-test-terminal-integration) 通过测试不同的设置组合来帮助诊断 shell 集成问题：


1. **当命令卡住时**：
   - 如果您看到 "command already running" 警告，请单击 "Reset Stats" 以重置终端状态
   - 这些警告表明 shell 集成未工作
   - 尝试不同的设置组合，直到找到有效的组合
   - 如果真的卡住了，请通过关闭窗口并按 F5 重启扩展

2. **测试设置**：
   - 系统地尝试不同的组合：
     * 终端命令延迟
     * Shell 集成设置
   - 记录哪些组合成功或失败
   - 这有助于识别 shell 集成问题的模式

3. **报告问题**：
   - 一旦找到有问题的配置
   - 记录确切的设置组合
   - 记下您的环境（操作系统、VSCode 版本、shell 和任何 shell 提示自定义）
   - 打开一个包含这些详细信息的问题，以帮助改进 shell 集成

### 其他资源

- [VSCode 终端输出问题 #237208](https://github.com/microsoft/vscode/issues/237208)
- [VSCode 终端集成测试存储库](https://github.com/KJ7LNW/vsce-test-terminal-integration)
- [Roo Code Shell 集成架构 PR](https://github.com/RooCodeInc/Roo-Code/pull/1365)

---

## 支持

如果您仍然遇到问题：

1. 检查 [Roo Code GitHub 问题](https://github.com/RooCodeInc/Roo-Code/issues)
2. 创建一个新问题，包含：
   - 操作系统和 VSCode 版本
   - Shell 类型
   - 重现步骤
   - 错误消息

如需额外帮助，请加入我们的 [Discord](https://discord.gg/roocode)。
