# Link Trust Website 部署指南

## 腾讯云 EdgeOne 部署

### 方式一：Git 自动部署（推荐）

1. 登录 [腾讯云 EdgeOne 控制台](https://console.cloud.tencent.com/edgeone)

2. 创建新站点
   - 点击「创建站点」
   - 输入域名：`linktrust.top`
   - 选择「静态网站托管」

3. 配置自动部署
   - 选择「Git 仓库」作为部署源
   - 授权 GitHub 账号
   - 选择仓库：`link-trust/link-trust`（或当前仓库）
   - 分支：`main`
   - 构建配置：
     - 工作目录：`website`
     - 构建命令：`npm install && npm run build`
     - 输出目录：`dist`

4. 完成部署
   - 点击「创建」开始首次部署
   - 后续代码推送到 main 分支将自动触发部署

### 方式二：手动上传

1. 本地构建项目
```bash
cd website
npm install
npm run build
```

2. 在 EdgeOne 控制台上传 `dist` 目录内容

### 方式三：CLI 部署

1. 安装 EdgeOne CLI
```bash
npm install -g @edgeone/cli
```

2. 登录腾讯云
```bash
eod login
```

3. 部署
```bash
cd website
eod deploy
```

## 域名配置

1. 在 EdgeOne 控制台添加自定义域名 `linktrust.top`

2. 配置 DNS
   - 添加 CNAME 记录指向 EdgeOne 提供的域名

3. 配置 HTTPS 证书（EdgeOne 自动签发）

## 环境变量

如需配置环境变量，在 EdgeOne 控制台的「构建配置」中添加。

## 故障排查

- 查看构建日志：EdgeOne 控制台 → 部署记录
- 回滚版本：EdgeOne 控制台 → 部署记录 → 选择历史版本回滚
