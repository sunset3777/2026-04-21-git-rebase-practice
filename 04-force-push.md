# 情境 04 — git push --force：推送被拒絕了

## 🎬 情境描述

你在 `feature-your-name` branch 上，發現剛才推送到遠端的 commit 有問題——  
`src/index.html` 裡多了一段不該出現的測試內容。

你在本地用 `git reset` 把那個 commit 撤銷了，  
然後試著推上去：

```bash
git push origin feature-your-name
```

結果看到這個錯誤：

```
 ! [rejected]        feature-your-name -> feature-your-name (non-fast-forward)
error: failed to push some refs to 'origin'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart.
```

😅 Git 拒絕了你的推送——因為你的本地歷史和遠端歷史「不一致」了。

---

## 🎯 你的任務

這個情境分兩個階段：

---

### 階段 A — 強制推送到自己的 branch

你確定這個 branch 只有你一個人在用，  
強制讓遠端歷史跟你的本地一致。

<details>
<summary>想一下再看</summary>

一般的 `git push` 要求遠端必須是本地的「祖先」才能推送。  
加上特定參數可以強制覆蓋遠端歷史——但這會讓遠端失去你覆蓋掉的 commit。

</details>

<details>
<summary>指令提示</summary>

```bash
git push --force origin feature-your-name
```

</details>

**✅ 完成條件：** 推送成功，遠端的 `feature-your-name` 歷史與本地一致。

---

### 階段 B — 在共用 branch 上嘗試 force push

現在換一個情境：你和協作者都在 `feature-shared` branch 上工作。  
協作者剛剛推了一個 commit，你也在本地做了修改並 reset 了某個 commit。

試試看對 `feature-shared` 執行 `git push --force`，觀察會發生什麼事。

> ⚠️ **這個操作會覆蓋協作者的 commit。**  
> 在這個練習環境裡這樣做沒關係——但請記住這在真實專案中可能造成嚴重問題。

<details>
<summary>觀察重點</summary>

Force push 之後：
- 協作者的 commit 從遠端消失了
- 協作者下次 `git pull` 會遇到衝突或歷史錯亂
- 如果沒有備份，那些 commit 就永遠不見了

</details>

**✅ 完成條件：** 親眼觀察到協作者的 commit 被覆蓋，並和協作者討論這個結果。

---

## 🧠 觀念筆記

| 指令 | 說明 |
|---|---|
| `git push --force` | 強制覆蓋遠端歷史 |
| `git push --force-with-lease` | 較安全的版本：若遠端有新 commit 則拒絕推送 |

> **Force Push 的黃金原則**
>
> 1. **只對自己獨用的 branch 使用** — 共用 branch（main、develop）禁止使用
> 2. **操作前先確認遠端狀態** — `git fetch` 後再決定要不要 force push
> 3. **優先考慮 `--force-with-lease`** — 比 `--force` 多一層保護，避免意外覆蓋他人的 commit
> 4. **修改已推送的歷史前，先告知協作者** — 避免對方下次 pull 時出現無法預期的錯誤

---

## 🎉 全部完成！

你已經走過所有情境，回到 [README](../README.md) 撰寫學習反思。
