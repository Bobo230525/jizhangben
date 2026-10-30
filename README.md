# 余量 · 个人预算账本

一个纯前端、无后端的个人预算记账网页。数据只保存在当前浏览器的 `localStorage`，支持完整 JSON 导出与导入。

## 功能

- 月度收入、支出与两级分类
- 默认预算与每月专属预算
- 严格按交易日期归属月份统计
- 固定弹性、按比例、全部长期、手动四种结算方式
- 弹性使用与长期存钱双资金池
- 代管资金与应收欠款账本
- 月度和年度/低频周期账单
- 响应式中文界面与本地数据备份

## 本地运行

需要 Node.js 20 或更高版本：

```bash
pnpm install
pnpm dev
```

浏览器打开 Vite 输出的本地地址。

## 构建

```bash
pnpm build
```

静态产物位于 `dist/`。本地直接打开构建文件并不适合作为运行方式，请使用：

```bash
pnpm preview
```

## GitHub Pages

有两种方式。推荐使用自动部署：

1. 把整个项目推送到 GitHub。
2. 在仓库 `Settings → Pages` 中把 Source 设为 **GitHub Actions**。
3. 等待 `.github/workflows/deploy.yml` 完成。
4. 打开 `https://<用户名>.github.io/<仓库名>/`。

也可以使用网页版直接上传静态发布文件：

```bash
pnpm build:pages
```

运行后会生成 `github-pages/`。在新 GitHub 仓库中，把该目录里的**所有内容**上传到仓库根目录：

- `index.html`
- `assets/`
- `manifest.webmanifest`
- `sw.js`
- `icon-192.png`
- `icon-512.png`
- `apple-touch-icon.png`
- `.nojekyll`

然后在 `Settings → Pages` 中选择 **Deploy from a branch → main → / (root)**。

## iPhone / PWA

在 Safari 打开已部署网站，使用分享菜单“添加到主屏幕”。应用使用独立窗口显示，并在首次打开后缓存静态资源，供离线启动。


构建使用相对资源路径，因此可直接部署到 GitHub Pages 仓库子路径或其他静态子目录。

## 数据说明

- 所有数据仅存在当前域名、当前浏览器的 `localStorage`。
- 更换设备、清理浏览器数据或更换部署域名之前，请在「数据与备份」中导出 JSON。
- 导入是**覆盖模式**，不会合并数据。
- 周期账单在网页打开时检查到期状态，不依赖后台服务或 GitHub Actions。

## 目录

```text
src/
├─ components/    通用界面组件
├─ pages/         九个业务页面
├─ data.ts        预设分类与初始数据
├─ store.tsx      localStorage 状态与账单到期处理
├─ types.ts       数据模型
└─ utils.ts       金额、月份、预算与结算计算
```

详细需求见 [SPEC.md](./SPEC.md)。
