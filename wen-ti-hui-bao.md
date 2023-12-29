# 🆘 問題回報

### 將專案 clone 下來後，下指令 npm run serve 嘗試執行專案，但無法運作。

> 還是建議依照 repo 中 README.md 步驟實做。
>
> OR
>
> 專案 clone 下來後，請依循以下步驟：
>
> * 確認環境
> * npm install
> * 根據 package.json 內的 script 定義來啟動專案，如 vite 預設為 "dev"，故指令下 npm run dev

### 如何打包？有需要什麼設定？

> 首先要先確認打包事項，例如：mode: production、stage？
>
>
>
> 根據 package.json 內的 script 定義來打包專案，template 中定義兩種 build，分別是 "build" 與 "build:stage"，區別在於打包時，會根據指定的 mode 對應到不同的環境變數以區別不同環境下的程式碼。
>
>
>
> 執行完後，有看到多一個 dist 檔就可以了，提供內容資料以發布應用程式。

### 部屬完成後，但畫面一片白是什麼問題？

> 接下來的說明與 vite.config.js 其中的 base 的關聯：
>
> 假設我要部署的 Server ip 位置在 http://10.xx.xx.xx/，base 可以設定為 "/"。
>
> 假設我要部署的 Server ip 位置在 http://10.xx.xx.xx/VUE/ABC，base 應當要設定為 "/VUE/ABC/"。
>
> 其中，base 關聯到的變數為 環境變數中的 VITE\_BASE\_PUBLIC\_PATH，故從打包到部屬的過程中，都應當要確認好需求。

### 部屬完成後，有畫面了，但圖片出不來？

> 1. 首先先確認 build 出來的 dist 是否有該圖片
> 2. 確認檔案是否有在部屬的過程中遺失
> 3. 透過 DevTools > Element 檢視沒有跑出來的圖片其路徑
> 4. 透過該路徑檢視 DevTools > Source 是否有下載到
> 5. 檢視 DevTools > Networks 確認圖片檔案的下載
>
>
>
> 明明 Request 的項目為 SVG 但 Response Header 的 Content-Type 卻是 text/plain

<figure><img src=".gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

確認 Response Server 的 mime.types 中是否有 image/svg+xml，，以下示範 Nginx 及 Apache：

<figure><img src=".gitbook/assets/image (82).png" alt=""><figcaption><p>Nginx</p></figcaption></figure>

<div data-full-width="true">

<figure><img src=".gitbook/assets/image (81).png" alt=""><figcaption><p>Apache</p></figcaption></figure>

</div>
