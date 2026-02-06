<p align="center">
  <a href="https://opencode.ai">
    <picture>
      <source srcset="packages/console/app/src/asset/logo-ornate-dark.svg" media="(prefers-color-scheme: dark)">
      <source srcset="packages/console/app/src/asset/logo-ornate-light.svg" media="(prefers-color-scheme: light)">
      <img src="packages/console/app/src/asset/logo-ornate-light.svg" alt="OpenCode logo">
    </picture>
  </a>
</p>
<p align="center">开源 AI 编程助手</p>
<p align="center"><strong>中文汉化版 (Community Chinese Localization)</strong></p>

> ⚠️ **免责声明**
>
> 这是 OpenCode 的社区中文汉化版本，由社区爱好者维护，**非官方版本**。
>
> - 原项目版权归 [Anomaly Labs](https://github.com/anomalyco) 所有
> - 汉化内容仅供学习和个人使用
> - 如有侵权，请联系删除

<p align="center">
  <a href="https://opencode.ai/discord"><img alt="Discord" src="https://img.shields.io/discord/1391832426048651334?style=flat-square&label=discord" /></a>
  <a href="https://www.npmjs.com/package/opencode-ai"><img alt="npm" src="https://img.shields.io/npm/v/opencode-ai?style=flat-square" /></a>
</p>

---

## 📥 下载安装

### 方式一：使用包管理器安装

```bash
# npm
npm i -g opencode-ai@latest

# Windows
scoop install opencode
choco install opencode

# macOS/Linux
brew install anomalyco/tap/opencode
```

### 方式二：下载本仓库的汉化版

访问 [Releases 页面](https://github.com/jaraim/opencode-chinese/releases) 下载：

| 文件 | 大小 | 说明 |
|------|------|------|
| **OpenCode-Setup.exe** | 50 MB | 🎯 安装包（推荐） |
| **opencode-desktop.exe** | 28 MB | 💻 便携版（免安装） |
| **opencode-cli.exe** | 153 MB | ⌨️ 命令行工具 |

---

## ✨ 汉化内容

本版本包含完整的中文界面汉化：

- ✅ **所有命令和菜单项** - TUI、Prompt、Session 路由全部汉化
- ✅ **提示信息和对话框** - 100+ 条 Tips 全部汉化
- ✅ **配置文件描述** - keybinds、permissions、MCP 等配置项汉化
- ✅ **智能体描述** - build、plan、docs、general 等智能体汉化
- ✅ **消息和状态文本** - toast、error、success 等提示汉化

---

## 🎯 智能体 (Agents)

OpenCode 内置两个智能体，可按 `Tab` 键切换：

- **build** - 默认智能体，完整开发权限
  - 可执行文件编辑、bash 命令等操作
  - 适合日常开发工作

- **plan** - 计划模式，只读智能体
  - 禁止文件编辑
  - 运行命令前会询问权限
  - 适合代码分析和规划

还有 **general** 子智能体，用于复杂搜索和多步骤任务。
在消息中使用 `@general` 调用。

---

## 🛠️ 自定义 Skills（4 个）

本版本预装了以下自定义技能：

| 技能名称 | 描述 | 使用方法 |
|-----------|------|----------|
| **bun-file-io** | Bun 文件 API 使用指南，用于文件读写操作 | `@bun-file-io` 或在提示中提及文件操作 |
| **skill-from-masters** | 基于专家方法论创建 AI 技能，包含写作、产品、销售、用户研究、工程等领域最佳实践 | `@skill-from-masters` |
| **mcp-github** | GitHub MCP 工具（渐进式披露优化），按需加载工具节省 90% 上下文 | `@mcp-github` 或提及 GitHub 操作 |
| **github-workflow** | 基于本地 GitHub MCP 的工作流，常用 GitHub 操作指南 | `@github-workflow` |

技能文件位置：`.opencode/skill/`

添加新技能：在 `.opencode/skill/<skill-name>/SKILL.md` 创建技能文件

---

## 🔌 MCP 服务器（10 个）

已配置以下 MCP (Model Context Protocol) 服务器：

### 数据库
| 名称 | 用途 | 命令 |
|------|------|------|
| **PostgreSQL** | PostgreSQL 数据库操作 | `bun x @modelcontextprotocol/server-postgres` |
| **SQLite** | SQLite 数据库操作 | `uvx mcp-server-sqlite` |

### 工具类
| 名称 | 用途 | 命令 |
|------|------|------|
| **Time** | 时间相关功能 | `uvx mcp-server-time` |
| **Memory** | 持久化记忆存储 | `bun x @modelcontextprotocol/server-memory` |
| **Fetch** | HTTP 请求 | `uvx mcp-server-fetch` |
| **Filesystem** | 文件系统操作 | `bun x @modelcontextprotocol/server-filesystem` |

### 开发类
| 名称 | 用途 | 命令 |
|------|------|------|
| **Git** | Git 操作 | `uvx mcp-server-git` |
| **Github** | GitHub API 集成 | `bun x @modelcontextprotocol/server-github` |
| **Everything** | 测试/示例服务器 | `bun x @modelcontextprotocol/server-everything` |
| **Sequential-thinking** | 序列化思考工具 | `bun x @modelcontextprotocol/server-sequential-thinking` |

### 使用方法

1. **查看 MCP 状态**：`Ctrl+X S` 或 `/status`
2. **切换 MCP 服务器**：`Ctrl+X ;` 或 `/mcp`
3. **配置文件**：`opencode.json`

### MCP 配置示例

```json
{
  "mcp": {
    "Github": {
      "type": "local",
      "command": ["bun", "x", "@modelcontextprotocol/server-github"],
      "enabled": true,
      "environment": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token"
      }
    }
  }
}
```

---

## 🚀 快速开始

### 基本使用

```bash
# 启动 OpenCode
opencode

# 查看所有命令
Ctrl+P

# 切换智能体
Tab

# 切换模型
Ctrl+X M

# 新建会话
Ctrl+X N

# 查看会话列表
Ctrl+X L
```

### 常用快捷键

| 快捷键 | 功能 |
|--------|------|
| `Ctrl+P` | 命令面板 |
| `Tab` | 切换智能体 (build/plan) |
| `Ctrl+X T` | 切换主题 |
| `Ctrl+X M` | 切换模型 |
| `Ctrl+X N` | 新建会话 |
| `Ctrl+X L` | 会话列表 |
| `Ctrl+X B` | 切换侧边栏 |
| `Ctrl+X E` | 打开编辑器 |
| `Ctrl+X Y` | 复制最后消息 |
| `Ctrl+X X` | 导出会话 |
| `Escape` | 停止响应 |

---

## 🏗️ 本地构建

如需从源码构建：

```bash
# 克隆仓库
git clone https://github.com/jaraim/opencode-chinese.git
cd opencode

# 安装依赖
bun install

# 构建 CLI 工具
cd packages/opencode
bun run build --single

# 构建桌面应用（需要 Rust）
cd packages/desktop
bun run tauri build
```

构建输出：
- CLI: `packages/opencode/dist/opencode-<平台>-<架构>/bin/opencode`
- 桌面版: `packages/desktop/src-tauri/target/release/bundle/`

---

## 📝 使用提示

### 文件操作
- 输入 `@` 后跟文件名可快速附加文件
- 拖放图片到终端添加为上下文
- `Ctrl+V` 从剪贴板粘贴图片

### 命令执行
- 以 `!` 开头可直接运行 shell 命令（如 `!ls -la`）
- 使用 `/undo` 撤销最后操作
- 使用 `/redo` 恢复撤销的操作

### 会话管理
- `/share` 创建公开分享链接
- `/compact` 精简长会话
- `/rename` 重命名会话

---

## ❓ 常见问题

### 与 Claude Code 有什么不同？

- **100% 开源** - 代码完全开放
- **不绑定提供商** - 支持 Claude、OpenAI、Google 及本地模型
- **开箱即用的 LSP 支持** - 智能代码分析
- **专注 TUI** - 由 neovim 用户打造，极致终端体验
- **客户端/服务器架构** - 支持远程控制

---

## 🤝 参与贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证与归属

- **原项目**: [OpenCode](https://github.com/anomalyco/opencode) by [Anomaly Labs](https://github.com/anomalyco)
- **许可证**: MIT License
- **中文汉化版**: 社区本地化版本，仅供教育目的使用
- **免责声明**: 这是一个非官方社区项目，所有商标和原始代码归其各自所有者所有

---

**加入社区** [Discord](https://discord.gg/opencode) | [X.com](https://x.com/opencode)

**下载地址**: https://github.com/jaraim/opencode-chinese/releases
