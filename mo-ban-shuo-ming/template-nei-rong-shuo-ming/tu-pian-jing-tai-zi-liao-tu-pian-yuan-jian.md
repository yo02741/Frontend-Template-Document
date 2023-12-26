# 圖片靜態資料 / 圖片元件

我們來盤點一下有哪些方式可以讀 SVG 檔案，並比較一下這些方法：

<table><thead><tr><th width="151" align="center">方法</th><th align="center">描述</th><th align="center">優點</th><th align="center">缺點</th></tr></thead><tbody><tr><td align="center">&#x3C;img> 讀 SVG</td><td align="center">使用 <code>&#x3C;img></code> 標籤將 SVG 圖像嵌入</td><td align="center">直覺快速，不需要將 SVG 內容直接放在模板中</td><td align="center">有限的控制，只能通過 CSS 調整外觀，更深層的元素無法異動。</td></tr><tr><td align="center"> inline SVG </td><td align="center">直接將 SVG 內容嵌入 Vue 組件模板中。</td><td align="center">完全控制 SVG 內容，且不需要存放靜態檔案。</td><td align="center">SVG 內容需要直接放在模板中，可能讓模板變得複雜。</td></tr><tr><td align="center">SVG Component</td><td align="center">將 SVG 創建為 Vue 組件</td><td align="center">完全控制 SVG 內容，且畫面變得很簡潔。</td><td align="center">需要更多的代碼和配置，相對複雜</td></tr></tbody></table>



之前的作法為在 src/assets/icons 或 src/assets/images 中放圖片，並使用 \<img> 讀 SVG ，若是該圖片有需要做樣式上的變化時，最多只能使用 CSS 的 filter 來處理，但滿容易遇到 filter 完後的顏色有誤差。&#x20;



因應透過 CSS Variable 控制 theme 的模式，需要異動 SVG  中的樣式，故選擇  inline SVG 或 SVG Component 較為合適，不過 inline SVG 的程式碼量很多，大喇喇的躺在 Component 裡面還滿刺眼的，因此使用 SVG Component 為定案。

但也並非所有的圖片都為 SVG、所有的圖片都需要根據 CSS Variable 去做變化，故會有部份圖片在 assets ，有部份被抽成 Component 的情況：



<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>
