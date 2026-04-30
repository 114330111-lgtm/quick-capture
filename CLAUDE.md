# 💡 快速靈感捕捉 (Quick Capture) — 專案紀錄

## 專案簡介
一個可安裝到手機桌面的 PWA，用於隨時記錄突然想到的點子或待辦事項。
支援電腦與手機即時同步（Firebase Firestore）。

## 線上網址
- **GitHub Pages（主要）**：https://114330111-lgtm.github.io/quick-capture/
- **GitHub Repo**：https://github.com/114330111-lgtm/quick-capture.git
- **Branch**：master

## 本機檔案位置
- 主程式：`C:\Users\lenny\Documents\quick-capture\index.html`
- Service Worker：`C:\Users\lenny\Documents\quick-capture\sw.js`
- Manifest：`C:\Users\lenny\Documents\quick-capture\manifest.json`
- Icon：`C:\Users\lenny\Documents\quick-capture\icon.svg`

## Firebase 設定
- **Project ID**：quick-capture-6f954
- **資料庫**：Cloud Firestore（asia-east1）
- **安全規則**：`allow read, write: if request.time < timestamp.date(2026, 5, 30);`
- **集合名稱**：`ideas`

## 資料結構（Firestore document）
```json
{
  "text": "想法內容",
  "tags": ["靈感"],
  "time": "<serverTimestamp>"
}
```

## 功能清單
- [x] 輸入想法並儲存（Ctrl+Enter 快速儲存）
- [x] 自動偵測標籤（根據關鍵字分類）
- [x] 下拉選單手動選擇/覆蓋標籤
- [x] 即時同步（電腦 ↔ 手機）
- [x] 搜尋 & 標籤篩選
- [x] 編輯 / 刪除 / 匯出 TXT
- [x] PWA 可安裝到手機桌面
- [x] 離線狀態顯示

## 標籤分類（AUTO_TAGS）
| 標籤 | Emoji | 代表關鍵字 |
|------|-------|-----------|
| 待辦 | ✅ | 記得、要做、提醒、todo |
| 靈感 | 💡 | 點子、創意、試試、突然 |
| Podcast | 🎙 | podcast、播客、節目 |
| 研究 | 🔬 | 論文、資料、分析、數據 |
| AI工具 | 🤖 | ai、gpt、claude、prompt |
| 日常 | 🌅 | 今天、心情、朋友、週末 |
| 工作 | 💼 | 會議、專案、客戶、deadline |
| 學習 | 📚 | 學、看書、課程、心得 |
| 財務 | 💰 | 錢、預算、投資、薪水 |
| 其他 | 📦 | 雜記、備忘、隨手 |

## 標籤顏色 CSS class
- tc0：紫色（#a78bfa）
- tc1：綠色（#34d399）
- tc2：橘色（#fb923c）
- tc3：粉紅（#f472b6）
- tc4：藍色（#60a5fa）
- tc5：黃色（#fbbf24）

## 已知注意事項
- **部署方式**：直接 `git push origin master`，GitHub Pages 自動更新（約 1-2 分鐘）
- **更新後需強制重整**：瀏覽器按 `Ctrl+Shift+R` 清除 Service Worker 快取
- **Service Worker 策略**：永遠從網路取得（sw.js v3），不做本地快取
- **Firestore 查詢**：不用 `orderBy`（避免索引問題），改在 JS 裡排序
- **不用 offline persistence**：直接 `getFirestore(app)`，確保即時同步

## 常用指令
```bash
# 進入專案目錄
cd "C:/Users/lenny/Documents/quick-capture"

# 推送更新
git add index.html && git commit -m "說明" && git push origin master

# 查看狀態
git log --oneline -5
git status
```
