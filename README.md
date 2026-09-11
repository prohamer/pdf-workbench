# PDF 工作台（PDF Workbench）

純前端、單頁的 PDF 編輯工具。所有處理都在瀏覽器本機完成，**檔案不會上傳到任何伺服器**。
本版本已將相依函式庫一併打包在 `vendor/`，可完全離線使用，不依賴外部 CDN。

## 功能

- 開啟 / 合併多個 PDF（一次選多檔即依序合併）
- 頁面縮圖瀏覽、縮放、符合寬度
- 拖曳排序、刪除頁面、單頁或批次旋轉
- 插入空白頁（可選插入到文件最前 / 本頁之後 / 文件最後）
- 頁碼：可針對全部或勾選頁面套用，支援前綴／後綴、起始頁碼、章節格式（如 `1-1`）、顯示總數、位置與字級
- 繪圖標註：畫筆（可線上簽名）、螢光筆、直線、箭頭、方框、文字、橡皮擦
- 復原 / 重作（涵蓋頁面增刪、移動、旋轉、頁碼、標註）
- 版面合併（N-up）：例如將 2 張 A4 合成 1 張 A3
- 下載全部 / 下載勾選頁面
- 匯出頁面為 PNG 圖片

## 使用方式

直接開啟 `index.html` 即可（需與 `vendor/` 資料夾放在一起）。

> 注意：`index.html` 依賴同目錄下的 `vendor/` 檔案，請勿單獨搬移 `index.html`。

## 發佈到 GitHub Pages

1. 建立一個 repository（免費方案需為 Public），將整個資料夾內容上傳（保留 `index.html` 與 `vendor/` 的相對位置）。
2. 進入 repo 的 **Settings → Pages**，Source 選「Deploy from a branch」，Branch 選 `main`、資料夾 `/(root)`，儲存。
3. 等待一到兩分鐘，網址格式為 `https://你的帳號.github.io/repo名稱/`。

## 技術說明

- 渲染：[PDF.js](https://github.com/mozilla/pdf.js)（Apache-2.0）
- 編修與輸出：[pdf-lib](https://github.com/Hopding/pdf-lib)（MIT）
- 兩者授權條款置於 `LICENSES/`。

### 幾點行為說明

- 繪圖標註、頁碼、N-up 於輸出時會壓平成一層圖層蓋在頁面上，原頁面文字仍保留；下載後標註即固定，無法再回頭編輯（一般標註工具的標準做法）。
- 頁碼一旦套用即固定於各頁，之後重新排序不會自動重編；如需更新，重新框選並再套用一次即可。
- 加密的 PDF 可能無法讀取或輸出。

## 更新函式庫

`vendor/` 內的檔案取自對應版本的 npm 套件：

- `pdfjs-dist@3.11.174` → `build/pdf.min.js`、`build/pdf.worker.min.js`
- `pdf-lib@1.17.1` → `dist/pdf-lib.min.js`

若要升級，取得新版對應檔案替換即可（升級 PDF.js 時 `pdf.min.js` 與 `pdf.worker.min.js` 版本需一致）。

## 隱私

本工具不含任何分析、追蹤或外部請求；打開網頁後即使斷網也能運作。
