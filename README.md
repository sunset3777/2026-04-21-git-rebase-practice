# 🧪 Git 實戰練習場

歡迎來到這個練習 repo！  
這裡準備了四個真實開發情境，讓你親手操作、親眼看見每個 Git 指令的效果。


---

## 🗺️ 情境地圖

| # | 情境 | 學習指令 | 難度 |
|---|---|---|---|
| 01 | [工作做到一半，任務來了](./01-stash.md) | `git stash` | ⭐ |
| 02 | [commit 錯了，怎麼辦？](./02-reset.md) | `git reset` | ⭐⭐ |
| 03 | [只想要那一個 commit](./03-cherry-pick.md) | `git cherry-pick` | ⭐⭐⭐ |
| 04 | [推送被拒絕了](./04-force-push.md) | `git push --force` | ⭐⭐⭐ |
| 05 | [讓 commit 歷史變漂亮](./05-rebase.md) | `git rebase` | ⭐⭐⭐⭐ |
| 06 | [多人同步開發生存法則](./06-sync-dev.md) | `git pull --rebase` | ⭐⭐⭐⭐ |
| 07 | [Approve 機制與審核](./07-review.md) | PR / Code Review | ⭐⭐ |

建議依序完成，每個情境都會用到前面建立的觀念。

---

## 🚀 開始之前

### 1. Clone 這個 repo

```bash
git clone https://github.com/study-rocket-coding/2026-04-21-git-practice
cd 2026-04-21-git-practice
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
2026-04-21-git-practice/
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

- 先試著自己查 `git status` 和 `git log --online`，通常能找到線索。
- 真的卡住了再找協作者討論。
- 任何操作都可以還原——除了 `reset --hard` 和 `force push` 之後要特別小心。

---

## ✍️ 完成後

所有情境走完之後，請依照任務規格的格式撰寫學習反思，並回覆在 Issue 下方。
Update on main
