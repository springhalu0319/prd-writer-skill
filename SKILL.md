---
name: prd-writer
description: 撰写Markdown格式的产品需求说明书(PRD)。触发条件：用户提到"需求文档"、"需求说明书"、"PRD"、"产品需求"、"写需求"等关键词，或明确要求撰写产品/功能需求规格。
---

# PRD 编写技能

基于 AI 辅助的产品需求文档(PRD)撰写工作流。

## 工作流程

### 阶段1：需求采集

若用户提供了会议记录、需求描述或功能清单，先整理为结构化需求：

```
## 核心业务流程
- 🔴 P0 功能名称：功能描述

## 用户端功能
- 🟡 P1 功能名称：功能描述

## 管理端功能
- 🟢 P2 功能名称：功能描述
```

优先级标注：🔴 P0（必须有）/ 🟡 P1（重要）/ 🟢 P2（优化项）

### 阶段2：Feature List 生成

按模块组织功能表格：

| 功能编号 | 功能名称 | 功能描述 | 优先级 | 备注 |
|---------|---------|---------|--------|------|
| U-01 | 手机号注册 | 用户通过手机号+验证码完成账号注册 | P0 | 需防刷机制 |

**完整性检查**：主动指出缺失环节（如有"加入购物车"但没"购物车编辑"）

### 阶段3：PRD 文档生成

使用 `references/prd-template.md` 模板生成完整PRD，包含：

1. 文档信息（版本、日期、编写人）
2. 项目背景（业务目标、目标用户、核心价值）
3. 产品架构（Mermaid mindmap）
4. 用户角色定义
5. 核心业务流程（Mermaid flowchart）
6. 详细功能说明（每个功能含：描述、前置条件、页面元素、交互逻辑、异常处理）
7. 非功能需求（性能、安全、兼容性）
8. 迭代规划

### 阶段4：原型生成（可选）

若用户需要原型，使用 UI-UX-Pro-Max 技能生成可交互 HTML 文件：

**设计能力**（来自 UI-UX-Pro-Max）：
- 57 种 UI 风格（Glassmorphism、Minimalism、Brutalism 等）
- 95 种行业配色（SaaS、电商、金融、医疗等）
- 56 种字体配对（Google Fonts）
- 98 条 UX 准则

**技术规格**：
- 单文件 HTML（Tailwind CSS + 原生 JS）
- 支持页面跳转、表单校验、loading 状态
- 响应式设计（移动端/桌面端）
- 可直接浏览器打开

**生成示例**：
```
用户：生成一个 SaaS 风格的原型
AI：使用 Corporate Blue 配色 + Minimalism 风格 + Inter 字体
```

### 阶段5：Cloudflare Pages 部署（可选）

若用户需要部署原型，使用 Cloudflare Pages（国内可访问）：

```bash
# 安装 Wrangler CLI
npm install -g wrangler

# 部署
cd prototype
wrangler pages deploy . --project-name=your-project-name
```

部署后获得地址：`https://your-project.pages.dev`

详见 `references/cloudflare-deploy.md`

## 输出文件

- `feature_list.md` - 功能清单
- `PRD.md` - 完整需求文档
- `prototype.html` - 可交互原型（可选）
- `prototype/` - Cloudflare Pages 部署目录（可选）

## 质量检查

生成后以四个角色审视：
1. **技术负责人**：技术实现难度、性能、安全
2. **挑剔用户**：操作便捷性、流程合理性
3. **运营负责人**：数据分析、营销推广
4. **测试工程师**：异常场景、边界问题
