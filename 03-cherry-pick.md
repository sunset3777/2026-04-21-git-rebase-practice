# 情境 03 — git cherry-pick：只想要那一個 commit

## 🎬 情境描述

你和協作者各自在不同的 branch 上開發。

協作者在 `feature-partner` branch 上，修好了 `src/index.html` 裡 header 標題的 bug，  
打開 VS Code，切換到 `feature-partner` branch，查看 commit 歷史：

```
fix: typo in footer
fix: header title in index.html  ← 你只想要這個！
wip: add subtitle to header
init partner feature
```

> 💡 **如何複製 commit hash？**  
> 在 VS Code 的 Timeline 中點選該 commit，右鍵選擇 **Copy Commit ID** 取得 hash。

你的 `main` branch 也有同樣的 header 標題問題，  
但你**不想把協作者整個 branch merge 進來**，只想把那一個修 bug 的 commit 帶過來。

---

## 🎯 你的任務

這個情境分兩個階段：

---

### 階段 A — cherry-pick 單筆 commit

從 VS Code 複製 `fix: header title in index.html` 的 hash，然後執行：

<details>
<summary>想一下再看</summary>

有個指令可以「摘取」某個 commit，把它的變更套用到目前的 branch，  
而不需要 merge 整個 branch。

</details>

<details>
<summary>指令提示</summary>

```bash
git checkout main
git cherry-pick <你複製的 hash>
```

</details>

**✅ 完成條件：** `git log --oneline` 在 `main` 上可以看到一個內容相同的新 commit。

---

### 階段 B — cherry-pick 區間（hash^..hash）

這次情境升級：協作者連續做了兩個相關的 commit，你兩個都想要：

```
fix: typo in footer
fix: header title in index.html  ← 想要
wip: add subtitle to header     ← 也想要
init partner feature
```

從 VS Code 分別複製 `wip: add subtitle to header` 和 `fix: header title in index.html` 的 hash，然後執行：

<details>
<summary>想一下再看</summary>

`cherry-pick` 支援區間語法：`A^..B` 代表「從 A 開始（含 A）到 B 為止」。  
注意 `^` 是讓範圍**包含**起點的關鍵。

</details>

<details>
<summary>指令提示</summary>

```bash
git cherry-pick <WIP commit 的 hash>^..<fix header 的 hash>
```

</details>

**✅ 完成條件：** `git log --oneline` 在 `main` 上依序出現這兩個 commit 的內容。

---

## 🧠 觀念筆記

| 語法 | 說明 |
|---|---|
| `git cherry-pick <hash>` | 複製單筆 commit 到目前 branch |
| `git cherry-pick A^..B` | 複製 A 到 B 的區間（含 A 和 B） |
| `git cherry-pick A..B` | 複製 A 到 B 的區間（**不含** A） |

> **cherry-pick 會產生新的 commit hash**  
> 內容一樣，但 hash 不同——因為它是一個全新的 commit，只是變更內容相同。

> **什麼時候用 cherry-pick？**  
> - 不想整個 branch merge，只需要特定修改時
> - hotfix 做在錯的 branch，需要移植到 main 時
> - 協作者的某個 commit 剛好解決了你的問題

---

## ➡️ 完成後

前往 [情境 04 — git push --force](./04-force-push.md)
