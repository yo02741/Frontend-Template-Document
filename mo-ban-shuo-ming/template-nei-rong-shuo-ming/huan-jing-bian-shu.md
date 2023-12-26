# 環境變數

通常會以 `development` 完成開發後，部屬上 `stage` 進行測試，測試無誤後再部屬至 `production`。

* `development` 可以使用 `npm run dev` 進行測試。
* `stage` 可以建立另一個 Script `"dev:stage": "vite --mode stage"`，並使用 `npm run dev:stage` 進行測試。
* `production` 可以使用 `npm run build` 完後， `使用 npm run preview` 進行測試。

**development**

```
# 注意： 前綴設為『 VITE_ 』才會被 Vite 認定為環境變數，否則會被忽略。

# 版本
NODE_ENV=development
# 應用程式名稱
VITE_APP_TITLE=dev/template
# 應用程式 API 路徑
VITE_APP_BASE_URL='/api'
# 應用程式公開路徑
VITE_BASE_PUBLIC_PATH='/'
```

**stage**

```
# 注意： 前綴設為『 VITE_ 』才會被 Vite 認定為環境變數，否則會被忽略。

# 版本
NODE_ENV=stage
# 應用程式名稱
VITE_APP_TITLE=stage/template
# 應用程式 API 路徑
VITE_APP_BASE_URL='/api'
# 應用程式公開路徑
VITE_BASE_PUBLIC_PATH='/'
```

**production**

```
# 注意： 前綴設為『 VITE_ 』才會被 Vite 認定為環境變數，否則會被忽略。

# 版本
NODE_ENV=production
# 應用程式名稱
VITE_APP_TITLE=prod/template
# 應用程式 API 路徑
VITE_APP_BASE_URL='/api'
# 應用程式公開路徑
VITE_BASE_PUBLIC_PATH='/'
```
