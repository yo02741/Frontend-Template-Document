# vite-plugin-vue-devtools

![](https://hackmd.io/\_uploads/r1QcAhoq3.png)

透過該插件增加 DX： Developer Experience ！

***

看下來最新鮮的是 `Graph` 以及 `inspect`，至於知道那些訊息可以做什麼，估計是深度的開發才會使用到了。

而透過使用這個插件，才讓我發現 `Vue DevTools` 原來除了此功能：

![](https://hackmd.io/\_uploads/ry2Nl6o92.png)

也有這個功能能夠直接開啟該檔案：

![](https://hackmd.io/\_uploads/r18IlTi9h.png)

終於不用在的舊專案的資料夾找檔案找老半天了！

***

### 安裝

```
npm install vite-plugin-vue-devtools -D
```

```javascript
// vite.config.js
import VueDevTools from "vite-plugin-vue-devtools";

export default defineConfig({
  // ...
  plugins: [
    // ...
    VueDevTools(),
  ],
})
```

\
\


將專案 run 起來後，可以看到底下有一個漂浮工具列，如下圖：

![](https://hackmd.io/\_uploads/SJL5vjs5n.png)

### 功能介紹

#### Component Inspector

點擊右方圖示並點擊區塊，能夠快速開啟該片段的檔案。

![](https://hackmd.io/\_uploads/HJ45dis52.png)

#### Vite Plugin Vue Devtools

點擊左方 Vue 圖示能夠開啟選單

![](https://hackmd.io/\_uploads/r1oivoic3.png)

**Overview**

能夠檢視 `Vue 版本`、`路由記數`、`元件記數`

![](https://hackmd.io/\_uploads/BkTG9io5n.png)

**Pages**

能夠檢視 `當前的路徑`、`路由總覽`

![](https://hackmd.io/\_uploads/SyOC9js53.png)

雙點路由能到導向 `欲前往路徑`，該插件也提供填入參數

![](https://hackmd.io/\_uploads/Hko7oiic2.png)

**Components**

如同大家熟知的 `Vue DevTools` 能夠巢狀的檢視元件與其內容

![](https://hackmd.io/\_uploads/r1X5Tjoq2.png)

能夠透過此按鈕，直接開啟此檔案

![](https://hackmd.io/\_uploads/S1h0yno9n.png)

**Rerender Trace**

點擊錄製，並進行操作，能夠紀錄下變數的異動

![](https://hackmd.io/\_uploads/H1kCz2s9n.png)

![](https://hackmd.io/\_uploads/SJH4bhicn.png)

**Assets**

該功能能夠檢視此專案的靜態資料

![](https://hackmd.io/\_uploads/HyIVQhj92.png)

**Timeline**

跟 Vue DevTools 大同小異，且 Vue DevTools 似乎功能更全面

![](https://hackmd.io/\_uploads/HkLFX2o93.png)

**Route / Pinia**

跟 Vue DevTools 大同小異

![](https://hackmd.io/\_uploads/HkR-N2ic3.png)

![](https://hackmd.io/\_uploads/rJQ74no53.png)

**Graph**

能夠看到檔案與檔案之間的關聯

![](https://hackmd.io/\_uploads/H1MDN3j9n.png)

**inspector**

允許使用者檢查 Vite 的轉換步驟。 了解每個插件如何改變你的代碼對於發現潛在問題可能有幫助

![](https://hackmd.io/\_uploads/B1W6D2i52.png)

![](https://hackmd.io/\_uploads/SkU3F3jq3.png)

**Documentations**

能夠直接連結到插件的官網及文件

![](https://hackmd.io/\_uploads/rkdQA3j92.png)
