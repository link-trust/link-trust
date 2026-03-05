# Link Trust Website

Link Trust 组织的官方网站。

## 技术栈

- [Astro](https://astro.build/) - 现代静态站点生成器
- TypeScript - 类型安全

## 开发

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build

# 预览生产构建
npm run preview
```

## 部署

本网站部署在腾讯云 EdgeOne。

### 自动部署

配置 GitHub Actions 自动部署：

1. 在 GitHub 仓库 Settings → Secrets and variables → Actions 添加以下 Secrets：
   - `TENCENT_SECRET_ID` - 腾讯云 SecretId
   - `TENCENT_SECRET_KEY` - 腾讯云 SecretKey
   - `EDGEONE_AREA_ID` - EdgeOne 区域 ID
   - `EDGEONE_ZONE` - EdgeOne 站点标识

2. 推送代码到 main 分支自动触发部署

### 手动部署

详见 [DEPLOYMENT.md](DEPLOYMENT.md)

## 项目结构

```
website/
├── public/              # 静态资源
├── src/
│   ├── components/      # Astro 组件
│   ├── layouts/         # 页面布局
│   └── pages/           # 路由页面
│       ├── index.astro  # 首页
│       ├── projects.astro  # 项目页面
│       └── about.astro  # 关于页面
├── .github/workflows/   # GitHub Actions 工作流
├── astro.config.mjs     # Astro 配置
├── edgeone.yaml         # EdgeOne 部署配置
└── package.json         # 项目依赖
```

## 许可证

MIT
