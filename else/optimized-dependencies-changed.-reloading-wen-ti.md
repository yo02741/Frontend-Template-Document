# optimized dependencies changed. reloading 問題

1️⃣ 關於 Element Plus 的 UI Components， 採官方建議的 Auto Import 而非 Full Import ( 能夠大幅降低打包大小 ) 或 Manually import ( 不需要維護到底引入了多少元件 ) 。

2️⃣ Demo 時，首先透過 template 建立一個新專案，啟動後，點選左方 Tab，則該 Tab 的相關內容才會開始執行找元件、撈必須資料的動作，並會造成畫面 reload。

<figure><img src="../.gitbook/assets/2023-09-08 14-27-41 (online-video-cutter.com).gif" alt=""><figcaption></figcaption></figure>

3️⃣ 測試部屬，首次開啟所有的 Tab 並不會在開發端那樣 reload。

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

4️⃣ 反覆測試後，發現並非每次的 dependencies 載入都會導致 reload

```
3:04:59 PM [vite] ✨ new dependencies optimized: element-plus/es/components/form/style/index, element-plus/es/components/radio-group/style/index, element-plus/es/components/radio/style/index, element-plus/es/components/checkbox-group/style/index, element-plus/es/components/checkbox/style/index, ...and 6 more
3:05:06 PM [vite] ✨ new dependencies optimized: element-plus/es/components/loading/style/index, element-plus/es/components/pagination/style/index, element-plus/es/components/table/style/index, element-plus/es/components/table-column/style/index, element-plus/es/components/popover/style/index
3:05:06 PM [vite] ✨ optimized dependencies changed. reloading
3:06:04 PM [vite] ✨ new dependencies optimized: element-plus/es/components/dialog/style/index, element-plus/es/components/button/style/index
3:06:04 PM [vite] ✨ optimized dependencies changed. reloading
3:06:23 PM [vite] ✨ new dependencies optimized: element-plus
3:06:23 PM [vite] ✨ optimized dependencies changed. reloading
```

5️⃣ 首先先了解一個 Vite 為何啟動速度這麼快 ( [Dependency Pre-Bundling](https://vitejs.dev/guide/dep-pre-bundling.html) )，該作法搭配上 動態 Component 及 後續鎖說的 Auto Import 能夠大幅的降低應用程式 initial 的負擔，對於 Fronetend Performance 有正影響。

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p> <a href="https://vitejs.dev/guide/dep-pre-bundling.html">Dependency Pre-Bundling</a></p></figcaption></figure>

6️⃣ 可以發現這些封包中並沒有 Tab 的內容 （ 因為我們使用 Dynamic Import 載入 Component ），也沒有看到 Element-Plus 相關的封包 （ 因為 Element-Plus 我們使用 Auto-Import 載入 ），因此點完 Tab 後載入大量資料也是預料中的事

7️⃣ 但是 reloading 的時機我們仍不得而知，開發區使用 Full Import 、部屬時使用 Auto Import 好像滿奇怪的



? [Dep Optimization Options](https://vitejs.dev/config/dep-optimization-options.html)





