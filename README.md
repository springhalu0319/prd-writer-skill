# PRD Writer Skill

一个基于 AI 的产品需求文档（PRD）编写技能，集成 **UI-UX-Pro-Max** 设计系统，帮助你快速完成从需求采集到专业原型生成的完整工作流。

**适用于**：Claude Code、Cursor、Windsurf、GitHub Copilot、Clawdbot 等 AI 编码助手。

## ✨ 功能特性

- 📝 **需求采集** - 从会议记录、功能描述中提取结构化需求
- 📋 **Feature List 生成** - 按模块组织功能清单，自动完整性检查
- 📄 **PRD 文档生成** - 生成包含 Mermaid 图表的完整需求文档
- 🎨 **专业原型生成** - 集成 UI-UX-Pro-Max，使用专业设计系统
- 🚀 **Cloudflare 部署** - 一键部署原型（国内可访问）

## 🎨 集成 UI-UX-Pro-Max

本 Skill **内置完整的 UI-UX-Pro-Max 设计数据库**：

| 资源 | 数量 | 说明 |
|------|------|------|
| UI 风格 | 67+ | Glassmorphism、Minimalism、Brutalism 等 |
| 配色方案 | 96+ | SaaS、电商、金融、医疗等行业配色 |
| 字体配对 | 57+ | Google Fonts 精选组合 |
| UX 准则 | 99+ | 无障碍、动画、交互最佳实践 |
| 图表类型 | 25+ | 数据可视化推荐 |
| 技术栈 | 13+ | React、Vue、Tailwind、Flutter 等 |

## 📦 安装

### 方式一：Git Clone（推荐）

```bash
# 克隆仓库
git clone https://github.com/springhalu0319/prd-writer-skill.git

# 按你的 AI 工具安装
# Claude Code
cp -r prd-writer-skill ~/.claude/skills/prd-writer

# Cursor
cp -r prd-writer-skill ~/.cursor/skills/prd-writer

# Clawdbot
cp -r prd-writer-skill ~/.clawdbot/skills/prd-writer

# 通用：放入项目根目录
cp -r prd-writer-skill ./prd-writer
```

### 方式二：按 AI 工具手动安装

| AI 工具 | 安装位置 |
|---------|---------|
| **Claude Code** | `.claude/skills/prd-writer/` |
| **Cursor** | `.cursor/skills/prd-writer/` 或项目根目录 |
| **Windsurf** | `.windsurf/skills/prd-writer/` |
| **GitHub Copilot** | `.github/skills/prd-writer/` |
| **Clawdbot** | `~/.clawdbot/skills/prd-writer/` |
| **其他 Agent** | 项目根目录 |

### 前置条件

搜索脚本需要 **Python 3.x**：

```bash
python3 --version  # 检查是否安装

# macOS
brew install python3

# Ubuntu/Debian
sudo apt update && sudo apt install python3

# Windows
winget install Python.Python.3.12
```

## 🚀 使用方法

### 触发词

- "帮我写一个 XXX 的 PRD"
- "写需求文档"
- "产品需求说明书"
- "生成原型"

### 完整工作流示例

```
用户：帮我写一个旅行行程记录 App 的 PRD

AI：好的，我来帮你写 PRD。请先回答几个问题：
1. 目标用户是谁？
2. 核心功能有哪些？

用户：个人用户，包含行程规划、旅途记录、回顾功能

AI：[生成 Feature List] → [生成 PRD 文档] → [质量检查]
需要生成原型吗？

用户：好的，生成原型

AI：我先使用 UI-UX-Pro-Max 生成设计系统...

# 执行设计系统搜索
python3 ui-ux-pro-max/scripts/search.py "travel lifestyle mobile app" --design-system -p "Travel App"

# 获取设计推荐：
# - 风格：Glassmorphism + Minimalism
# - 配色：Travel/Lifestyle palette (Ocean Blue, Sunset Orange)
# - 字体：Inter + Merriweather
# - UX：Mobile-first, 44px touch targets

# 基于设计系统生成原型...
[生成 prototype.html]

用户：部署到线上

AI：[部署到 Cloudflare Pages]
访问地址：https://travel-app.pages.dev
```

## 📁 Skill 结构

```
prd-writer/
├── SKILL.md                    # 主技能文件（Agent 读取入口）
├── README.md                   # 使用说明
├── LICENSE                     # MIT 开源协议
├── references/
│   ├── prd-template.md         # PRD 文档模板
│   ├── feature-list-template.md
│   ├── quality-checklist.md    # 四角色质量检查
│   ├── prototype-guide.md      # 原型生成指南
│   ├── prompts.md              # Prompt 模板库
│   └── cloudflare-deploy.md    # 部署指南
└── ui-ux-pro-max/              # 设计系统（完整集成）
    ├── scripts/
    │   └── search.py           # 设计搜索脚本
    └── data/
        ├── styles.csv          # 67+ UI 风格
        ├── colors.csv          # 96+ 配色方案
        ├── typography.csv      # 57+ 字体配对
        ├── ux-guidelines.csv   # 99+ UX 准则
        ├── charts.csv          # 25+ 图表类型
        ├── products.csv        # 产品类型推荐
        ├── landing.csv         # 落地页结构
        └── stacks/             # 技术栈指南
            ├── html-tailwind.csv
            ├── react.csv
            ├── vue.csv
            └── ...
```

## 🎯 UI-UX-Pro-Max 使用方法

### 1. 生成设计系统（必须）

```bash
python3 ui-ux-pro-max/scripts/search.py "<产品类型> <关键词>" --design-system -p "项目名"
```

示例：
```bash
# SaaS 产品
python3 ui-ux-pro-max/scripts/search.py "SaaS dashboard enterprise" --design-system -p "Analytics"

# 电商
python3 ui-ux-pro-max/scripts/search.py "ecommerce fashion beauty" --design-system -p "Beauty Store"

# 医疗健康
python3 ui-ux-pro-max/scripts/search.py "healthcare wellness app" --design-system -p "Health Tracker"
```

### 2. 详细搜索（按需）

```bash
# 搜索 UI 风格
python3 ui-ux-pro-max/scripts/search.py "glassmorphism dark" --domain style

# 搜索配色
python3 ui-ux-pro-max/scripts/search.py "fintech professional" --domain color

# 搜索字体
python3 ui-ux-pro-max/scripts/search.py "elegant luxury" --domain typography

# 搜索 UX 准则
python3 ui-ux-pro-max/scripts/search.py "animation accessibility" --domain ux

# 搜索技术栈指南
python3 ui-ux-pro-max/scripts/search.py "form validation" --stack html-tailwind
```

## 📄 输出文件

| 文件 | 说明 |
|------|------|
| `feature_list.md` | 功能清单（按模块组织） |
| `PRD.md` | 完整的产品需求文档 |
| `quality_report.md` | 四角色质量检查报告 |
| `design-system/` | UI-UX-Pro-Max 生成的设计系统 |
| `prototype.html` | 可交互 HTML 原型 |
| `prototype/` | Cloudflare Pages 部署目录 |

## 🔄 工作流程

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  需求采集   │ → │ Feature List │ → │  PRD 文档   │
└─────────────┘    └─────────────┘    └─────────────┘
                                            ↓
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Cloudflare  │ ← │  原型生成   │ ← │  设计系统   │
│   部署      │    │             │    │(UI-UX-Pro) │
└─────────────┘    └─────────────┘    └─────────────┘
```

## 🤝 兼容性

| AI 工具 | 支持状态 |
|---------|----------|
| Claude Code | ✅ 完全支持 |
| Cursor | ✅ 完全支持 |
| Windsurf | ✅ 完全支持 |
| GitHub Copilot | ✅ 完全支持 |
| Clawdbot | ✅ 完全支持 |
| 其他 Agent | ✅ 支持（放入项目根目录） |

## 📚 致谢

- [UI-UX-Pro-Max](https://ui.cod.ndjp.net/) - 专业级设计智能数据库
- 《AI 辅助产品需求与原型设计工作流》教程

## 🤝 贡献

欢迎提交 Issue 和 PR！

## 📜 License

MIT License
