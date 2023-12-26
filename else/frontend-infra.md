# Frontend Infra

DRY principle -> 過度抽象化（over-abstraction）與過早最佳化（premature-optimization）

***

Web Frontend Infra Team

* Boilerplate / Template / Generator
* Sharing Code
* Design System
* Unified CI/CD Infra
* Deploying & Serving
* Monitoring

***

只要目標是 提昇開發效率 （ DRY principle，快速建制基礎 ）、維持產品質量 （ 找出最佳實踐、統一規範 ），不管是小團隊或大團隊，都可以針對 frontend infra 投入。

***

* Boilerplate / Template / Generator：已撰寫 shell script&#x20;
* Coding Style：ESLint & Prettier
* Sharing Code：目前暫無前端團隊建構的 utilities，UI Component Library 可以考慮設計 （ 外部 package ）
* Design System：透過團隊熟悉的 Element-UI 以及主題定義，達到樣式統一 （ 議題：部份專案只需要這一塊 ）
* Testing：Unit Test 應該是每個專案都要跑的 … E2E 目前都是手動 …
* Dependency Management：目前並未管理各專案要用什麼套件、版本，若要管理的話可考慮使用 Renovate 來定期檢查依賴與升級，再找一個長期專案測試看看
* Preview URL：根據目前團隊的運作模式，似乎不太需要，大多都是部屬的測試區測試，也沒啥不方便的 ( 或是我不清楚 Preview URL 能作到什麼
* Development Tools：像是 bundle analyzer 之類的套件 … 交付專案前優化，可引入
* CI/CD Pipeline：除了基礎的 dev/stage/production 打包，可加入 unit test / coverage / sonarQube 等機制，但是否是每個專案都需要，是否要將這些功能加入 template，是否需要讓使用者選擇是否加入 …
* Deploying & Serving：目前前端團隊比較沒接觸這塊
* Observability （ Logging、Tracing、Metrics、Web Vitals、Error ）：
  * 目前前端是只有使用到 Graylog ，可以達到 Logging&#x20;
  * （ Surveying ）[Frontend Performance](https://chenyo.gitbook.io/frontend-performance/)：透過 Lighthouse 實現 Web Vitals 、Metrics 的統計
  * （ Someday ）透過 Sentry 紀錄 Error
  * （ Someday ）Grafana 呈現數值



參考文章、文件

[成為前端建築師吧！透過 Frontend Infra 為前端應用打造穩健且高效率的開發體驗](https://oldmo860617.medium.com/%E6%88%90%E7%82%BA%E5%89%8D%E7%AB%AF%E5%BB%BA%E7%AF%89%E5%B8%AB%E5%90%A7-%E9%80%8F%E9%81%8E-frontend-infra-%E7%82%BA%E5%89%8D%E7%AB%AF%E6%87%89%E7%94%A8%E6%89%93%E9%80%A0%E7%A9%A9%E5%81%A5%E4%B8%94%E9%AB%98%E6%95%88%E7%8E%87%E7%9A%84%E9%96%8B%E7%99%BC%E9%AB%94%E9%A9%97-21566b5c95d3)

[imteekay / frontend-infrastructure](https://github.com/imteekay/frontend-infrastructure)
