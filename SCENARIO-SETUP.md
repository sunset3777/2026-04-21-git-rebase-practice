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

## 🏗️ 佈置情境 06：功能分支協作 (Feature Branching)

**目的：** 模擬標準的「大功能分支」與「個人任務分支」協作。

### 操作步驟：
1. **第一步：建立大功能分支 (Base Branch)**
   ```bash
   git checkout main
   git checkout -b feature/shop
   echo "Shop Structure" > shop.html
   git add . && git commit -m "feat: 建立商店基礎架構"
   ```
2. **第二步：扮演「夥伴」更新大功能分支**
   ```bash
   echo "Partner: 增加資料庫設定" >> shop.html
   git add . && git commit -m "feat: 增加資料庫連線設定"
   ```
3. **第三步：扮演「你」在更早的起點開發小功能**
   ```bash
   # 回到夥伴動手前的那個 commit (也就是剛剛 main 的位置)
   git checkout -b feature/cart main
   # 故意改同一個檔案製造衝突
   echo "Me: 開發購物車介面" >> shop.html
   git add . && git commit -m "feat: 購物車 UI 初版"
   ```
4. **完成佈置！** 請輸入 `git log --oneline --graph --all`。
   你會看到 `feature/cart` 與 `feature/shop` 分叉了。

---

## 🏗️ 佈置情境 07：Approve 與 Review

**目的：** 練習 GitHub PR 流程。這部分需要手動在 GitHub 網頁操作。

### 操作步驟：
1. **Push 分支：** 將你的練習分支推送到 GitHub。
   ```bash
   git push origin feature/cart
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
git branch -D test-rebase feature/shop feature/cart
```
