# 🧪 Git 實戰練習場

歡迎來到這個練習 repo！  
這裡準備了四個真實開發情境，讓你親手操作、親眼看見每個 Git 指令的效果。


---

## 🗺️ 情境地圖

| # | 情境 | 學習指令 | 難度 |
|---|---|---|---|
| 01 | [工作做到一半，任務來了](./tasks/01-stash.md) | `git stash` | ⭐ |
| 02 | [commit 錯了，怎麼辦？](./tasks/02-reset.md) | `git reset` | ⭐⭐ |
| 03 | [只想要那一個 commit](./tasks/03-cherry-pick.md) | `git cherry-pick` | ⭐⭐⭐ |
| 04 | [推送被拒絕了](./tasks/04-force-push.md) | `git push --force` | ⭐⭐⭐ |

建議依序完成，每個情境都會用到前面建立的觀念。

---

## 🚀 開始之前

### 1. Clone 這個 repo

```bash
git clone https://github.com/study-rocket-coding/2026-04-21-git-practice-template
cd 2026-04-21-git-practice-template
```

### 2. 確認所有 branch 都已存在

```bash
git branch -a
```

你應該會看到以下幾個 branch：

```
  main                  ← 乾淨的基準
  hotfix-bad-commits    ← 預埋亂掉的歷史，供 reset 練習用
  feature-shared        ← 模擬多人協作的共用 branch
  feature-partner       ← 模擬協作者的 branch，供 cherry-pick 練習用
```

### 3. 建立你的練習 branch

```bash
git checkout -b feature-your-name
```

> 把 `your-name` 換成你自己的名字，例如 `feature-alice`。

---

## 📁 Repo 結構

```
git-practice/
├── README.md           # 你現在在這裡
├── tasks/
│   ├── 01-stash.md
│   ├── 02-reset.md
│   ├── 03-cherry-pick.md
│   └── 04-force-push.md
└── src/
    ├── index.html      # 主要練習檔案
    └── style.css       # 輔助練習檔案
```

---

## 💬 遇到問題？

- 先試著自己查 `git status` 和 `git log --oneline`，通常能找到線索。
- 真的卡住了再找協作者討論。
- 任何操作都可以還原——除了 `reset --hard` 和 `force push` 之後要特別小心。

---

## ✍️ 完成後

所有情境走完之後，請依照任務規格的格式撰寫學習反思，並回覆在 Issue 下方。

---

## 🛠️ 給管理者：如何從零建立這個 Repo

第一次建立這個練習 repo 時，請依照以下步驟手動操作。

### 1. 初始化並建立基本檔案

```bash
mkdir git-practice && cd git-practice
git init
git checkout -b main
mkdir src tasks
```

建立 `src/index.html` 和 `src/style.css`（複製 repo 裡的內容），然後：

```bash
git add .
git commit -m "chore: init project"
```

### 2. 在 main 上建立兩個額外的 commit

```bash
git checkout -b feat-style-update
```

在 `src/style.css` 把 header 背景色從 `#4a90d9` 改為 `#2c3e50`：

```css
header {
  background-color: #2c3e50;
  color: white;
  padding: 16px 24px;
}
```

```bash
git add src/style.css
git commit -m "style: update header background color"
```

再把 hero section 的字體大小加大：

```css
.hero p {
  font-size: 18px;
}
```

```bash
git add src/style.css
git commit -m "style: update hero font size"
```

完成後 merge 回 main：

```bash
git checkout main
git merge feat-style-update
git branch -d feat-style-update
```

### 3. 建立 hotfix-bad-commits

```bash
git checkout -b hotfix-bad-commits
```

在 `src/index.html` 把 footer 年份從 2024 改為 2025：

```html
<p>© 2025 git-practice</p>
```

```bash
git add src/index.html
git commit -m "fix: update footer year"
```

在 `src/index.html` 的 `</main>` 前加入以下測試用假資料：

```html
<!-- 測試用，記得移除 -->
<section class="test-data">
  <p>姓名：測試使用者</p>
  <p>Email：test@example.com</p>
  <p>電話：0912-345-678</p>
</section>
```

```bash
git add src/index.html
git commit -m "chore: add test data in index.html"
```

### 4. 建立 feature-partner

```bash
git checkout main
git checkout -b feature-partner
```

在 `src/index.html` 的 `<h1>` 下方加入副標題：

```html
<header>
  <h1>Git 練習專案</h1>
  <p>版本控制實戰練習</p>
</header>
```

```bash
git add src/index.html
git commit -m "feat: add subtitle to header"
```

把 `<h1>` 的文字從「Git 練習專案」改為「Git 實戰練習場」：

```html
<h1>Git 實戰練習場</h1>
```

```bash
git add src/index.html
git commit -m "fix: header title in index.html"
```

把 footer 的 `git-practice` 改為 `Git Practice`：

```html
<p>© 2025 Git Practice</p>
```

```bash
git add src/index.html
git commit -m "fix: typo in footer"
```

### 5. 建立 feature-shared

```bash
git checkout main
git checkout -b feature-shared
```

在 `src/index.html` 的 `</body>` 前加入以下內容，然後 commit：

```html
<!-- 公告區塊 -->
<section class="announcement">
  <p>系統將於本週六凌晨進行維護，請提前備份。</p>
</section>
```

```bash
git add src/index.html
git commit -m "feat: add announcement section"
```

接著再加入以下內容，然後 commit：

```html
<!-- 最新消息 -->
<section class="news">
  <p>v2.0 即將上線，敬請期待！</p>
</section>
```

```bash
git add src/index.html
git commit -m "feat: add news section"
```

### 6. Push 所有 branch 到 GitHub

```bash
git remote add origin <your-repo-url>
git push -u origin --all
```
