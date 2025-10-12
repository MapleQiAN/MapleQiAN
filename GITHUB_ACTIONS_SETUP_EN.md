# GitHub Actions Setup Guide (English Version)

## Issue Summary

Your GitHub Actions workflows are failing due to missing GitHub Secrets configuration. Here's a detailed guide to fix them.

## Required Secrets

### 1. ACCESS_TOKEN (Required)
Used by the **Update Fork Star** workflow.

**How to create:**
1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Set token name (e.g., `PROFILE_ACCESS_TOKEN`)
4. Select scopes:
   - ✅ `repo` (Full control of repositories)
   - ✅ `workflow` (Update GitHub Action workflows)
5. Click "Generate token"
6. **Important**: Copy the generated token (shown only once)

**How to add to repository:**
1. Go to your repository `MapleQiAN/MapleQiAN`
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `ACCESS_TOKEN`
5. Secret: Paste the token you just copied
6. Click "Add secret"

---

### 2. METRICS_TOKEN (Required)
Used by the **GitHub Metrics** workflow.

**How to create:**
1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Set token name (e.g., `METRICS_TOKEN`)
4. Select scopes:
   - ✅ `repo` (Full control of repositories)
   - ✅ `read:org` (Read org data)
   - ✅ `read:user` (Read user data)
   - ✅ `read:packages` (Read packages)
   - ✅ `repo:status` (Access commit status)
5. Click "Generate token"
6. Copy the generated token

**How to add to repository:**
1. Go to your repository `MapleQiAN/MapleQiAN`
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `METRICS_TOKEN`
5. Secret: Paste the token
6. Click "Add secret"

---

### 3. GH_TOKEN (Required)
Used by the **Waka Readme** workflow.

**Note**: You can use the same token as `ACCESS_TOKEN` or `METRICS_TOKEN`.

**If creating a new one:**
1. Follow the same steps above
2. Ensure it has the `repo` scope

**How to add to repository:**
1. Go to your repository `MapleQiAN/MapleQiAN`
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `GH_TOKEN`
5. Secret: Paste the token
6. Click "Add secret"

---

### 4. WAKATIME_API_KEY (Optional, if using WakaTime)
Used by **Waka Readme** and **GitHub Metrics** workflows.

**How to get:**
1. Visit [WakaTime Settings](https://wakatime.com/settings/account)
2. Find the "Secret API Key" section
3. Copy the API Key

**How to add to repository:**
1. Go to your repository `MapleQiAN/MapleQiAN`
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `WAKATIME_API_KEY`
5. Secret: Paste your WakaTime API Key
6. Click "Add secret"

---

## Fixed Workflow Issues

### ✅ contrib.yml (3D Contrib)
Added `permissions: contents: write` to allow the workflow to push changes to the repository.

### ✅ waka.yml (Waka Readme)
Fixed `SHOW_TITLE` parameter format (changed from `true` to `"True"`).

---

## Verify the Fix

After adding all required secrets:

1. Go to the Actions tab in your repository
2. Manually trigger a failed workflow (click on the workflow → Run workflow)
3. Check if the workflow runs successfully

---

## Security Tips

⚠️ **Important**:
- Never expose Personal Access Tokens directly in code
- Rotate your tokens regularly
- Only grant the minimum permissions needed
- If a token is compromised, immediately revoke it in GitHub Settings

---

## Need Help?

If you encounter issues during setup:
1. Check the error logs in the Actions tab
2. Ensure all secret names are spelled correctly
3. Verify that tokens have the required permissions

Happy coding! 🎉
