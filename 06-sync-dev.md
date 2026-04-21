# 情境 06 — 同步開發：多人同分支的生存法則

## 🎬 情境描述

團隊決定在 `feature-shared` 這個分支上共同開發一個大功能。
你剛剛寫好了一段程式碼準備 push，卻發現夥伴 A 搶先一步 push 了！

此時如果你直接 `git pull`，Git 會自動幫你做一個 merge，產生一條多餘的線。
我們要練習如何優雅地同步。

---

## 🎯 你的任務

### 階段 A — 使用 Pull Rebase 同步

當遠端有新東西，而你本地也有新 commit 時。

<details>
<summary>想一下再看</summary>

一般 `git pull` 會產生一條交叉線。使用 `--rebase` 參數可以讓你的本地變更「排隊」在遠端變更之後。

</details>

<details>
<summary>指令提示</summary>

```bash
# 不要只用 git pull，改用 rebase 模式
git pull --rebase origin feature-shared
```
這會先把你的本地 commit 「拔起來」，把遠端的新 commit 接上，再把你的 commit 放回去。

</details>

**✅ 完成條件：** 成功同步，且 `git log` 顯示你的 commit 在夥伴的 commit 之後。

---

### 階段 B — 處理同分支衝突 (Conflict)

你跟夥伴同時改了 `index.html` 的同一行。

1. 修改 `index.html` 並 commit。
2. 嘗試 `git pull --rebase`，你會看到 `CONFLICT (content): Merge conflict in index.html`。
3. 手動打開檔案處理衝突（選擇保留哪一邊，或兩者都要）。
4. 執行以下指令：
   ```bash
   git add index.html
   git rebase --continue
   ```

**✅ 完成條件：** 成功解決衝突並完成同步。

---

## 🧠 觀念筆記

| 模式 | 效果 |
|---|---|
| `git pull` | 等於 fetch + merge (容易產生雜亂 commit) |
| `git pull --rebase` | 等於 fetch + rebase (保持歷史線性) |

> **團隊共識**
> 在多人開發同一個分支時，建議養成 `git pull --rebase` 的習慣，這樣可以避免分支圖變成「麻花捲」。
