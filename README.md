# my_github_actions
Download XXX via GitHub Actions
this is template for use github aciton download someting you need.


# ex. 📦 Grafana Plugins Offline Downloader
> 利用 GitHub Actions 在境外环境自动下载 Grafana 官方插件，并打包为 Release 供国内用户离线使用。
> 适用于无法直连 `storage.googleapis.com` 的用户，解决以下报错：

当前默认打包以下三个官方 Explore 增强插件（兼容 Grafana ≥12.0）：

| 插件 | 版本 | 功能 |
|------|------|------|
| [`grafana-lokiexplore-app`](https://grafana.com/grafana/plugins/grafana-lokiexplore-app/) | `v1.0.34` | 增强 Loki 日志探索体验 |
| [`grafana-exploretraces-app`](https://grafana.com/grafana/plugins/grafana-exploretraces-app/) | `v1.3.0` | 统一 Trace 可视化入口 |
| [`grafana-metricsdrilldown-app`](https://grafana.com/grafana/plugins/grafana-metricsdrilldown-app/) | `v1.0.29` | 从指标下钻到日志/链路 |

---

## 🚀 使用步骤

### 1️⃣ 配置工作流（可选：修改插件或版本）

编辑文件：  
`.github/workflows/download-grafana-plugins.yml`

你可以：
- 修改插件版本号
- 增加/删除插件
- 调整输出 ZIP 文件名

> 💡 默认已配置好最新稳定版，开箱即用。

---

### 2️⃣ ⚠️ 【重要】配置 Personal Access Token（解决 403 错误）

GitHub Actions 默认权限不足，**必须手动配置 Token 才能创建 Release**。

#### 步骤如下：

1. **创建 Token**
   - 进入 GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
   - 点击 **Generate new token (classic)**
   - 填写：
     - **Note**: `grafana-plugins-release`
     - **Expiration**: 按需选择
     - **Scopes**: ✅ 勾选 **`repo`**（必须包含 `public_repo`）
   - 点击 **Generate token**，**立即复制生成的 token**（只显示一次！）

2. **添加为仓库 Secret**
   - 回到本仓库 → **Settings** → **Secrets and variables** → **Actions**
   - 点击 **New repository secret**
   - 名称：`MY_GITHUB_ACTIONS_TOKEN`
   - 值：粘贴你刚复制的 token
   - 点击 **Add secret**

> 🔒 Token 仅用于 Action 自动发布 Release，不会出现在日志或代码中。

---

### 3️⃣ 触发 GitHub Actions

1. 进入仓库顶部菜单 → **Actions**
2. 左侧选择工作流：**📦 Download Grafana Plugins**
3. 点击右上角 **Run workflow** → 再点 **Run workflow**
4. 等待 1～2 分钟，直到状态变为 ✅ **Success**

---

### 4️⃣ 下载插件包

1. 返回仓库主页 → 点击 **Releases**
2. 找到最新版本（如 `Grafana Plugins Bundle (...)`）
3. 下载文件：**`grafana-plugins-offline.zip`**

✅ 该文件包含所有插件目录，可直接用于离线部署。

---
