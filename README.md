# 🍬一颗跳跳糖

实用软件与精品网站导航，基于 [WebStack-Hugo](https://github.com/shenweiyan/WebStack-Hugo) 模板构建的静态导航站。

## 特性

- 14 个主分类、87 个子分类、490+ 精选站点，数据来源于「小众技术工具库」
- 全部 logo 本地化存储，加载失败自动回退默认图标
- 左侧边栏 + 搜索 + 一言 + 网站提交入口
- 按本地时间自动切换日间/夜间模式（19:00–07:00，可在 `config.toml` 调整，手动切换优先）
- 糖果主题 SVG logo，日间/夜间双版本
- GitHub Pages 子路径 / 自有服务器根路径 双部署适配（`absURL` 动态拼接）

## 本地开发

```bash
# 需要先安装 Hugo extended (>= 0.152.2)
hugo server

# 浏览器访问 http://localhost:1313/
```

## 目录结构

```
├── config.toml                 # 站点配置（站点名、分类、夜间模式、logo 路径等）
├── data/webstack.yml           # 导航数据（分类 + 站点条目）
├── content/about.md            # 关于页面
├── static/assets/images/logos/ # 本地化站点 logo（490+）
├── themes/WebStack-Hugo/       # 主题（含少量本地化修改）
├── Dockerfile / nginx.conf     # 服务器 Docker 部署
└── .github/workflows/deploy.yml
```

## 部署

推送到 `main` 分支自动触发 GitHub Actions：

1. **GitHub Pages** — 构建并发布到 `https://qiect.github.io/tttnav/`
2. **阿里云服务器** — 构建静态文件 → SCP 上传 → Docker（nginx:alpine）运行在 `8001` 端口
   - 依赖仓库 Secrets：`SERVER_USERNAME`、`SERVER_PASSWORD`

## 添加 / 修改导航数据

编辑 `data/webstack.yml`，按现有格式追加分类或站点条目即可；logo 放入 `static/assets/images/logos/` 并在条目中引用文件名，未提供 logo 的站点自动使用默认图标。
