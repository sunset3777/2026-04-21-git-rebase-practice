# 情境 06 — 團隊協作：功能分支的同步藝術

## 🎬 情境描述

在專業團隊中，我們通常會由一個「大功能分支（Base Branch）」出發。
例如：團隊正在開發 `feature/shop` (商店系統)，而你負責其中的 `feature/cart` (購物車功能)。

當你在寫購物車時，夥伴已經先把商店系統的基礎代碼更新到 `feature/shop` 了。
為了避免最後合併時發生巨大衝突，你必須定期將你的分支 **Rebase** 到大功能分支之上。

---

## 🎯 你的任務

### 階段 A — 更新你的分支基底 (Sync with Base)

將你的 `feature/cart` 分支「墊」在最新的 `feature/shop` 之上。

<details>
<summary>想一下再看</summary>

雖然可以用 `git merge`，但在開發分支中，我們更傾向使用 `git rebase`。
這會讓你的購物車功能看起來像是「基於最新的商店系統」開發的，保持歷史紀錄是一條直線。

</details>

<details>
<summary>指令提示</summary>

```bash
# 確保你在自己的小分支
git checkout feature/cart

# 把大功能分支的變更領進來，接在你的 commit 之前
git rebase feature/shop
```

</details>

**✅ 完成條件：** 輸入 `git log --oneline --graph`，確認你的 commit 已經排在 `feature/shop` 的最新進度之上。

---

### 階段 B — 處理跨分支衝突 (Conflict)

如果在 Rebase 過程中，你跟夥伴剛好改到了同一個檔案的同一行。

1. Git 會停下來並顯示 `CONFLICT`。
2. 手動打開檔案處理衝突。
3. 執行以下指令：
   ```bash
   git add <衝突的檔案>
   git rebase --continue
   ```

**✅ 完成條件：** 成功解決衝突並完成同步。

---

## 🧠 觀念筆記

| 指令 | 效果 |
|---|---|
| `git rebase [base-branch]` | 把當前分支的起點，移到目標分支的最前端 |

> **開發者的金律**
> 在自己的功能分支尚未合併回主線前，**「勤於 Rebase 主線」**。
> 這樣可以把衝突化整為零，避免在最後 PR 時才一次處理累積了一個月的巨大衝突。
