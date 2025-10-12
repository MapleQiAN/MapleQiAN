# 🚀 快速修复指南 - GitHub Actions

> **目标**: 在 5 分钟内完成所有配置，让你的 GitHub Actions 工作流恢复正常运行！

---

## ⚡ 立即开始（3 步完成）

### 步骤 1️⃣: 创建 Personal Access Token

1. 点击打开 → [GitHub Token 创建页面](https://github.com/settings/tokens/new)
2. 填写以下信息：
   - **Note**: `Actions Token for MapleQiAN Profile`
   - **Expiration**: 建议选择 `90 days` 或 `No expiration`（自行承担风险）
   - **Select scopes**: 勾选以下权限
     - ✅ `repo` (全部子选项)
     - ✅ `workflow`
     - ✅ `read:org`
     - ✅ `read:user`
     - ✅ `read:packages`

3. 滚动到底部，点击 **Generate token**
4. ⚠️ **立即复制显示的 token**（这是唯一一次显示！）
   - 格式类似: `ghp_xxxxxxxxxxxxxxxxxxxx`
   - 建议先保存到记事本

---

### 步骤 2️⃣: 添加 Secrets 到仓库

1. 打开你的仓库设置 → [添加 Secrets](https://github.com/MapleQiAN/MapleQiAN/settings/secrets/actions/new)

2. 依次添加以下 3 个 secrets（**使用同一个 token**）：

   **Secret 1: ACCESS_TOKEN**
   - Name: `ACCESS_TOKEN`
   - Secret: 粘贴你刚才复制的 token
   - 点击 "Add secret"

   **Secret 2: METRICS_TOKEN**
   - 再次点击 "New repository secret"
   - Name: `METRICS_TOKEN`
   - Secret: 粘贴同一个 token
   - 点击 "Add secret"

   **Secret 3: GH_TOKEN**
   - 再次点击 "New repository secret"
   - Name: `GH_TOKEN`
   - Secret: 粘贴同一个 token
   - 点击 "Add secret"

3. (可选) 如果使用 WakaTime:
   - 从 [WakaTime Settings](https://wakatime.com/settings/account) 获取 API Key
   - 添加 Secret: Name 为 `WAKATIME_API_KEY`

---

### 步骤 3️⃣: 验证修复

1. 进入 [Actions 页面](https://github.com/MapleQiAN/MapleQiAN/actions)
2. 选择任意一个之前失败的工作流（如 "Update Fork Star"）
3. 点击 **Run workflow** → **Run workflow** 按钮
4. 等待约 1-2 分钟，查看结果
5. 如果显示 ✅ 绿色对勾，恭喜你成功了！

---

## ✅ 完成后的状态

所有工作流应该全部显示绿色 ✅：

- ✅ Snake Contrib - 生成 GitHub 贡献蛇形图
- ✅ Recent Blog - 自动更新博客文章
- ✅ 3D Contrib - 生成 3D 贡献图
- ✅ Update Fork Star - 更新 star/fork 数量
- ✅ GitHub Metrics - 生成统计图表
- ✅ Waka Readme - 显示编码时间

---

## 🆘 遇到问题？

### 常见问题 FAQ

**Q1: Token 创建后在哪里查看？**
> A: Token 只在创建时显示一次！如果丢失，需要重新创建。

**Q2: Secret 名称要区分大小写吗？**
> A: 是的！必须完全匹配: `ACCESS_TOKEN`, `METRICS_TOKEN`, `GH_TOKEN`

**Q3: 可以用同一个 token 吗？**
> A: 可以！如果 token 有足够的权限，三个 Secret 可以使用同一个 token。

**Q4: 工作流还是失败怎么办？**
> A: 查看详细错误日志:
> 1. 进入 Actions → 点击失败的工作流
> 2. 点击红色 ❌ 的 job 名称
> 3. 展开失败的步骤查看错误信息
> 4. 根据错误信息检查 token 权限或 secret 名称

**Q5: Token 需要定期更新吗？**
> A: 建议每 90 天更新一次，或设置过期时间后及时更换。

---

## 📚 更多帮助

- 📖 [完整故障排查报告](./ACTIONS_FIX_REPORT.md)
- 📖 [详细配置指南（中文）](./GITHUB_ACTIONS_SETUP.md)
- 📖 [Detailed Guide (English)](./GITHUB_ACTIONS_SETUP_EN.md)

---

## 🎉 大功告成！

配置完成后，你的 GitHub Profile 将自动显示：
- 📊 详细的活动统计
- 🐍 贡献图动画
- 📝 最新博客文章
- ⏰ 编码时间统计
- 🎨 3D 贡献可视化

享受你的自动化 GitHub Profile 吧！✨

---

**有任何问题？** 在 [Issues](https://github.com/MapleQiAN/MapleQiAN/issues) 中提问。
