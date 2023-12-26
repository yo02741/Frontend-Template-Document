# 補充：樣式表檔名

> 結論：Vite 專案下，不需要主動安裝 Sass Compiler 編譯樣式，其實不需要在無須編譯的檔案前面加下底線，這邊還留有下底線的原因：用於辨識什麼檔案為主要的樣式表、什麼檔案為引入的樣式表。

此 Frontend Template 使用 Sass 作為 CSS preprocessor，使用其 SCSS 語法進行撰寫。

瀏覽器並不能讀懂 Sass，故需要編譯成 CSS 檔。

平常開發時，若所有的檔案都為 `xxxxx.sass / xxxxx.scss`  ，Sass Compiler 會將所有的副檔名為 `.sass / .scss` 的檔案編譯。

為了好管理樣式，通常會定義一個樣式入口，如：`all.scss`

將不需要編譯的檔名前面加上`下底線`，如：`_checkbox.scss`

再透過 `@import` 引入樣式表。

<figure><img src="../../../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

&#x20;Frontend Template 建構於 Vite 上，Vite 本身有支援 Sass，故我們安裝 Sass 作為我們的 CSS Preprocessor，並不需要額外安裝套件來編譯 Sass/SCSS 到 CSS 。
