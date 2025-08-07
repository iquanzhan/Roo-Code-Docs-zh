---
description: 了解推荐用于 Roo Code 的 MCP 服务器，包括 Context7。学习如何通过分步说明安装和配置 MCP 服务器。
keywords:
  - MCP 服务器
  - Context7
  - Roo Code MCP
  - MCP 安装
  - MCP 配置
  - 推荐服务器
image: /img/social-share.jpg
sidebar_label: 推荐的 MCP 服务器
---

# 推荐的 MCP 服务器

虽然 Roo Code 可以连接到任何遵循规范的模型上下文协议 (MCP) 服务器，但社区已经构建了几个开箱即用的高质量服务器。本页面整理了我们**积极推荐**的服务器，并提供分步设置说明，以便您在几分钟内开始工作。

> 我们将保持此列表的更新。如果您维护了一个希望我们考虑的服务器，请提交拉取请求。

---

## Context7

`Context7` 是我们首选的通用 MCP 服务器。它附带了一组高度需求的工具，通过单个命令安装，并且在每个支持 MCP 的主要编辑器中都有出色的支持。

### 为什么我们推荐 Context7

* **一键安装** – 所有内容都已打包，无需本地构建步骤。
* **跨平台** – 在 macOS、Windows、Linux 上运行，或在 Docker 内部运行。
* **积极维护** – 来自 Upstash 团队的频繁更新。
* **丰富的工具集** – 数据库访问、网络搜索、文本工具等。
* **开源** – 以 MIT 许可证发布。

---

## 在 Roo Code 中安装 Context7

有两种常见的注册服务器方式：

1. **全局配置** – 在每个工作区中都可用。
2. **项目级配置** – 与您的代码一起提交到版本控制中。

我们将在下面介绍这两种方式。

### 1. 全局配置

1. 通过点击 <Codicon name="server" /> 图标打开 Roo Code **MCP 设置**面板。
2. 点击 **编辑全局 MCP**。
3. 将下面的 JSON 粘贴到 `mcpServers` 对象内并保存。

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

**Windows (cmd.exe) 变体**

```json
{
  "mcpServers": {
    "context7": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

在 **Windows (cmd)** 上，您可能还需要通过 `cmd.exe` 调用 `npx`：

<img src="/img/recommended-mcp-servers/context7-global-setup-fixed.png" alt="将 Context7 添加到全局 MCP 设置" width="600" />

### 2. 项目级配置

如果您更喜欢将配置提交到您的仓库，请在项目根目录创建一个名为 `.roo/mcp.json` 的文件，并添加相同的代码段：

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

**Windows (cmd.exe) 变体**

```json
{
  "mcpServers": {
    "context7": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

<img src="/img/recommended-mcp-servers/context7-project-setup-fixed.png" alt="将 Context7 添加到项目级 MCP 文件" width="600" />

> 当全局和项目文件都定义了同名服务器时，**项目配置优先**。

---

## 验证安装

1. 确保在 MCP 设置面板中打开了 **启用 MCP 服务器**。
2. 您现在应该看到列出的 **Context7**。如果尚未运行，请点击 <Codicon name="activate" /> 切换开关启动它。
3. 首次调用 Context7 工具时，Roo Code 会提示您。批准请求以继续。

<img src="/img/recommended-mcp-servers/context7-running-fixed.png" alt="Context7 在 Roo Code 中运行" width="400" />

---

## 下一步

* 在服务器面板中浏览 Context7 附带的工具列表。
* 为最常使用的工具配置 **始终允许** 以简化您的工作流程。
* 想要公开您自己的 API？请查看 [MCP 服务器创建指南](/features/mcp/using-mcp-in-roo#enabling-or-disabling-mcp-server-creation)。

寻找其他服务器？请关注此页面 – 我们将很快添加更多推荐！