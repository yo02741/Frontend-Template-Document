# vite-plugin-html-env

需求：不同環境下的打包的專案，應用名稱不盡相同，希望透過環境變數的方式。

```javascript
// vite.config.js

// VitePluginHtmlEnv 能夠將環境變數注入到 index.html 中
import VitePluginHtmlEnv from "vite-plugin-html-env";

export default defineConfig({
    plugin: [
        VitePluginHtmlEnv(),
    ]
})
```

```
// .env.development
VITE_APP_TITLE=dev/template

// .env.stage
VITE_APP_TITLE=stage/template

// .env.production
VITE_APP_TITLE=prod/template
```

```html
<!- index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/sltung-logo-mark.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><{ VITE_APP_TITLE }></title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>
```

使用這種語法 -> <{ VITE\_APP\_TITLE }>



注意：雖然我們的 build script 是寫  `"build": "vite build"`  預設指定到 production，但 vite-plugin-html-env 預設是抓 .env 中的變數，像我們並沒有 .env 的檔案，因此變數會為 undefined，固改為 `"build": "vite build --mode production"` 。
