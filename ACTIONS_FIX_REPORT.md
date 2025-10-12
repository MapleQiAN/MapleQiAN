# 🔧 GitHub Actions 故障排查完成报告

## 📊 问题总结

你的 GitHub Actions 工作流出现以下故障：

| 工作流 | 状态 | 原因 |
|--------|------|------|
| ✅ **Snake Contrib** | 正常运行 | 无问题 |
| ✅ **Recent Blog** | 正常运行 | 无问题 |
| ❌ **3D Contrib** | 失败 | 权限不足 |
| ❌ **Update Fork Star** | 失败 | 缺少 ACCESS_TOKEN |
| ❌ **GitHub Metrics** | 失败 | 缺少 METRICS_TOKEN |
| ❌ **Waka Readme** | 失败 | 参数错误 + 缺少 GH_TOKEN |

---

## ✅ 已自动修复的问题

### 1. contrib.yml (3D Contrib) - 权限问题
**问题**: 工作流尝试推送更改时遇到 403 错误  
**原因**: 默认的 `GITHUB_TOKEN` 权限不足  
**修复**: 添加了 `permissions: contents: write` 配置

```yaml
permissions:
  contents: write
```

### 2. waka.yml (Waka Readme) - 参数格式错误
**问题**: `SHOW_TITLE` 参数使用了布尔值 `true`  
**原因**: 该 action 要求使用字符串格式  
**修复**: 改为字符串 `"True"`

```yaml
SHOW_TITLE : "True"  # 原来是 true
```

---

## 🔑 需要手动添加的 Secrets

以下是你需要在 GitHub 仓库设置中添加的 Secrets：

### 必需的 Secrets

1. **ACCESS_TOKEN** - 用于 Fork Star 工作流
   - 权限需求: `repo`, `workflow`
   - [创建教程见下方](#如何创建-personal-access-token)

2. **METRICS_TOKEN** - 用于 GitHub Metrics 工作流
   - 权限需求: `repo`, `read:org`, `read:user`, `read:packages`, `repo:status`
   - [创建教程见下方](#如何创建-personal-access-token)

3. **GH_TOKEN** - 用于 Waka Readme 工作流
   - 权限需求: `repo`
   - 💡 提示: 可以与 ACCESS_TOKEN 使用同一个 token

### 可选的 Secrets

4. **WAKATIME_API_KEY** - 用于 WakaTime 统计（如果你使用 WakaTime）
   - 从 [WakaTime Settings](https://wakatime.com/settings/account) 获取

---

## 📖 详细配置指南

我已经为你创建了两份详细的配置指南：

- **中文版本**: [`GITHUB_ACTIONS_SETUP.md`](./GITHUB_ACTIONS_SETUP.md)
- **English Version**: [`GITHUB_ACTIONS_SETUP_EN.md`](./GITHUB_ACTIONS_SETUP_EN.md)

这些文档包含：
- ✅ 如何创建 Personal Access Token 的详细步骤
- ✅ 每个 token 需要哪些权限
- ✅ 如何添加 Secrets 到仓库
- ✅ 安全最佳实践

---

## 🚀 快速开始（3 步完成）

### 第 1 步：创建 Personal Access Token

1. 访问 [GitHub Personal Access Tokens](https://github.com/settings/tokens)
2. 点击 **Generate new token (classic)**
3. 设置名称和权限（参考上方表格）
4. 点击 **Generate token**
5. ⚠️ **立即复制 token**（只显示一次！）

### 第 2 步：添加 Secrets 到仓库

1. 访问你的仓库: https://github.com/MapleQiAN/MapleQiAN
2. 进入 **Settings** → **Secrets and variables** → **Actions**
3. 点击 **New repository secret**
4. 添加以下 secrets:
   - Name: `ACCESS_TOKEN`, Secret: [你的 token]
   - Name: `METRICS_TOKEN`, Secret: [你的 token]
   - Name: `GH_TOKEN`, Secret: [你的 token]
   - (可选) Name: `WAKATIME_API_KEY`, Secret: [你的 WakaTime key]

### 第 3 步：验证修复

1. 进入仓库的 **Actions** 页面
2. 选择一个之前失败的工作流
3. 点击 **Run workflow** 手动触发
4. 等待工作流完成，检查是否成功 ✅

---

## 🔒 安全提示

⚠️ **重要安全建议**：

- ❌ 永远不要在代码中直接写入 token
- 🔄 定期轮换你的 tokens（建议每 90 天）
- 🛡️ 只授予必要的最小权限
- 🚨 如果 token 泄露，立即在 [GitHub Settings](https://github.com/settings/tokens) 撤销
- 🔍 定期检查 token 的使用情况

---

## 📋 工作流说明

### 已正常运行的工作流

1. **Snake Contrib** (`.github/workflows/snake.yml`)
   - 生成 GitHub 贡献图的蛇形动画
   - 状态: ✅ 正常

2. **Recent Blog** (`.github/workflows/blog.yml`)
   - 自动更新 README 中的博客文章
   - 状态: ✅ 正常

### 需要配置 Secrets 的工作流

3. **3D Contrib** (`.github/workflows/contrib.yml`)
   - 生成 3D 贡献图
   - 需要: 权限配置（✅ 已修复）

4. **Update Fork Star** (`.github/workflows/fork_star.yml`)
   - 更新仓库的 star 和 fork 数量
   - 需要: `ACCESS_TOKEN`

5. **GitHub Metrics** (`.github/workflows/metrics.yml`)
   - 生成详细的 GitHub 活动统计图表
   - 需要: `METRICS_TOKEN`, `WAKATIME_API_KEY`（可选）

6. **Waka Readme** (`.github/workflows/waka.yml`)
   - 在 README 中显示编码时间统计
   - 需要: `GH_TOKEN`, `WAKATIME_API_KEY`（可选）
   - 参数错误: ✅ 已修复

---

## 🆘 故障排查

### 如果工作流仍然失败

1. **检查 Secret 名称**
   - 确保名称拼写完全正确（区分大小写）
   - `ACCESS_TOKEN`, `METRICS_TOKEN`, `GH_TOKEN`, `WAKATIME_API_KEY`

2. **检查 Token 权限**
   - 重新创建 token 时，仔细选择所需的权限
   - 参考上方的权限需求表

3. **查看错误日志**
   - 进入 Actions → 选择失败的工作流 → 点击失败的 job
   - 查看详细的错误信息

4. **手动触发测试**
   - 在 Actions 页面，点击工作流名称
   - 点击 "Run workflow" 按钮
   - 观察执行结果

---

## 📚 参考资源

- [GitHub Actions 官方文档](https://docs.github.com/zh/actions)
- [创建 Personal Access Token](https://docs.github.com/zh/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- [使用 Secrets](https://docs.github.com/zh/actions/security-guides/encrypted-secrets)
- [WakaTime 设置](https://wakatime.com/settings/account)

---

## ✨ 总结

✅ **已完成**:
- 修复了 `contrib.yml` 的权限配置
- 修复了 `waka.yml` 的参数错误
- 创建了详细的中英文配置指南

⏳ **待完成**:
- 添加 `ACCESS_TOKEN` secret
- 添加 `METRICS_TOKEN` secret
- 添加 `GH_TOKEN` secret
- (可选) 添加 `WAKATIME_API_KEY` secret

完成这些配置后，所有的 GitHub Actions 工作流都将正常运行！🎉

---

**有问题?** 请查看详细配置指南或在 GitHub Issues 中提问。

祝你使用愉快！💪
