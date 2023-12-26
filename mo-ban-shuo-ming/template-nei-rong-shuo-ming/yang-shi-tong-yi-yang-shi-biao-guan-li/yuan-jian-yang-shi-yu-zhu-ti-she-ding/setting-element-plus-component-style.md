# Setting Element-Plus Component Style

初步將常用到的元件修改為設計稿的樣式，例如常用到的 input、select、etc.

將元件的樣式表拆開撰寫，並引入 all.scss

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

```scss
// assets/scss/all.scss

@import "element-plus/theme-chalk/el-message";
@import "element-plus/theme-chalk/el-badge";
@import "./element-plus/checkbox";
@import "./element-plus/date-picker";
@import "./element-plus/date-range-picker";
@import "./element-plus/input";
@import "./element-plus/message";
@import "./element-plus/radio";
@import "./element-plus/select";
@import "./element-plus/skeleton";
@import "./element-plus/time-picker";
@import "./element-plus/tooltip";
```

最後在從 main.js 引入應用程式

```javascript
// main.js

import "./assets/scss/all.scss";
```
