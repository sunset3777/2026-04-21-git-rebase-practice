# 情境 05 — git rebase：讓 commit 歷史變漂亮

## 🎬 情境描述

你在 `feature-your-name` 分支上開發了兩天，期間為了怕弄丟程式碼，你推了幾個標題很爛的 commit（例如：`fixed typo`, `debug again`, `test`）。

同時，你的夥伴已經把 `main` 分支更新了，現在你的分支落後於 `main`。如果你現在直接 merge，會產生一個雜亂的「Merge branch 'main' into ...」紀錄。

你的目標是：
1. 把那幾個爛 commit 合併成一個有意義的 commit。
2. 把你的分支「接」在最新的 `main` 後面。

---

## 🎯 你的任務

### 階段 A — 互動式 Rebase (Squash)

將最近的 3 個 commit 合併成一個。

<details>
<summary>想一下再看</summary>

如果你有三個 commit 想合併，你可以使用 `git rebase -i`。在打開的視窗中，把第二個之後的 `pick` 改成 `squash`，這代表「把這個 commit 塞進前一個裡面」。

</details>

<details>
<summary>指令提示</summary>

```bash
# 進入互動模式，數字 3 代表最近 3 個 commit
git rebase -i HEAD~3
```
在文字編輯器中：
1. 第一個 commit 保持 `pick`。
2. 後面的 commit 改成 `squash` (或簡寫 `s`)。
3. 儲存後，Git 會請你重新輸入一個乾淨的 commit 訊息。

</details>

**✅ 完成條件：** 使用 `git log --oneline` 檢查，原本的三個 commit 變成了一個。

---

### 階段 B — 更新分支基底 (Rebase onto main)

假設遠端 `main` 有更新，將你的開發線移到 `main` 的最新位置。

<details>
<summary>指令提示</summary>

```bash
# 先同步遠端資訊
git fetch origin

# 執行 rebase，把自己的 commit 接在 origin/main 後面
git rebase origin/main
```

</details>

**⚠️ 關鍵警告：** 如果你之前已經 push 過這個分支，rebase 完後必須使用 `git push --force-with-lease` 才能推上去。

**✅ 完成條件：** 你的 commit 歷史現在是接在 `main` 的最新 commit 之後，形成一條直線。

---

## 🧠 觀念筆記

| 指令 | 用途 |
|---|---|
| `git rebase -i` | 整理、修改、合併舊的 commit |
| `git rebase [branch]` | 重新定義分支的起點，維持線性歷史 |
| `git rebase --continue` | 解決衝突後，繼續執行 rebase |
| `git rebase --abort` | 情況不對勁，放棄 rebase 回到原狀 |

> **為什麼要用 Rebase 而不是 Merge？**
> Rebase 會讓專案歷史看起來像是一條線，沒有分支交錯的線段。這對大型專案的追蹤非常有幫助，但 **絕對不要對「已經推送到共用分支」的 commit 做 rebase**。
