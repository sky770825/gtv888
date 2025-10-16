# 全球商聯會 Landing Page

## 📖 專案說明

這是一個專為**全球商聯會**設計的專業紓困服務 Landing Page，採用現代化響應式設計，完美適配所有設備。

## ✨ 主要特色

### 🎨 設計特點
- ✅ **100% 響應式設計** - 從手機到 4K 顯示器完美適配
- ✅ **移動優先** - Mobile-First 設計理念
- ✅ **流暢動畫** - 平滑的滾動和過渡效果
- ✅ **現代化 UI** - 符合 2025 年設計趨勢
- ✅ **無障礙訪問** - 支援螢幕閱讀器和鍵盤導航

### 🛠️ 技術規格
- **HTML5** - 語義化標籤結構
- **CSS3** - Flexbox、Grid、媒體查詢、CSS 變數
- **JavaScript** - 原生 ES6+（無框架依賴）
- **字體** - Google Fonts (Noto Sans TC)
- **圖標** - Font Awesome 6.4.0

### 📱 響應式斷點
```
手機：< 768px
平板：768px - 1024px
桌面：> 1024px
大螢幕：> 1440px
```

## 📂 檔案結構

```
專案資料夾/
├── index.html              # 主頁面（包含所有 HTML、CSS、JS）
├── README.md               # 本說明文件
├── 工作流程記錄.md         # 專案開發流程記錄
└── 內容收集.md             # 內容收集文檔
```

## 🚀 使用方式

### 方法一：直接開啟
1. 雙擊 `index.html` 文件
2. 將在預設瀏覽器中開啟

### 方法二：本地伺服器（推薦）
使用 VS Code Live Server 或其他本地伺服器：
```bash
# 使用 Python
python -m http.server 8000

# 使用 Node.js
npx http-server
```

### 方法三：部署到網站
將 `index.html` 上傳到任何網頁託管服務：
- GitHub Pages
- Netlify
- Vercel
- 自己的伺服器

## 📋 頁面區塊說明

### 1. 導航欄（Navigation）
- 固定置頂設計
- 滾動時添加陰影效果
- 手機版自動轉換為漢堡選單
- 包含：首頁、服務介紹、準備資料、申請流程、服務優勢、聯絡我們

### 2. 英雄區（Hero Section）
- 全螢幕高度設計
- 漸層背景 + 動態效果
- 主標題、副標題、描述文字
- 雙 CTA 按鈕（立即諮詢、了解更多）

### 3. 服務類型（Services）
- 兩大服務：個人紓困、企業紓困
- 卡片式設計，hover 動畫效果
- 桌面 2 欄、平板 2 欄、手機 1 欄

### 4. 準備資料（Requirements）
- **個人紓困準備資料**（9 項）
- **企業紓困準備資料**（7 項）
- 互動式列表，hover 顯示強調效果
- 溫馨提醒區塊

### 5. 申請流程（Process）
- 四步驟流程說明
- 數字標示清晰
- 漸層背景設計
- 桌面 4 欄、平板 2 欄、手機 1 欄

### 6. 服務優勢（Features）
- 六大優勢特色
- 圖標 + 標題 + 說明
- 3 欄網格佈局（響應式調整）

### 7. 聯絡我們（Contact）
- 電話、Line、Email 聯絡方式
- 營業時間資訊
- 漸層卡片設計

### 8. 頁尾（Footer）
- Logo + 簡介
- 快速導航連結
- 版權聲明

## 🎨 自訂修改指南

### 修改顏色
在 CSS `:root` 區塊中修改顏色變數：

```css
:root {
    --primary-color: #1e3a8a;      /* 主色調 */
    --secondary-color: #f59e0b;    /* 次要色 */
    --accent-color: #10b981;       /* 強調色 */
}
```

### 修改文字內容
直接在 HTML 中搜尋並修改對應文字。

### 修改聯絡資訊
找到 `<section class="contact">` 區塊：
```html
<p><a href="tel:0900000000">0900-000-000</a></p>  <!-- 修改電話 -->
<p><a href="mailto:service@example.com">service@example.com</a></p>  <!-- 修改 Email -->
```

### 修改準備資料清單
找到 `<section class="requirements">` 區塊，修改 `<li>` 項目。

### 添加 Logo
在導航欄的 `.logo` 區塊中添加圖片：
```html
<a href="#" class="logo">
    <img src="your-logo.png" alt="Logo" style="height: 40px;">
    全球商聯會
</a>
```

## 📱 響應式測試

### 推薦測試設備/尺寸
- **手機**：iPhone SE (375px)、iPhone 12 Pro (390px)、Galaxy S20 (360px)
- **平板**：iPad (768px)、iPad Pro (1024px)
- **桌面**：1366px、1920px、2560px

### Chrome DevTools 測試
1. 按 `F12` 開啟開發者工具
2. 點擊「切換設備工具欄」圖標（或按 `Ctrl+Shift+M`）
3. 選擇不同設備進行測試

## 🌐 瀏覽器兼容性

### 完全支援
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

### 基本支援
- ⚠️ IE 11（部分新特性不支援）

## ⚡ 性能優化

### 已實施的優化
1. **CSS 變數** - 減少重複代碼
2. **懶加載觀察者** - 滾動動畫優化
3. **Font Awesome CDN** - 圖標按需載入
4. **Google Fonts** - 字體優化載入
5. **媒體查詢優化** - 減少不必要的樣式計算

### 進一步優化建議
1. **圖片優化** - 使用 WebP 格式
2. **代碼壓縮** - 使用 CSS/JS 壓縮工具
3. **CDN 部署** - 使用 CDN 加速資源載入

## 🔧 常見問題

### Q: 如何修改導航欄 Logo？
A: 在 HTML 中找到 `<a href="#" class="logo">` 區塊，將文字替換為 `<img>` 標籤。

### Q: 手機選單無法開啟？
A: 確保 JavaScript 代碼正確載入，檢查瀏覽器控制台是否有錯誤訊息。

### Q: 如何添加更多服務項目？
A: 複製 `.service-card` 區塊，修改內容即可。Grid 佈局會自動調整。

### Q: 如何更改字體？
A: 修改 Google Fonts 連結和 CSS 中的 `font-family` 屬性。

### Q: 如何添加背景圖片？
A: 在英雄區（`.hero`）的 CSS 中添加：
```css
.hero {
    background-image: url('your-image.jpg');
    background-size: cover;
    background-position: center;
}
```

## 📞 技術支援

如有任何問題或需要協助，請聯絡開發團隊。

## 📝 更新日誌

### v1.0.0 (2025-10-16)
- ✅ 初始版本發布
- ✅ 完整響應式設計
- ✅ 個人與企業紓困準備資料
- ✅ 六大服務優勢
- ✅ 四步驟申請流程
- ✅ 聯絡資訊區塊
- ✅ 手機選單功能
- ✅ 平滑滾動效果
- ✅ 滾動動畫

## 📜 授權

© 2025 全球商聯會 All Rights Reserved.

---

**製作日期**: 2025-10-16  
**版本**: 1.0.0  
**技術**: HTML5 + CSS3 + JavaScript ES6+
