# 專案結構

> * **/src/assets/icons** 放小 icon

> * **/src/assets/images** 放大圖片

> * **/src/assets/scss** 放樣式表

> * **/src/axios** 放處理 API 的一切東西

> * **/src/components** 放置所有的 components
>
> > * 若有`基礎共用`的 components，可以開個 `/src/components/Base` 資料夾存放
> > * 若有多個 components 屬於`同個群組`，可以開資料夾存放在一起，e.g. `/src/components/Modal`

> * **/src/router** Vue Router 相關

> * **/src/stores** Pinia 的 modules

> * **/src/views** 應同步 Vue Router，有關 router-view 的放這

> * **/App.vue** 拿來 createApp 並掛在在 `#app` DOM 上的 Component

> * **/main.js** App 的進入點

> * **/.env.\[development/stage/production]** 各環境的環境變數，若有需要 local env 自行添加

> * **/.eslintrc.js** ESLint Config

> * **/.gitignore** Files for Git Ignore

> * **/.prettierrc.js** Prettier Config

> * **/index.html** 該 App 的 index.html

> * **/package-lock.json** 目前 Library 安裝的版本

> * **/package.json** 指定 Library 安裝的版本、其餘 Script 、其餘設定與資訊

> * **/README.md** 系統說明文件

> * **/vite.config.js** vite 的設定文件
