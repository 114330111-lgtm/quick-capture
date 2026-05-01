# 💡 個人工具集 (Quick Capture Suite) — 專案紀錄

## 專案簡介
一組可安裝到手機桌面的個人工具，全部使用 Firebase Firestore 即時同步（電腦 ↔ 手機）。
統一部署在同一個 GitHub Pages Repo 與 Firebase 專案下。

## 線上網址總覽
| 工具 | 網址 |
|------|------|
| 💡 快速靈感捕捉 | https://114330111-lgtm.github.io/quick-capture/ |
| 🍽️ 美食筆記 | https://114330111-lgtm.github.io/quick-capture/restaurant.html |
| 🛍️ 購物清單 | https://114330111-lgtm.github.io/quick-capture/wantlist.html |

- **GitHub Repo**：https://github.com/114330111-lgtm/quick-capture.git
- **Branch**：master

## 本機檔案位置
```
C:\Users\lenny\Documents\quick-capture\
├── index.html        # 💡 快速靈感捕捉（主程式）
├── restaurant.html   # 🍽️ 美食筆記
├── wantlist.html     # 🛍️ 購物清單
├── sw.js             # Service Worker（v3，永遠從網路取得）
├── manifest.json     # PWA manifest
├── icon.svg          # App icon
└── CLAUDE.md         # 本記錄檔
```

## Firebase 設定（三個工具共用同一個 Firebase 專案）
- **Project ID**：quick-capture-6f954
- **資料庫**：Cloud Firestore（asia-east1）
- **安全規則**：`allow read, write: if request.time < timestamp.date(2026, 5, 30);`
- **Firestore 集合**：
  - `ideas`（快速靈感捕捉）
  - `restaurants`（美食筆記）
  - `wantlist`（購物清單）

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

## 各工具功能說明

### 💡 快速靈感捕捉（index.html）
- 輸入想法並儲存（Ctrl+Enter）
- 自動偵測標籤 + 下拉選單手動覆蓋
- 10 個分類：待辦 ✅、靈感 💡、Podcast 🎙、研究 🔬、AI工具 🤖、日常 🌅、工作 💼、學習 📚、財務 💰、其他 📦
- 搜尋、標籤篩選、編輯、刪除、匯出 TXT

### 🍽️ 美食筆記（restaurant.html）
- 記錄餐廳（想吃 / 已吃 / 推薦）
- 城市、標籤、評分、價格、Google Maps 連結
- 列表 / 地圖雙檢視、搜尋篩選
- ⚠️ 照片僅存本機，不同步至 Firestore（base64 太大）

### 🛍️ 購物清單（wantlist.html）
- 記錄想入手的物品（必買 / 考慮 / 等特價 / 已入手 / 放棄）
- 品牌、國別、類別、尺寸、顏色、商品連結
- 價格歷史追蹤（可記錄多次價格變動）
- ⚠️ 照片僅存本機，不同步至 Firestore

## 已知注意事項
- **部署方式**：直接 `git push origin master`，GitHub Pages 自動更新（約 1-3 分鐘）
- **更新後需強制重整**：瀏覽器按 `Ctrl+Shift+R` 清除 Service Worker 快取
- **Service Worker 策略**：永遠從網路取得（sw.js v3），不做本地快取
- **Firestore 查詢**：不用 `orderBy`（避免索引問題），改在 JS 裡排序
- **不用 offline persistence**：直接 `getFirestore(app)`，確保即時同步
- **Firebase 安全規則到期**：2026/5/30，到期前需至 Firebase Console 更新規則

## 常用指令
```bash
# 進入專案目錄
cd "C:/Users/lenny/Documents/quick-capture"

# 推送更新（單一檔案）
git add index.html && git commit -m "說明" && git push origin master

# 推送更新（多個檔案）
git add . && git commit -m "說明" && git push origin master

# 查看狀態
git log --oneline -5
git status
```
