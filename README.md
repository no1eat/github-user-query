# GitHub 用户信息查询 🔍

一个纯原生、零依赖的 GitHub 用户信息查询工具。输入用户名，即可查看该用户的详细资料、仓库、Star 仓库、贡献热力图和最近动态。单文件应用，双击即可运行。

## 功能特性

- **用户资料**：头像、姓名、简介、公司、所在地、邮箱、个人网站、Twitter、GitHub 主页等
- **账号统计**：公开仓库、粉丝、关注、获星总数、被 Fork 总数、原创仓库
- **账号年龄**：精确到「年 / 月 / 天」，以及注册周年纪念提醒
- **贡献热力图**：最近一年的贡献图
- **仓库列表**：折叠显示前 6 个，点击「展开全部」后无限滚动加载
- **Star 仓库**：显示 Star 总数 + 前 6 个，点击「展开全部」后无限滚动加载
- **最近动态**：最近 20 条公开活动
- **登录状态**：配置 Token 后限额从 60 次/小时提升到 5000 次/小时
- **动态图标**：标签页图标为蓝色圆角「不」字，可点击变色；支持切换页面背景色

## 文件说明

| 文件 | 说明 |
| --- | --- |
| `deepseek_html_20260908_1813b3.html` | 主页面（单文件应用，浏览器打开即可用） |
| `config.js` | 本地配置，存放真实 Token（已加入 `.gitignore`，勿提交） |
| `config.example.js` | Token 配置模板（可安全发布，复制为 `config.js` 后填入自己的 Token） |
| `README.md` | 项目说明 |

## 如何使用

1. 保证 `deepseek_html_20260908_1813b3.html` 和 `config.js` 在同一个文件夹里。
2. 双击 `deepseek_html_20260908_1813b3.html`，用浏览器打开。
3. 在输入框输入任意 GitHub 用户名（例如 `octocat`），点击「查询」或按回车。
4. 查看该用户的详细资料、仓库、Star 仓库和最近动态。
5. （可选）点击左上角「图标变色」切换标签页图标颜色，点击右上角「背景变色」切换页面背景色。

> 不配置 Token 也能用，但未登录时 GitHub API 限额为 **60 次/小时**，频繁查询容易撞上限。配置 Token 后提升到 **5000 次/小时**。

## Token 配置步骤

1. 打开 GitHub → 右上角头像 → **Settings** → 左侧 **Developer settings** → **Personal access tokens**。
2. 点击 **Tokens (classic)**。
3. 点击 **Generate new token (classic)**。
4. 随便写个名字（比如 `github-user-query`），有效期选 **90 天**。
5. 权限勾选 **public_repo**（只读公开仓库，足够用了）。
6. 点击最下方 **Generate token**，立刻复制那个 `ghp_` 开头的字符串。
7. 把文件夹里的 `config.example.js` 复制一份并重命名为 `config.js`，然后把 Token 粘贴进去：

```js
window.GITHUB_TOKEN = 'ghp_你的Token';
```

8. 保存后刷新页面，顶部提示会从「未登录」变成「已登录（使用 Token，限额 5000 次/小时）」。

## 安全提醒

- Token 属于敏感凭证，请勿提交到公开仓库，也不要分享给他人。
- 项目已自带 `.gitignore`，会自动忽略 `config.js`，请勿强制提交它。
- 如果 Token 不小心泄露，请立即到 GitHub 吊销并重新生成。

## 技术说明

- 纯原生 HTML / CSS / JavaScript，无需构建、无需任何依赖。
- 数据来自 GitHub 公开 REST API（`api.github.com`）。
- 标签页图标使用内联 SVG data URI 动态生成，无外部文件。
