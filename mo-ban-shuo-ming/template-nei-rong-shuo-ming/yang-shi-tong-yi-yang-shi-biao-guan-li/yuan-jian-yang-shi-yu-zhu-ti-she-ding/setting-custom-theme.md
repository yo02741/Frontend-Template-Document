# Setting Custom theme

使用該方式重新定義樣式

```scss
// assets/scss/element-plus/index.scss

@forward "element-plus/theme-chalk/src/common/var.scss" with (
...
)
```

再透過 Vite > [css.preprocessorOptions](https://vitejs.dev/config/shared-options#css-preprocessoroptions) 引入樣式表

```javascript
// vite.config.js

css: {
  preprocessorOptions: {
    scss: {
      additionalData: `
        @use "@/assets/scss/element-plus/index.scss" as *;
      `,
    },
  },
},
```

而其中，為了讓開發者更方便管理，故將 Sass Variable 再進一步的抽出

<pre class="language-scss"><code class="lang-scss"><strong>// assets/scss/element-plus/_variables.scss
</strong>
// $colors
$primary-color: #009a5b;
$secondary-color: #6b747d;
$success-color: #4aac48;
$danger-color: #ff5252;
$error-color: #ff5252;
$warning-color: #ffcc03;
$info-color: #1ea8c5;
$light-color: #f8f9fb;
$dark-color: #303133;

// $text-color
$primary-text-color: #222222;
$regular-text-color: #222222;
$secondary-text-color: #6b747d;
$placeholder-text-color: #9c9c9c;
$disabled-text-color: #dddddd;

// $border-color
$base-border-color: #b2bbc4;
$light-border-color: #ccd1d8;
$lighter-border-color: #e0e1e9;
$extra-light-border-color: #edf1f1;

// $font-size
// 這邊用 css variable 的原因是：
// FontSizeController 這個 component 會根據這邊的值去改變 root 的 font-size
// 而 JavaScript 沒有辦法讀寫 sass variable，所以用 css variable
$base-font-size: var(--base-font-size);
$title-font-size: 1.75rem;
$extra-large-font-size: 1.375rem;
$large-font-size: 1.25rem;
$medium-font-size: 1.125rem;
$small-font-size: 0.875rem;
$extra-small-font-size: 0.8125rem;
</code></pre>

所以 index.scss 大略會像這樣子，使用定義好的變數進行樣式覆蓋

```scss
// assets/scss/element-plus/index.scss

@use "./variables" as var;

@forward "element-plus/theme-chalk/src/common/var.scss" with (
  $text-color: (
    "primary": var.$primary-text-color,
    "regular": var.$primary-text-color,
    "secondary": var.$secondary-text-color,
    "placeholder": var.$placeholder-text-color,
    "disabled": var.$disabled-text-color,
  ),
);
```
