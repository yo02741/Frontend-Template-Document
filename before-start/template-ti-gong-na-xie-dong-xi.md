# Template 提供哪些東西？

> 功能導向

* 定義開發環境 （ use node 16
* 建構基礎的專案 （ use Vite + Vue 3
* 定義 / 規範專案的語法檢查與 Code Style （ use ESLint & Prettier
* 設定環境變數 （ Env
* 設定應用程式開發端設定（ use vite.config.js
* 前端發送 http request / 管理後端 API （ use Axios
* 建立樣式規範 （ use Element-Plus、Sass
* 定義前端路由規範（ use Vue-Router 4
* 定義前端模組規範（ use Pinia
* 持續整合（ use GitLab CI
* 單元測試（ use Vitest
* 元件測試（ use Vue Test Utils
* 導入增加 DX 的 Library （ e.g. unplugin-auto-import、unplugin-vue-components

> 設計導向

Best Practice & 常見功能範例

* Linter 與 Formatter 規範與設定流程
* 登入流程設計
* 身份驗證 Authentication (AuthN) 與驗證授權 Authorization (AuthZ) 機制開發
* 路由定義、結構規劃、路由或元件存取權管理
* Pinia Module 設計、功能拆分、使用方式
* Token 相關問題處理 ( use Axios interceptors
*
  * Missing Token 處理
  * Token Expired 處理與 Refresh Token 與重新呼叫後端 API 流程
* 後端 API 管理與模組拆分、開發環境 http request Proxy 設定
* 環境變數對應、Git Branch、GitLab CI 設計
* Vite 加載環境變數範例
* Vite 調整應用程式 title 範例 ( use vite-plugin-html-env
* 規範前端專案結構
* Component 與 Style 相關
*
  * Element-Plus On-demand Import
  * Element-Plus 整合應用程式設計
  * Element-Plus 的 Component Style 設計
  * Style Sheets 設計與全域共用 Sass variables、mixin、function 設定
  * Theme 設定與元件開發思維
  * 靜態資料與 Image Component 取決思維
  * Component 設計與拆分，以單一責任制設計，以漸進性模組思維前進
  * Component溝通範例
  * 常見 View實做
  *
    * Login
    * Home
    * Error
  * 常見 Component實做
  *
    * Timer
    * Font-Size Controller
    * Functional Selector
    * Transfer
* 使用 Composition API
* 使用 script setup
