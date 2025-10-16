# Google Sheets 欄位設定指南

## 📊 表格欄位配置

請在 Google Spreadsheet 中建立以下欄位（第一行作為標題行）：

### 完整欄位列表

| 欄位英文名 | 欄位中文名 | 資料類型 | 說明 |
|-----------|-----------|---------|------|
| A - 時間戳記 | 時間戳記 | 日期時間 | 自動記錄提交時間 |
| B - 姓名 | 姓名 | 文字 | 申請人姓名（必填） |
| C - 出生年月日 | 出生年月日 | 日期 | 申請人生日（必填） |
| D - 性別 | 性別 | 文字 | 男/女（必填） |
| E - 連絡電話 | 連絡電話 | 文字 | 聯絡電話號碼（必填） |
| F - 店家名稱 | 店家名稱 | 文字 | 商家名稱（選填） |
| G - LINE ID | LINE ID | 文字 | LINE 帳號（選填） |
| H - 通訊地址 | 通訊地址 | 文字 | 完整通訊地址（必填） |
| I - 資訊來源 | 資訊來源 | 文字 | 得知管道（必填） |
| J - 介紹人名稱 | 介紹人名稱 | 文字 | 推薦人姓名（選填） |
| K - 匯款後四碼 | 匯款後四碼 | 文字 | 匯款帳號後四碼（必填） |

---

## 🎯 第一行標題設定（複製貼上）

```
時間戳記	姓名	出生年月日	性別	連絡電話	店家名稱	LINE ID	通訊地址	資訊來源	介紹人名稱	匯款後四碼
```

---

## 📝 Google Apps Script 設定步驟

### 步驟 1：開啟 Google Sheets
1. 前往您的 Google Spreadsheet：
   https://docs.google.com/spreadsheets/d/1KoNX9OIFi0GW0lWAH6T1pgVa1CiW35YOyRXhkknR_Zs/edit

2. 在第一行（Row 1）建立上述欄位標題

### 步驟 2：創建 Apps Script
1. 點擊 **擴充功能** → **Apps Script**
2. 刪除預設代碼
3. 貼上以下代碼：

```javascript
function doPost(e) {
  try {
    // 獲取活動試算表
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    
    // 解析接收到的數據
    const data = JSON.parse(e.postData.contents);
    
    // 準備要寫入的行數據
    const row = [
      data.timestamp || new Date().toISOString(),  // 時間戳記
      data.name || '',                              // 姓名
      data.birthdate || '',                         // 出生年月日
      data.gender || '',                            // 性別
      data.phone || '',                             // 連絡電話
      data.storeName || '',                         // 店家名稱
      data.lineId || '',                            // LINE ID
      data.address || '',                           // 通訊地址
      data.source || '',                            // 資訊來源
      data.referrer || '',                          // 介紹人名稱
      data.paymentCode || ''                        // 匯款後四碼
    ];
    
    // 將數據附加到試算表
    sheet.appendRow(row);
    
    // 返回成功響應
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'success', 'row': row }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // 返回錯誤響應
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'error', 'error': error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

// 測試函數
function test() {
  const testData = {
    timestamp: new Date().toISOString(),
    name: "測試姓名",
    birthdate: "1990-01-01",
    gender: "男",
    phone: "0912345678",
    storeName: "測試店家",
    lineId: "testline",
    address: "台北市測試路123號",
    source: "網站資料",
    referrer: "測試介紹人",
    paymentCode: "1234"
  };
  
  doPost({
    postData: {
      contents: JSON.stringify(testData)
    }
  });
}
```

### 步驟 3：部署 Web App
1. 點擊 **部署** → **新增部署作業**
2. 選擇類型：**網頁應用程式**
3. 設定如下：
   - **說明**：全球商聯會店家申請表單
   - **執行身分**：我
   - **具有存取權的使用者**：任何人
4. 點擊 **部署**
5. **複製 Web App URL**（重要！）

### 步驟 4：更新網頁代碼
在 `charity-merchant-program.html` 中找到這段代碼：

```javascript
const scriptURL = 'YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL';
```

替換為您的實際 Web App URL，例如：
```javascript
const scriptURL = 'https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec';
```

並取消註釋這行：
```javascript
// sendToGoogleSheets(formData);
```
改為：
```javascript
sendToGoogleSheets(formData);
```

---

## ✅ 測試步驟

1. 在 Apps Script 中運行 `test()` 函數，確認數據能正確寫入
2. 在網頁上填寫表單並提交
3. 檢查 Google Sheets 是否收到新數據

---

## 🔒 安全性建議

1. **定期備份**：設定 Google Sheets 自動備份
2. **權限控制**：確保只有授權人員能編輯試算表
3. **數據驗證**：在試算表中設定數據驗證規則
4. **通知設定**：設定新數據提交時的電子郵件通知

---

## 📧 Email 通知設定（可選）

在 Apps Script 中添加以下代碼以發送郵件通知：

```javascript
function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    const data = JSON.parse(e.postData.contents);
    
    const row = [
      data.timestamp || new Date().toISOString(),
      data.name || '',
      data.birthdate || '',
      data.gender || '',
      data.phone || '',
      data.storeName || '',
      data.lineId || '',
      data.address || '',
      data.source || '',
      data.referrer || '',
      data.paymentCode || ''
    ];
    
    sheet.appendRow(row);
    
    // 發送郵件通知
    const recipient = 'your-email@example.com'; // 替換為您的郵箱
    const subject = '新的店家申請 - ' + data.name;
    const body = `
收到新的店家申請：

姓名：${data.name}
電話：${data.phone}
店家名稱：${data.storeName || '未填寫'}
地址：${data.address}
資訊來源：${data.source}
介紹人：${data.referrer || '無'}
匯款後四碼：${data.paymentCode}

申請時間：${data.timestamp}
    `;
    
    MailApp.sendEmail(recipient, subject, body);
    
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'success' }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'error', 'error': error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

---

## 📊 數據分析建議

在 Google Sheets 中可以添加以下分析欄位：

### 額外分析欄位（L-P 欄）

| 欄位 | 名稱 | 公式範例 |
|-----|------|---------|
| L | 年齡 | `=DATEDIF(C2,TODAY(),"Y")` |
| M | 申請月份 | `=TEXT(A2,"YYYY-MM")` |
| N | 狀態 | 手動填寫（待審核/已聯繫/已完成） |
| O | 備註 | 手動填寫 |
| P | 負責人 | 手動填寫 |

---

## 🎨 表格美化建議

1. **凍結首行**：檢視 → 凍結 → 1 列
2. **設定篩選器**：資料 → 建立篩選器
3. **條件格式**：
   - 必填欄位如果空白則標紅
   - 新申請（24小時內）標黃
4. **資料驗證**：
   - 性別欄位限制為「男」或「女」
   - 電話欄位限制為數字格式
   - 匯款後四碼限制為4位數字

---

## 📞 技術支援

如有任何問題，請聯繫：
- 北區秘書長：孫偉騰
- 電話：0989-422-478

---

**建立日期**：2025年  
**最後更新**：2025年

