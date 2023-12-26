# Axios

主要在 `index.js` 設定 Axios 實例與 API 定義，並在 `interceptors` 中處理 `token` 相關設定。

```javascript
// src/axios/index.js

import axios from "axios";

/**
 * 建立不同的 axios 實例
 * 透過 baseURL 的設定，可以讓不同的 axios 實例發送請求到不同的網域
 * （ 請配合 server.proxy ）
 *
 * 若有需要部屬到不同的網域，可以透過環境變數來設定 baseURL
 */

const ARequest = axios.create({
  baseURL: "/a",
});

const BRequest = axios.create({
  baseURL: "/b",
});

const CRequest = axios.create({
  baseURL: "/c",
});

/**
 * API 統一在這管理，需要呼叫 API 時，只要在 component 中 import 這些 function 即可
 */

export const getAData = () => ARequest.get("/data");

export const updateAData = (payload) => ARequest.post("/data", payload);

export const getBData = () => BRequest.get("/data");

export const updateBData = (payload) => BRequest.post("/data", payload);

export const getCData = () => CRequest.get("/data");

export const updateCData = (payload) => CRequest.post("/data", payload);
```

```javascript
// src/axios/interceptors

import axios from "axios";

/**
 * 這邊透過 global axios 設定 interceptors 來攔截 req res
 *
 * 若你的情境為不同的 instance 需要不同的 interceptors
 * 請去 axios/index.js export 出 instance 並個別設定
 */

// 於 main.js 中 import 並執行
export const setupInterceptors = () => {
  axios.interceptors.request.use(
    (config) => {
      // 若專案的 token 並非透過 cookie 方式傳遞，可以在此設定 HTTP Header
      return config;
    },
    (error) => Promise.reject(error)
  );

  axios.interceptors.response.use(
    (response) => response,
    (error) => {
      /**
       * 若專案有 refresh token 的機制，可以在此設定
       *
       * 原則上是在 response 回來後
       * 檢查是 1. Missing Token 或 2. Token Expired
       *
       * 1. 若是 Missing Token，則直接導向登入頁
       * 2. 若是 Token Expired，則發送 refresh token 的請求，
       * 並在成功後重新發送原本的請求，若仍失敗則導向登入頁
       */
      return Promise.reject(error);
    }
  );
};
```

```javascript
// src/main.js
.
.
import axios from "axios";
import VueAxios from "vue-axios";
import { setupInterceptors } from "./axios/interceptors";
setupInterceptors();

app.use(VueAxios, axios);
.
.
```
