---
name: prd-writer
description: 撰写Markdown格式的产品需求说明书(PRD)，并生成可交互原型。触发条件：用户提到"需求文档"、"需求说明书"、"PRD"、"产品需求"、"写需求"、"原型"等关键词。集成 UI-UX-Pro-Max 设计系统。
---

# PRD 编写技能

基于 AI 辅助的产品需求文档(PRD)撰写工作流，集成 UI-UX-Pro-Max 设计系统。

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

### 阶段4：原型生成（集成 UI-UX-Pro-Max）

若用户需要原型，**必须先使用 UI-UX-Pro-Max 生成设计系统**：

#### Step 1: 生成设计系统

```bash
python3 ui-ux-pro-max/scripts/search.py "<产品类型> <行业> <风格关键词>" --design-system -p "项目名称"
```

示例：
```bash
# 旅行 App
python3 ui-ux-pro-max/scripts/search.py "travel lifestyle mobile app" --design-system -p "Travel App"

# SaaS 产品
python3 ui-ux-pro-max/scripts/search.py "SaaS dashboard enterprise" --design-system -p "Analytics Pro"

# 电商
python3 ui-ux-pro-max/scripts/search.py "ecommerce fashion beauty" --design-system -p "Beauty Store"
```

#### Step 2: 获取详细设计数据（按需）

```bash
# 获取配色方案
python3 ui-ux-pro-max/scripts/search.py "travel lifestyle" --domain color

# 获取字体配对
python3 ui-ux-pro-max/scripts/search.py "modern elegant" --domain typography

# 获取 UX 准则
python3 ui-ux-pro-max/scripts/search.py "mobile animation" --domain ux

# 获取技术栈指南
python3 ui-ux-pro-max/scripts/search.py "responsive form" --stack html-tailwind
```

#### Step 3: 生成原型

基于设计系统输出，生成 HTML 原型：
- 使用推荐的 UI 风格（如 Glassmorphism、Minimalism）
- 应用推荐的配色方案
- 使用推荐的字体配对
- 遵循 UX 准则

**技术规格**：
- 单文件 HTML（Tailwind CSS + 原生 JS）
- 支持页面跳转、表单校验、loading 状态
- 响应式设计（移动端/桌面端）
- 可直接浏览器打开

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

## UI-UX-Pro-Max 设计数据

本 Skill 集成了完整的 UI-UX-Pro-Max 设计数据库：

### 可搜索的设计域

| 域 | 内容 | 示例关键词 |
|---|------|-----------|
| `product` | 产品类型推荐 | SaaS, e-commerce, healthcare, beauty |
| `style` | UI 风格 | glassmorphism, minimalism, dark mode |
| `color` | 配色方案 | saas, ecommerce, healthcare, fintech |
| `typography` | 字体配对 | elegant, playful, professional |
| `landing` | 页面结构 | hero, testimonial, pricing |
| `chart` | 图表类型 | trend, comparison, funnel |
| `ux` | UX 准则 | animation, accessibility, z-index |

### 可用技术栈

`html-tailwind`（默认）、`react`、`nextjs`、`vue`、`svelte`、`swiftui`、`react-native`、`flutter`、`shadcn`

## 输出文件

- `feature_list.md` - 功能清单
- `PRD.md` - 完整需求文档
- `design-system/` - 设计系统（由 UI-UX-Pro-Max 生成）
- `prototype.html` - 可交互原型
- `prototype/` - Cloudflare Pages 部署目录

## 质量检查

生成后以四个角色审视：
1. **技术负责人**：技术实现难度、性能、安全
2. **挑剔用户**：操作便捷性、流程合理性
3. **运营负责人**：数据分析、营销推广
4. **测试工程师**：异常场景、边界问题

## UI 质量检查清单

在交付原型前验证：

### 视觉质量
- [ ] 不使用 emoji 作为图标（使用 SVG）
- [ ] 所有图标来自统一图标库（Heroicons/Lucide）
- [ ] Hover 状态不会导致布局偏移
- [ ] 使用主题色（bg-primary）而非 var() 包装

### 交互
- [ ] 所有可点击元素有 `cursor-pointer`
- [ ] Hover 状态提供清晰视觉反馈
- [ ] 过渡动画平滑（150-300ms）
- [ ] 键盘导航时焦点状态可见

### 亮/暗模式
- [ ] 亮色模式文字有足够对比度（4.5:1 最低）
- [ ] 玻璃/透明元素在亮色模式下可见
- [ ] 边框在两种模式下都可见

### 无障碍
- [ ] 所有图片有 alt 文本
- [ ] 表单输入有 label
- [ ] 颜色不是唯一的指示器
- [ ] 尊重 `prefers-reduced-motion`
