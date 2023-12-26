# 字體控制器 Font Size Controller

<figure><img src="../../../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

元件說明：使用者能夠點擊 『 小、標準、大 』 來異動應用程式的基準字體大小

實做方式：透過 JavaScript 更改字體大小 （ CSS Variable ）



額外事件：

1. 專案使用 Element-Plus，為求專案樣式一致，故實做 Custom Theme&#x20;
2. Element-Plus 實做 Custom Theme ，透過 Sass 異動樣式
3. Sass 為 CSS Preprocessor，JavaScript 並沒有辦法直接地去讀寫 Sass Variable
4. 故字體使用 CSS Variable，再轉換成 Sass Variable，最後進行樣式表覆蓋。

```scss
// _global.scss

:root {
  // 若要改 base 字體大小，記得也要改 FontSizeController 的 fontSizeDict
  --base-font-size: 16px;
}

body,
html {
  font-size: var(--el-font-size-base);
}
```

```scss
// /src/assets/scss/element-plus/_variables.scss

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
```

<pre class="language-scss"><code class="lang-scss">// /src/assets/scss/element-plus/index.scss

<strong>@use "sass:math";
</strong><strong>@use "sass:map";
</strong>@use "./variables" as var;

@forward "element-plus/theme-chalk/src/common/var.scss" with (
  $font-size:
    (
      "title": var.$title-font-size,
      "extra-large": var.$extra-large-font-size,
      "large": var.$large-font-size,
      "medium": var.$medium-font-size,
      "base": var.$base-font-size,
      "small": var.$small-font-size,
      "extra-small": var.$extra-small-font-size,
    ),
);
</code></pre>



```javascript
// stores/appInfo.js

export const useAppInfoStore = defineStore("AppInfo", {
  state: () => ({
    activeFontSize: "normal",
    fontSizeDict: {
      small: { size: "14px", label: "小" },
      normal: { size: "16px", label: "標準" },
      large: { size: "18px", label: "大" },
    },
  }),
});

```

```javascript
// FontSizeController.vue

<script setup>
import { useAppInfoStore } from "@/stores/appInfo";
const appInfoStore = useAppInfoStore();
const { activeFontSize, fontSizeDict } = storeToRefs(appInfoStore);

const updateFontSize = (type) => {
  activeFontSize.value = type;
  document.documentElement.style.setProperty(
    "--base-font-size",
    fontSizeDict.value[type].size
  );
};
</script>

<template>
  <ul class="font-size-group">
    <li
      v-for="(value, type) in fontSizeDict"
      :key="type"
      :style="{ fontSize: value.size }"
      :class="{ active: activeFontSize === type }"
      @click="updateFontSize(type)"
    >
      <span>{{ value.label }}</span>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
.font-size-group {
  display: flex;
  align-items: flex-end;
  padding: 12px 0;
  height: 100%;
  gap: 10px;
  transition: all 0.3s;
  li {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5px;
    background: var(--el-color-primary-dark-1);
    border: 1px solid var(--el-color-primary-light-1);
    border-radius: 5px;
    color: #ffffff;
    font-weight: 500;
    transition: all 0.3s;
    cursor: pointer;
    &:hover,
    &.active {
      background: var(--el-color-primary-dark-3);
    }
  }
}
</style>

```
