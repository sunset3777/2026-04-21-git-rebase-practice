# 情境 07 — Approve 機制：誰說了才算？

## 🎬 情境描述

程式碼寫完了，直接 merge 進 `main` 是非常危險的。
在專業團隊中，我們會透過 **Pull Request (PR)** 或 **Merge Request (MR)** 來進行 Code Review（代碼審核）。

---

## 🎯 你的任務

### 階段 A — 發起 PR 與指定 Reviewer

這部分需要在 GitHub / GitLab 介面操作。

1. 將你的分支 push 到遠端。
2. 在網頁按下 **"Compare & pull request"**。
3. 在右側欄找到 **Reviewers**，指定你的夥伴（練習對象）。
4. 在描述欄位寫下你改了什麼。

---

### 階段 B — 模擬 Review 修改建議

如果你是**審核者 (Reviewer)**：
1. 點擊 "Files changed" 頁籤。
2. 在某行程式碼旁邊點擊 `+` 號，留下一個建議（例如：「這行變數命名可以更好」）。
3. 點擊 **"Start a review"**。
4. 最後點擊右上方 **"Finish review"**，選擇 **"Request changes"**。

如果你是**開發者**：
1. 根據建議在本地修改程式碼。
2. `git add` & `git commit`。
3. 直接 `git push`（PR 頁面會自動更新，不需重新發 PR）。

---

### 階段 C — Approve 與 Merge

1. 審核者確認修改沒問題後，點擊 **"Approve"**。
2. 觀察 PR 狀態變綠色。
3. 執行 **"Squash and merge"**（這會把整個 PR 的多個 commit 合併成一個乾淨的 commit 並進入主線）。

**✅ 完成條件：** PR 成功被合併，且 `main` 分支拿到了你的功能。

---

## 🧠 觀念筆記

- **LGTM**：Looks Good To Me (審核常用語，代表沒問題)。
- **Nitpick**：代表「這只是小建議，不改也沒關係」。
- **Branch Protection**：專案設定中可以規定「必須至少 1 人 Approve」才能合併，這是防止壞程式碼進入主線的最強防線。
