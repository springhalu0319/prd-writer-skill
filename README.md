# PRD Writer Skill for Clawdbot

一个基于 AI 的产品需求文档（PRD）编写技能，帮助你快速完成从需求采集到原型生成的完整工作流。

## ✨ 功能特性

- 📝 **需求采集** - 从会议记录、功能描述中提取结构化需求
- 📋 **Feature List 生成** - 按模块组织功能清单，自动完整性检查
- 📄 **PRD 文档生成** - 生成包含 Mermaid 图表的完整需求文档
- 🎨 **原型生成** - 生成可交互的 HTML 原型（Tailwind CSS）
- 🚀 **Vercel 部署** - 一键部署原型到 Vercel

## 📦 安装

### 方式一：复制到 Clawdbot Skills 目录

```bash
# 克隆仓库
git clone https://github.com/nicekate/prd-writer-skill.git

# 复制到 Clawdbot skills 目录
cp -r prd-writer-skill ~/.clawdbot/skills/prd-writer
```

### 方式二：直接下载

```bash
cd ~/.clawdbot/skills
git clone https://github.com/nicekate/prd-writer-skill.git prd-writer
```

## 🚀 使用方法

安装后，在与 Clawdbot 对话时使用以下触发词即可：

- "帮我写一个 XXX 的 PRD"
- "写需求文档"
- "产品需求说明书"
- "PRD"

### 示例对话

```
用户：帮我写一个旅行行程记录小程序的PRD

Agent：好的，我来帮你写PRD。请先回答几个问题：
1. 目标用户是谁？
2. 核心功能有哪些？
3. 需要哪些端？（App/小程序/后台）

用户：个人用户，包含行程规划、旅途记录、回顾功能，需要App和后台

Agent：[生成 Feature List] → [生成 PRD 文档] → [质量检查]
需要我生成可交互原型吗？

用户：好的，生成原型并部署到 Vercel

Agent：[生成 HTML 原型] → [部署到 Vercel] → 返回在线地址
```

## 📁 Skill 结构

```
prd-writer/
├── SKILL.md                          # 主技能文件
└── references/
    ├── prd-template.md               # PRD 文档模板
    ├── feature-list-template.md      # Feature List 模板
    ├── quality-checklist.md          # 四角色质量检查
    ├── prototype-guide.md            # HTML 原型生成指南
    ├── prompts.md                    # Prompt 模板库
    └── vercel-deploy.md              # Vercel 部署指南
```

## 📄 输出文件

使用此 Skill 后，会在项目目录生成：

| 文件 | 说明 |
|------|------|
| `feature_list.md` | 功能清单（按模块组织） |
| `PRD.md` | 完整的产品需求文档 |
| `quality_report.md` | 四角色质量检查报告 |
| `prototype.html` | 可交互 HTML 原型 |
| `vercel-deploy/` | Vercel 部署项目 |

## 🔄 工作流程

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  需求采集   │ → │ Feature List │ → │  PRD 文档   │
└─────────────┘    └─────────────┘    └─────────────┘
                                            ↓
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ Vercel 部署 │ ← │  原型生成   │ ← │  质量检查   │
└─────────────┘    └─────────────┘    └─────────────┘
```

## 🎯 PRD 模板特点

生成的 PRD 文档包含：

1. **文档信息** - 版本、日期、编写人
2. **项目背景** - 业务目标、目标用户、核心价值
3. **产品架构** - Mermaid mindmap 图
4. **用户角色定义** - 角色和权限表格
5. **核心业务流程** - Mermaid flowchart 图
6. **详细功能说明** - 页面元素、交互逻辑、异常处理
7. **非功能需求** - 性能、安全、兼容性
8. **迭代规划** - MVP 到完整版本规划

## ✅ 质量检查

生成 PRD 后会自动进行四角色审查：

| 角色 | 审查维度 |
|------|----------|
| 🔧 技术负责人 | 技术实现难度、性能、安全风险 |
| 👤 挑剔用户 | 操作便捷性、流程合理性 |
| 📊 运营负责人 | 数据分析、埋点、营销需求 |
| 🧪 测试工程师 | 异常场景、边界条件 |

## 🌐 原型部署

生成的原型可以一键部署到 Vercel：

```bash
cd vercel-deploy
vercel --prod
```

## 📚 参考文档

此 Skill 参考了《AI 辅助产品需求与原型设计工作流》教程，整合了：

- 豆包 App 会议记录提取方法
- Gemini 长上下文分析能力
- Claude Code 文件操作流程
- UI-UX-Pro-Max 原型生成思路

## 🤝 贡献

欢迎提交 Issue 和 PR！

## 📜 License

MIT License
