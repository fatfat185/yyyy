# 🧪 实验室观察管理系统 (Lab Observation Manager)

用于科研实验（如乳液稳定性实验）的观察时间管理和提醒工具。

纯前端单文件应用，无需后端，数据存储在浏览器 LocalStorage 中。

## 功能特性

- **样品管理** — 添加、编辑、删除、复制实验样品
- **自定义观察点** — 自由配置观察时间点（小时 + 分钟双输入，如 2h30min）
- **批量添加** — 逗号分隔一次输入多个观察点（如 `1h,2h,4h,6h,8h,24h`）
- **自动计算观察时间** — 观察时间 = 起始时间 + 观察间隔，严格按真实时间计算
- **实时倒计时** — 每秒刷新，显示剩余天/时/分/秒
- **浏览器提醒** — 观察前弹出通知 + 声音（阈值可自定义）
- **一键完成** — 点击完成自动记录完成时间
- **实验照片** — 每个观察任务支持上传照片（自动压缩）和备注
- **数据统计** — 顶部卡片显示样品总数、待观察、已完成、已逾期
- **CSV 导入/导出** — 支持数据备份和迁移
- **LocalStorage 持久化** — 关闭浏览器数据不丢失
- **响应式设计** — 支持电脑和手机浏览器

## 可选 PWA 增强

在 `lab-observation-manager.html` 的 `<head>` 中加入以下两行即可启用 PWA（可安装到桌面）和自定义图标：

```html
<link rel="icon" type="image/svg+xml" href="/favicon.svg">
<link rel="manifest" href="/manifest.json">
```

这不会影响任何现有功能。

## 部署到 GitHub Pages + Cloudflare Pages

### 项目结构

```
├── lab-observation-manager.html   # 主应用（入口）
├── _headers                       # Cloudflare 安全头 + 缓存策略
├── _redirects                     # 根路径重写 → 主应用
├── favicon.svg                    # 网站图标（烧瓶 SVG）
├── manifest.json                  # PWA 清单（可选）
├── robots.txt                     # SEO 爬虫规则
├── sitemap.xml                    # 站点地图
├── 404.html                       # 自定义 404 页面
└── README.md                      # 本文件
```

### 第一步：上传到 GitHub

```bash
# 在 GitHub 上创建新仓库，例如 lab-observation-manager

# 在项目目录初始化 git
cd /Users/fatfat/Desktop/ai
git init
git add lab-observation-manager.html _headers _redirects favicon.svg manifest.json robots.txt sitemap.xml 404.html README.md
git commit -m "初始化实验室观察管理系统"
git branch -M main
git remote add origin https://github.com/你的用户名/lab-observation-manager.git
git push -u origin main
```

### 第二步：连接 Cloudflare Pages

1. 打开 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 左侧菜单 → **Workers & Pages** → **Pages** → **连接到 Git**
3. 选择你的 GitHub 仓库
4. 构建设置：
   | 配置项 | 值 |
   |--------|-----|
   | **Framework preset** | None |
   | **Build command** | （留空） |
   | **Build output directory** | `.` |
   | **Root directory** | （留空） |
5. 点击 **Save and Deploy**

### 部署原理

- **`_redirects`** 将根路径 `/` 重写为 `/lab-observation-manager.html`（200 状态码，浏览器地址栏不变）
- **`_headers`** 设置安全头和缓存策略
- Cloudflare Pages 自动分发到全球 CDN 节点

### 自定义域名（可选）

1. Cloudflare Pages → 你的项目 → **Custom domains**
2. 输入你的域名 → 按提示配置 DNS
3. Cloudflare 自动申请 SSL 证书

## 本地使用

直接用浏览器打开 `lab-observation-manager.html` 即可。建议允许浏览器通知权限以获得观察提醒。

## 浏览器兼容性

Chrome、Edge、Firefox、Safari 全支持。

## 许可证

MIT License
