# 🛠️ 練習情境佈置指南 (Scenario Setup)

如果你發現你的本地 Repo 太過乾淨，沒有衝突或亂掉的歷史可以練習，請依照以下步驟手動「製造問題」。

---

## 🏗️ 佈置情境 05：Rebase 整理與更新

**目的：** 建立 3 個亂七八糟的 commit，並讓 `main` 領先你的分支。

### 操作步驟：
1. **更新 main：**
   ```bash
   git checkout main
   echo "Update on main" >> README.md
   git add README.md
   git commit -m "Update README on main"
   ```
2. **建立練習分支與亂 commit：**
   ```bash
   git checkout -b test-rebase
   echo "1" >> index.html; git add index.html; git commit -m "fixed typo"
   echo "2" >> index.html; git add index.html; git commit -m "debug again"
   echo "3" >> index.html; git add index.html; git commit -m "test"
   ```
3. **完成！** 現在你可以開始執行 `05-rebase.md` 的任務了。

---

## 🏗️ 佈置情境 06：多人同步開發 (Pull Rebase)

**目的：** 模擬你跟遠端（夥伴）同時修改了同一個分支的情況。

### 操作步驟：
1. **建立共用分支：**
   ```bash
   git checkout main
   git checkout -b feature-shared
   ```
2. **建立你的本地 commit：**
   ```bash
   echo "My local change" >> index.html
   git add index.html
   git commit -m "My feature work"
   ```
3. **模擬遠端（夥伴）已經 Push 了：**
   此處我們手動移動 `origin` 的指標（進階操作）：
   ```bash
   git branch partner-work
   echo "Partner's change" >> index.html
   git add index.html
   git commit -m "Partner's update on shared branch"
   # 將本地的 origin 指向這個新的 commit
   git update-ref refs/remotes/origin/feature-shared HEAD
   # 回到你原本的 commit 狀態
   git reset --hard HEAD~1
   ```
4. **完成！** 輸入 `git log --all --oneline --graph`，你會看到你的 commit 跟 origin 分叉了。

---

## 🏗️ 佈置情境 07：Approve 與 Review

**目的：** 練習 GitHub PR 流程。這部分需要手動在 GitHub 網頁操作。

### 操作步驟：
1. **Push 分支：** 將你的練習分支推送到 GitHub。
   ```bash
   git push origin test-rebase
   ```
2. **開啟網頁：** 到 GitHub Repo 頁面，點擊 **"Pull requests"** -> **"New pull request"**。
3. **設定保護：** 
   - 到 **Settings** > **Branches**。
   - 點擊 **"Add branch protection rule"**。
   - Branch name pattern 輸入 `main`。
   - 勾選 **"Require a pull request before merging"**。
   - 勾選 **"Require approvals"** (Required number: 1)。
4. **練習開始：** 找你的夥伴來對這個 PR 進行「退件」或「留言建議」。

---

## 🧹 如何重來？

如果練習弄爛了想重來，最快的方法是刪除分支：
```bash
git checkout main
git branch -D test-rebase feature-shared
```
然後重新執行上述步驟即可。
