# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在本仓库工作时提供指引。

## 项目概述

杭州容游和杭州咕哩的公司静态官网，托管在 Firebase Hosting 上。页面内容为公司简介、用户协议和隐私政策。

## 部署

Firebase 项目 ID 为 `onyou-d3894`，托管根目录为 `public/`。

```bash
# 部署到 Firebase（需要安装 firebase-tools 并有项目权限）
firebase deploy --only hosting
```

Firebase CLI 需要登录认证。如果开了 VPN，先设置代理：

```bash
export http_proxy=http://localhost:<代理端口号>
firebase login
```

## 架构

存在三个站点目录，但只有 `public/` 是当前生效的托管根目录：

- **`public/`** — 当前部署的站点，杭州容游 (onyoufun.com) 页面。
- **`public-onyoufun/`** — 容游站点的另一版本，未部署，仅作备份参考。
- **`public-guli/`** — 杭州咕哩站点，未部署，仅作备份参考。

如需切换部署的站点，将对应目录的内容替换 `public/` 即可。

每个站点的目录结构一致：`index.html` + `web_files/`（CSS 在 `web_files/` 下，图片在 `web_files/i/` 下，隐私政策和用户协议为独立 HTML 文件，各自的 CSS 在对应子目录中）。

## CI/CD

- **推送至 `main` 分支**：自动部署到 Firebase 生产环境（live channel）。
- **Pull Request**：自动部署到预览 channel 供审阅。
