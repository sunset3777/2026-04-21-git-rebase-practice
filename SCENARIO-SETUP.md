# 🛠️ 練習情境佈置指南 (Scenario Setup)

如果你發現你的本地 Repo 太過乾淨，沒有衝突或亂掉的歷史可以練習，請依照以下步驟手動「製造問題」。

---

## 🏗️ 佈置情境 05：Rebase 整理與更新

**目的：** 建立 3 個亂七八糟的 commit，並讓 `main` 領先你的分支。

### 操作步驟：
1. **更新 main：**
   ```bash
   git checkout main
   echo "Update on main" >> README.md && git add . && git commit -m "Update README on main"
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

## 🏗️ 佈置情境 06：多人同步開發 (單人模擬版)

**目的：** 模擬你在開發時，夥伴已經搶先一步 Push 到遠端的情境。即使沒有遠端 Repo，我們也能透過「切換分支」來完美模擬。

### 操作步驟：
1. **第一步：扮演「夥伴」（右手）**
   我們先在 `feature-shared` 分支上寫好一段內容。
   ```bash
   git checkout main
   git checkout -b feature-shared
   echo "Partner: 我改了第一行" > index.html
   git add index.html
   git commit -m "Partner's update"
   ```
2. **第二步：扮演「你自己」（左手）**
   我們要「回到過去」夥伴還沒動手前，來開發你的新功能。
   ```bash
   # 回到 main 分支起點，開一個新分支代表你自己的進度
   git checkout -b my-work main
   # 寫下你的內容（故意改同一行來製造衝突）
   echo "Me: 我也改了第一行" > index.html
   git add index.html
   git commit -m "My feature work"
   ```
3. **完成佈置！** 請輸入 `git log --oneline --graph --all`。
   你會看到 `my-work` 與 `feature-shared` 分叉成兩條平行線了！

### 💡 如何開始練習：
請在 `my-work` 分支執行：`git rebase feature-shared`。
這就等同於在真實環境中執行 `git pull --rebase`。

---

## 🏗️ 佈置情境 07：Approve 與 Review

**目的：** 練習 GitHub PR 流程。這部分需要手動在 GitHub 網頁操作。

### 操作步驟：
1. **Push 分支：** 將你的練習分支推送到 GitHub。
   ```bash
   git push origin my-work
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

如果練習弄爛了想重來，最快的方法是刪除測試分支：
```bash
git checkout main
git branch -D test-rebase feature-shared my-work
```
