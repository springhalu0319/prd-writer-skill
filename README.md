# PRD Writer Skill

一个基于 AI 的产品需求文档（PRD）编写技能，帮助你快速完成从需求采集到原型生成的完整工作流。

**适用于**：Claude Code、Cursor、Windsurf、GitHub Copilot、Clawdbot 等 AI 编码助手。

## ✨ 功能特性

- 📝 **需求采集** - 从会议记录、功能描述中提取结构化需求
- 📋 **Feature List 生成** - 按模块组织功能清单，自动完整性检查
- 📄 **PRD 文档生成** - 生成包含 Mermaid 图表的完整需求文档
- 🎨 **原型生成** - 生成可交互的 HTML 原型（集成 UI-UX-Pro-Max）
- 🚀 **Cloudflare 部署** - 一键部署原型到 Cloudflare Pages（国内可访问）

## 📦 安装

### 方式一：NPM 一键安装（推荐）

```bash
# 进入你的项目目录
cd your-project

# 安装 UI-UX-Pro-Max（原型生成依赖）
npm install -g uipro-cli
uipro init --ai all

# 克隆 PRD Writer Skill
git clone https://github.com/springhalu0319/prd-writer-skill.git .prd-writer
```

### 方式二：按 AI 工具手动安装

| AI 工具 | 安装位置 |
|---------|---------|
| **Claude Code** | `.claude/skills/prd-writer/` |
| **Cursor** | `.cursor/rules/prd-writer.md` 或项目根目录 |
| **Windsurf** | `.windsurf/workflows/prd-writer.md` |
| **GitHub Copilot** | `.github/prompts/prd-writer.prompt.md` |
| **Clawdbot** | `~/.clawdbot/skills/prd-writer/` |
| **其他 Agent** | 项目根目录或 Agent 指定的 skills 目录 |

```bash
# 示例：安装到 Claude Code
mkdir -p .claude/skills
cp -r prd-writer-skill .claude/skills/prd-writer

# 示例：安装到 Clawdbot
cp -r prd-writer-skill ~/.clawdbot/skills/prd-writer
```

## 🚀 使用方法

安装后，在与 AI 助手对话时使用以下触发词即可：

- "帮我写一个 XXX 的 PRD"
- "写需求文档"
- "产品需求说明书"
- "PRD"

### 示例对话

```
用户：帮我写一个旅行行程记录 App 的 PRD

AI：好的，我来帮你写 PRD。请先回答几个问题：
1. 目标用户是谁？
2. 核心功能有哪些？
3. 需要哪些端？（App/小程序/后台）

用户：个人用户，包含行程规划、旅途记录、回顾功能，需要 App 和后台

AI：[生成 Feature List] → [生成 PRD 文档] → [质量检查]
需要我生成可交互原型吗？

用户：好的，生成原型并部署

AI：[使用 UI-UX-Pro-Max 生成 HTML 原型] 
    → [部署到 Cloudflare Pages] 
    → 返回在线地址
```

## 📁 Skill 结构

```
prd-writer/
├── SKILL.md                          # 主技能文件（Agent 读取入口）
├── README.md                         # 使用说明
├── LICENSE                           # MIT 开源协议
└── references/
    ├── prd-template.md               # PRD 文档模板
    ├── feature-list-template.md      # Feature List 模板
    ├── quality-checklist.md          # 四角色质量检查
    ├── prototype-guide.md            # HTML 原型生成指南
    ├── prompts.md                    # Prompt 模板库
    └── cloudflare-deploy.md          # Cloudflare Pages 部署指南
```

## 📄 输出文件

使用此 Skill 后，会在项目目录生成：

| 文件 | 说明 |
|------|------|
| `feature_list.md` | 功能清单（按模块组织） |
| `PRD.md` | 完整的产品需求文档 |
| `quality_report.md` | 四角色质量检查报告 |
| `prototype.html` | 可交互 HTML 原型 |
| `prototype/` | Cloudflare Pages 部署目录 |

## 🔄 工作流程

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  需求采集   │ → │ Feature List │ → │  PRD 文档   │
└─────────────┘    └─────────────┘    └─────────────┘
                                            ↓
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Cloudflare  │ ← │  原型生成   │ ← │  质量检查   │
│   部署      │    │(UI-UX-Pro) │    └─────────────┘
└─────────────┘    └─────────────┘
```

## 🎨 原型生成（集成 UI-UX-Pro-Max）

本 Skill 集成了 [UI-UX-Pro-Max](https://ui.cod.ndjp.net/) 设计技能：

- **57 种 UI 风格**：Glassmorphism、Minimalism、Brutalism 等
- **95 种配色方案**：SaaS、电商、金融、医疗等行业专属配色
- **56 种字体配对**：Google Fonts 精选组合
- **8 种技术栈**：React、Vue、Tailwind、SwiftUI、Flutter 等

### 安装 UI-UX-Pro-Max

```bash
npm install -g uipro-cli
uipro init --ai claude  # 或 cursor/windsurf/all
```

## 🌐 原型部署

生成的原型可以一键部署到 Cloudflare Pages（国内可访问）：

```bash
# 安装 Wrangler CLI
npm install -g wrangler

# 登录 Cloudflare
wrangler login

# 部署
cd prototype
wrangler pages deploy . --project-name=my-prototype
```

部署后获得地址：`https://my-prototype.pages.dev`

## ✅ 质量检查

生成 PRD 后会自动进行四角色审查：

| 角色 | 审查维度 |
|------|----------|
| 🔧 技术负责人 | 技术实现难度、性能、安全风险 |
| 👤 挑剔用户 | 操作便捷性、流程合理性 |
| 📊 运营负责人 | 数据分析、埋点、营销需求 |
| 🧪 测试工程师 | 异常场景、边界条件 |

## 🤝 兼容性

| AI 工具 | 支持状态 |
|---------|----------|
| Claude Code | ✅ 完全支持 |
| Cursor | ✅ 完全支持 |
| Windsurf | ✅ 完全支持 |
| GitHub Copilot | ✅ 完全支持 |
| Clawdbot | ✅ 完全支持 |
| 其他 Agent | ✅ 支持（放入项目根目录） |

## 📚 参考文档

此 Skill 参考了《AI 辅助产品需求与原型设计工作流》教程，整合了：

- 豆包 App 会议记录提取方法
- Gemini 长上下文分析能力
- Claude Code 文件操作流程
- UI-UX-Pro-Max 原型生成能力

## 🤝 贡献

欢迎提交 Issue 和 PR！

## 📜 License

MIT License
