# 情境 02 — git reset：commit 錯了，怎麼辦？

## 🎬 情境描述

你在 `hotfix-bad-commits` branch 上，剛剛做了幾個 commit。  
打開 VS Code，點選左側的 **Source Control 圖示（Ctrl+Shift+G）**，  
再點選右上角的時鐘圖示（**View Git Graph** 或 **Timeline**）查看 commit 歷史。

你會看到類似這樣的紀錄：

```
chore: add test data in index.html  ← 這個不該 commit！
fix: update footer year
chore: init project
```

你發現最新的 commit 把一段測試用的假資料也一起提交了，  
這不應該出現在正式記錄裡。

> 💡 **如何複製 commit hash？**  
> 在 VS Code 的 Timeline 或 Git Graph 中，點選該 commit，  
> 右鍵選擇 **Copy Commit ID** 即可取得完整 hash。

---

## 🎯 你的任務

這個情境分三個階段，請依序完成：

---

### 階段 A — git reset HEAD（把檔案從暫存區退出）

你修改了 `src/index.html`，然後不小心 `git add` 了，但還沒 commit。  
你想把它從暫存區退出來（保留檔案修改）。

<details>
<summary>想一下再看</summary>

`git add` 之後、`git commit` 之前，檔案會在「暫存區」。  
有個指令可以把它退回「工作區」，但不影響檔案內容。

</details>

<details>
<summary>指令提示</summary>

```bash
git reset HEAD src/index.html
# 或 Git 新版語法：
git restore --staged src/index.html
```

</details>

**✅ 完成條件：** `git status` 顯示 `src/index.html` 回到 `Changes not staged`。

---

### 階段 B — git reset hash（回退到指定 commit，保留變更）

你想撤銷最新那個 commit（`chore: add test data in index.html`），  
但**保留**那次修改的檔案內容（讓它回到工作區）。

先從 VS Code 複製 `fix: update footer year` 這個 commit 的 hash，再執行：

<details>
<summary>想一下再看</summary>

`git reset` 可以指定一個 commit hash，讓 HEAD 移回那個位置。  
預設模式（`--mixed`）會把被撤銷的 commit 內容退回工作區。

</details>

<details>
<summary>指令提示</summary>

```bash
git reset <你複製的 hash>
```

</details>

**✅ 完成條件：** VS Code 的 commit 歷史不再出現 `chore: add test data`，但 `git status` 可以看到那次的修改還在。

---

### 階段 C — git reset --hard（回退並完全丟棄變更）

這次你確定那個 commit 的內容完全不要了，  
想要**乾淨地**回到 `fix: update footer year`，連檔案修改都一起丟掉。

> ⚠️ **注意：這個操作不可逆。** 丟掉的變更無法透過一般方式找回。

一樣從 VS Code 複製 `fix: update footer year` 的 hash，再執行：

<details>
<summary>想一下再看</summary>

加上 `--hard` 參數，會讓工作區和暫存區都跟著 reset 到指定的 commit 狀態。

</details>

<details>
<summary>指令提示</summary>

```bash
git reset --hard <你複製的 hash>
```

</details>

**✅ 完成條件：** VS Code 的 commit 歷史不再出現 `chore: add test data`，且工作區乾淨無任何變更。

---

## 🧠 觀念筆記

| 指令 | 暫存區 | 工作區檔案 | 說明 |
|---|---|---|---|
| `git reset HEAD <file>` | ✅ 退出 | 不變 | 把特定檔案從暫存區退回工作區 |
| `git reset <hash>` | 清空 | 保留變更 | 回退 commit，修改退回工作區 |
| `git reset --hard <hash>` | 清空 | ❌ 丟棄 | 完全回到指定 commit 的狀態 |

> **什麼時候用哪個？**
> - 只是 `add` 錯了 → `reset HEAD`
> - commit 錯了但內容還有用 → `reset hash`
> - commit 錯了且內容完全不要 → `reset --hard`（用前三思）

---

## ➡️ 完成後

前往 [情境 03 — git cherry-pick](./03-cherry-pick.md)
