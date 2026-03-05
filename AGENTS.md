# AGENTS.md - Link Trust Website

This file provides guidance for agentic coding agents working in this repository.

## Project Overview

Link Trust 组织官方网站，使用 Astro 构建的静态站点。部署在腾讯云 EdgeOne。

**技术栈：**
- Astro 5.x - 静态站点生成器
- TypeScript - 类型系统
- HTML/CSS - 页面结构和样式

## Build Commands

所有命令在项目根目录 (`website/`) 执行：

```bash
# 安装依赖
npm install

# 开发模式（启动本地服务器）
npm run dev

# 构建生产版本
npm run build

# 预览生产构建
npm run preview

# Astro CLI 命令
npm run astro -- <command>
```

## Project Structure

```
link-trust/
├── public/              # 静态资源（favicon 等）
├── src/
│   ├── components/      # 可复用 Astro 组件
│   ├── layouts/         # 页面布局组件
│   └── pages/           # 路由页面
│       ├── index.astro  # 首页
│       ├── projects.astro  # 项目展示页
│       └── about.astro  # 关于页面
├── .github/
│   ├── profile/         # GitHub 组织资料
│   │   └── README.md    # 组织介绍
│   └── workflows/       # GitHub Actions
│       └── deploy-edgeone.yml
├── AGENTS.md            # 本文件
├── DEPLOYMENT.md        # 部署指南
├── README.md            # 项目说明
├── astro.config.mjs     # Astro 配置
├── edgeone.yaml         # EdgeOne 部署配置
├── package.json         # 依赖配置
└── tsconfig.json        # TypeScript 配置
```

## Code Style Guidelines

### Astro 组件规范

1. **Frontmatter 格式**
   - 所有 `.astro` 文件必须以 `---` 开头的 frontmatter 开始
   - Props 接口定义使用 TypeScript
   - 导入语句放在 frontmatter 内

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';

interface Props {
  title: string;
  description?: string;
}

const { title, description = "默认描述" } = Astro.props;
---
```

2. **组件结构**
   - 使用语义化 HTML 标签（`<header>`, `<main>`, `<footer>`, `<section>`, `<article>`）
   - 布局组件使用 `<slot />` 插入内容
   - 样式使用 `<style>` 标签，支持 scoped CSS

3. **样式规范**
   - 使用 CSS 变量定义主题色
   - 类名使用 kebab-case（如 `.feature-card`）
   - 响应式设计使用媒体查询
   - 全局样式放在 `BaseLayout.astro` 的 `<style is:global>` 中

### TypeScript 规范

1. **类型定义**
   - 所有组件 Props 必须定义接口
   - 使用可选属性 `?:` 处理非必需参数
   - 数组和对象明确类型

2. **命名约定**
   - 组件文件：PascalCase（如 `BaseLayout.astro`）
   - 变量/函数：camelCase
   - 常量：UPPER_CASE
   - CSS 类：kebab-case

3. **导入规范**
   - 相对路径导入使用 `../` 或 `./`
   - 组件导入按字母顺序
   - 避免循环依赖

### 代码组织

1. **文件内顺序**
   - Frontmatter（导入和逻辑）
   - HTML 模板
   - 样式（`<style>` 标签）

2. **页面路由**
   - 文件名决定路由路径
   - `index.astro` 为目录默认页
   - 动态路由使用 `[param].astro`

### 错误处理

1. **构建错误**
   - 运行 `npm run build` 验证构建
   - 检查 TypeScript 类型错误

2. **运行时错误**
   - Astro 是静态生成，无客户端运行时错误
   - 确保所有动态数据在构建时可用

3. **404 处理**
   - 创建 `404.astro` 处理未找到页面
   - 配置 EdgeOne 路由重定向

## Git 工作流

```bash
# 提交规范
git add .
git commit -m "<type>: <description>"

# 类型：feat, fix, docs, style, refactor, test, chore
git push origin main
```

## Deployment

### GitHub Actions 自动部署

推送到 `main` 分支自动触发 EdgeOne 部署。

**需要的 Secrets：**
- `TENCENT_SECRET_ID`
- `TENCENT_SECRET_KEY`
- `EDGEONE_AREA_ID`
- `EDGEONE_ZONE`

### 手动部署

参考 `DEPLOYMENT.md` 了解详细部署步骤。

## Testing

当前项目无自动化测试。建议：

1. 构建验证：`npm run build`
2. 本地预览：`npm run preview`
3. 链接检查：手动验证所有内部和外部链接
4. 响应式测试：使用浏览器开发者工具

## Common Tasks

### 添加新页面

1. 在 `src/pages/` 创建 `.astro` 文件
2. 导入 `BaseLayout` 组件
3. 添加导航链接到 `BaseLayout.astro`

### 添加新组件

1. 在 `src/components/` 创建组件文件
2. 定义 Props 接口
3. 在页面中导入使用

### 修改样式

1. 组件级样式：在组件 `<style>` 中定义
2. 全局样式：修改 `BaseLayout.astro` 的 `<style is:global>`
3. 主题色：更新 CSS 变量

## External Links

- [Astro 文档](https://docs.astro.build)
- [Astro Discord](https://astro.build/chat)
- [腾讯云 EdgeOne 文档](https://cloud.tencent.com/document/product/1552)
