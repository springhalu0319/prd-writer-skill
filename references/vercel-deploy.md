# Vercel 部署指南

## 项目结构

生成可部署到 Vercel 的项目结构：

```
prototype/
├── public/
│   └── index.html          # 主页面
├── api/                    # (可选) Serverless Functions
│   └── hello.js
├── vercel.json             # Vercel 配置
└── package.json            # 项目配置
```

## 快速生成

### 1. 创建项目目录

```bash
mkdir -p prototype/public prototype/api
```

### 2. vercel.json 配置

```json
{
  "version": 2,
  "public": true,
  "cleanUrls": true,
  "trailingSlash": false,
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "X-XSS-Protection", "value": "1; mode=block" }
      ]
    }
  ],
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

### 3. package.json（可选）

```json
{
  "name": "prototype",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "npx serve public",
    "build": "echo 'Static site, no build needed'"
  }
}
```

### 4. 主页面 public/index.html

将生成的原型 HTML 放入 `public/index.html`

## 多页面支持

如果原型有多个页面：

```
prototype/
├── public/
│   ├── index.html          # 首页
│   ├── login.html          # 登录页
│   ├── dashboard.html      # 仪表盘
│   └── assets/
│       ├── style.css
│       └── script.js
├── vercel.json
└── package.json
```

### 多页面 vercel.json

```json
{
  "version": 2,
  "routes": [
    { "src": "/login", "dest": "/login.html" },
    { "src": "/dashboard", "dest": "/dashboard.html" },
    { "src": "/(.*)", "dest": "/index.html" }
  ]
}
```

## 部署命令

### 方式1：CLI 部署

```bash
# 安装 Vercel CLI
npm i -g vercel

# 进入项目目录
cd prototype

# 登录（首次）
vercel login

# 部署预览
vercel

# 部署生产
vercel --prod
```

### 方式2：Git 连接

1. 将代码推送到 GitHub/GitLab
2. 在 Vercel Dashboard 导入项目
3. 自动检测为静态站点
4. 每次 push 自动部署

## 环境变量（可选）

如需配置环境变量：

### vercel.json 中配置

```json
{
  "env": {
    "API_URL": "https://api.example.com"
  }
}
```

### HTML 中使用（通过 API 路由）

```javascript
// api/config.js
export default function handler(req, res) {
  res.json({
    apiUrl: process.env.API_URL
  });
}
```

## Serverless API（可选）

如果原型需要简单的后端 API：

### api/hello.js

```javascript
export default function handler(req, res) {
  const { name = 'World' } = req.query;
  res.status(200).json({
    message: `Hello ${name}!`,
    timestamp: new Date().toISOString()
  });
}
```

### api/submit.js（表单提交示例）

```javascript
export default async function handler(req, res) {
  if (req.method !== 'POST') {
    return res.status(405).json({ error: 'Method not allowed' });
  }
  
  const { name, email } = req.body;
  
  // 模拟处理
  console.log('Received:', { name, email });
  
  res.status(200).json({
    success: true,
    message: '提交成功',
    data: { name, email }
  });
}
```

### 前端调用 API

```javascript
async function submitForm() {
  const response = await fetch('/api/submit', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      name: document.getElementById('name').value,
      email: document.getElementById('email').value
    })
  });
  const data = await response.json();
  showToast(data.message);
}
```

## 部署检查清单

- [ ] `public/index.html` 存在且可正常打开
- [ ] 所有静态资源路径使用相对路径或 `/` 开头
- [ ] 外部 CDN 资源使用 HTTPS
- [ ] `vercel.json` 配置正确
- [ ] 本地 `npx serve public` 测试通过

## 常见问题

### 1. 资源 404
确保路径正确：
```html
<!-- ❌ 错误 -->
<script src="script.js"></script>

<!-- ✅ 正确 -->
<script src="/assets/script.js"></script>
```

### 2. 路由刷新 404
添加 SPA 重写规则到 vercel.json：
```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```

### 3. API 跨域
Vercel 同域 API 无需配置 CORS，直接用相对路径 `/api/xxx`
