# GitHub Actions 配置指南

## 问题说明

你的 GitHub Actions 工作流失败是因为缺少必要的 GitHub Secrets 配置。以下是详细的修复步骤。

## 需要添加的 Secrets

### 1. ACCESS_TOKEN (必需)
用于 **Update Fork Star** 工作流。

**如何创建：**
1. 访问 GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. 点击 "Generate new token (classic)"
3. 设置 token 名称（如: `PROFILE_ACCESS_TOKEN`）
4. 选择权限：
   - ✅ `repo` (完整的仓库访问权限)
   - ✅ `workflow` (更新 GitHub Actions 工作流)
5. 点击 "Generate token"
6. **重要**: 复制生成的 token（只显示一次）

**如何添加到仓库：**
1. 访问你的仓库 `MapleQiAN/MapleQiAN`
2. 进入 Settings → Secrets and variables → Actions
3. 点击 "New repository secret"
4. Name: `ACCESS_TOKEN`
5. Secret: 粘贴刚才复制的 token
6. 点击 "Add secret"

---

### 2. METRICS_TOKEN (必需)
用于 **GitHub Metrics** 工作流。

**如何创建：**
1. 访问 GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. 点击 "Generate new token (classic)"
3. 设置 token 名称（如: `METRICS_TOKEN`）
4. 选择权限：
   - ✅ `repo` (完整的仓库访问权限)
   - ✅ `read:org` (读取组织数据)
   - ✅ `read:user` (读取用户数据)
   - ✅ `read:packages` (读取包信息)
   - ✅ `repo:status` (访问提交状态)
5. 点击 "Generate token"
6. 复制生成的 token

**如何添加到仓库：**
1. 访问你的仓库 `MapleQiAN/MapleQiAN`
2. 进入 Settings → Secrets and variables → Actions
3. 点击 "New repository secret"
4. Name: `METRICS_TOKEN`
5. Secret: 粘贴刚才复制的 token
6. 点击 "Add secret"

---

### 3. GH_TOKEN (必需)
用于 **Waka Readme** 工作流。

**注意**: 这个可以使用与 `ACCESS_TOKEN` 或 `METRICS_TOKEN` 相同的 token。

**如果需要创建新的：**
1. 按照上述步骤创建新 token
2. 确保包含 `repo` 权限

**如何添加到仓库：**
1. 访问你的仓库 `MapleQiAN/MapleQiAN`
2. 进入 Settings → Secrets and variables → Actions
3. 点击 "New repository secret"
4. Name: `GH_TOKEN`
5. Secret: 粘贴 token
6. 点击 "Add secret"

---

### 4. WAKATIME_API_KEY (可选，如果使用 WakaTime)
用于 **Waka Readme** 和 **GitHub Metrics** 工作流。

**如何获取：**
1. 访问 [WakaTime Settings](https://wakatime.com/settings/account)
2. 找到 "Secret API Key" 部分
3. 复制 API Key

**如何添加到仓库：**
1. 访问你的仓库 `MapleQiAN/MapleQiAN`
2. 进入 Settings → Secrets and variables → Actions
3. 点击 "New repository secret"
4. Name: `WAKATIME_API_KEY`
5. Secret: 粘贴 WakaTime API Key
6. 点击 "Add secret"

---

## 已修复的工作流问题

### ✅ contrib.yml (3D Contrib)
已添加 `permissions: contents: write` 权限，允许工作流推送更改到仓库。

### ✅ waka.yml (Waka Readme)
已修复 `SHOW_TITLE` 参数格式（从 `true` 改为 `"True"`）。

---

## 验证修复

添加所有必需的 secrets 后：

1. 进入仓库的 Actions 页面
2. 手动触发一个失败的工作流（点击工作流 → Run workflow）
3. 检查工作流是否成功运行

---

## 安全提示

⚠️ **重要**:
- 永远不要在代码中直接暴露 Personal Access Tokens
- 定期轮换你的 tokens
- 只授予工作流所需的最小权限
- 如果 token 泄露，立即在 GitHub Settings 中撤销它

---

## 需要帮助？

如果在配置过程中遇到问题，请：
1. 检查 Actions 页面的错误日志
2. 确认所有 secrets 名称拼写正确
3. 验证 tokens 拥有所需的权限

祝使用愉快！🎉
