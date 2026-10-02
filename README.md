# Tokyo Journey｜東京六天五夜

手機優先的單頁 Web App，2026/11/12–11/17。

公開網址：[Tokyo Journey](https://liuyj0624.github.io/tokyo-trip-2026/)

## 操作

固定日期列與天氣／回飯店工具列；只有中間卡片區上下滑動。底部選單懸浮在卡片上方，最後一張卡片可捲到選單上方閱讀。右上 Quokka GIF 沒有超連結。

- 公開訪客可以瀏覽行程、地圖、交通與共用購物清單。
- 指定編輯者從頂部「公開瀏覽 · 登入」使用電子郵件登入連結驗證。管理員信箱由後端成員名單設定。未列入成員名單的帳號無法寫入。
- 編輯者可長按卡片直接拖移排序；鍵盤使用 Alt＋上下鍵。卡片 ⋯ 可編輯名稱、地點、時間、說明、路線、備註，複製、跨日期移動、新增或移除。
- 時間可點選修改，交通時間與地圖順序由同一份行程資料產生。
- 「整天調整時間」先預覽再套用，略過鎖定及未定時間，阻止跨日調整。
- 地圖有當日編號總覽及單站 Google Maps。總覽座標是約略位置，虛線只表示順序，不代表實際交通路線。新增地點可在編輯表單補座標；未填仍可查詢單站地圖。
- 購物清單按店家分組，可篩選未購買、加入商品照片（JPG／PNG／WebP，2 MB）。商品照片公開可見。
- 行前清單附 Visit Japan Web 入境申報、離境免稅確認入口及日本官方操作說明。
- 修改同步到雲端，其他已開啟頁面自動更新。Realtime 訂閱加上每 15 秒更新檢查；返回前景也重新讀取。
- 「修改紀錄／復原」可查看最近 20 筆舊版本並恢復。版本衝突時不自動覆蓋他人資料；可下載未送出的修改，再載入新版。

## 每個人獨立的票券

底部「票券」頁集中顯示所有日期的個人票券，支援手動新增、編輯、刪除與復原。可填寫名稱、使用日期、訂位編號、預約時間及備註，並附加 QR 圖片或 PDF（10 MB）。舊版附在行程上的票券與附件會直接出現在這個頁面。資料只放在該裝置、該網站的目前瀏覽器 IndexedDB，不會上傳 Supabase、公開分享或納入共用 JSON 備份；管理自己的票券不需要登入。

Safari、其他瀏覽器和主畫面 Web App 的儲存空間可能不同；請在平常使用的入口加入票券。清除網站資料、換手機或改用其他瀏覽器不會自動帶走票券，請自行保留原始檔。票券集中管理，不會因為行程刪除或日期切換而隱藏。

## 天氣與交通

Open-Meteo 每 15 分鐘檢查並支援手動更新。日期超出最長約 16 天預報範圍時顯示「預報未開放」，不以今日天氣冒充行程預報。交通卡片路線及時間是行程安排；即時班次與轉乘由 Google Maps 查詢，App 未串接列車即時延誤服務。

## 部署與後端

`index.html` 包含 App 程式、行程、SVG 圖示與背景，不需建置。需要 HTTPS 靜態網站及網路；Supabase JS、Leaflet、圖磚、GIF、字型及天氣由外部服務提供。

Supabase 專案 `gwbycwgdueqkzmzmuoow`：

- `trip_state` 公開唯讀；變更只透過 `save_trip` RPC。
- `trip_members` 只供管理員管理。角色由已驗證使用者信箱與成員表核對。
- `trip_history` 只供指定編輯者／管理員讀取。
- `save_trip` 鎖定資料列並核對 revision，保留前一版本。
- `trip-products` 為商品照片公開 bucket，只有編輯者可上傳。
- 沒有票券雲端資料表或票券 bucket。
- 前端只有可公開的 publishable key，沒有 service-role key、資料庫密碼或管理金鑰。

`supabase-setup.sql` 是已執行的初始設定，包含建立 policy，不可不加判斷地重跑；後續應使用 migration。

舊版 localStorage 清單不會自動公開。雲端尚未有修改，且管理員瀏覽器保有舊資料時，可在共用行程對話框選擇分享舊版改動。

## 來源

- [最終行程](https://chatgpt.com/share/6aba7b12-f318-83e8-bc6f-04c1adf26736)
- [Open-Meteo](https://open-meteo.com/en/docs)
- [Google Maps URLs](https://developers.google.com/maps/documentation/urls/get-started)
- [Visit Japan Web](https://www.vjw.digital.go.jp/)
- [日本免稅新制官方說明](https://www.mlit.go.jp/kankocho/tax-free/content/001991234.pdf)
- [Quokka GIF／Dinotaeng](https://giphy.com/stickers/dinotaeng-transparent-emoji-quokka-zPj0uudmLSYZhABim2)

門票、餐廳訂位、航班時間與開放日仍需自行確認；原行程不代表已完成預約。

