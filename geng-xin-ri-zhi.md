# 🆕 更新日誌

### TabList 功能列  與 currentCategory 相關

> by 佳豪：currentCategory & currentTab 設計不適用於 『 從 TabList 以外的地方觸發變更路由』，擬設計讓路由變更後自動變更 currentCategory & currentTab 機制

原本設計為 currentCategory 放在 TabList.vue 中，切換 category 時再做 assign。

但若是有功能為切換到不同 category 下的某個 tab 時，且其所在位置不在 TabList.vue 裡面，當前結構無法直觀地 assign 值，故將 currentCategory 移動至 sidebar.js module。

另外，同步調整 showChildren 相關的程式碼，改為直接加在 tabList 中 （ 『 若 item 該層有 children，請加上 showChildren 』  ），並追加多個 getters 來實做 showChildren 的切換。

```javascript
{
  label: "TEST Children",
  component: "TheExample6",
  children: [
    {
      label: "TEST Children 1",
      component: "TheExample6_1",
    },
    {
      label: "TEST Children 2",
      component: "TheExample6_2",
    },
  ],
  showChildren: false, //  『 若 item 該層有 children，請加上 showChildren 』
},
{
  label: "Element Plus: Feedback",
  component: "TheExample5",
},
```

### &#x20;ElMessage 註冊相關

> by 佳豪：ElMessage 使用需經過取得 store 後執行 action 不太方便，擬設計註冊至 Vue 實體方便全局呼叫

#### ElMessage 相關，研究透過不同方式實做

1. Provide/Inject + pinia.use 註冊事件
2. app.config.globalProperties 直接註冊
3. exported function

⏩ Provide/Inject + pinia.use 註冊事件

```javascript
// main.js

import { useElMessageStore } from "./stores/element-plus/message";
const ElMessageStore = useElMessageStore();
app.provide("$message", ElMessageStore.showMessage);
pinia.use(({ store }) => {
  store.$message = ElMessageStore.showMessage;
});
```

```javascript
// vue component

<script setup>
const message = inject("$message");
const sayHello = () => message("success", "This is a success");
</script>
```

<pre class="language-javascript"><code class="lang-javascript"><strong>// Pinia module 
</strong>
actions: {
  testMessage() {
    this.$message("warning", "test message");
  },
},
</code></pre>

⏩ app.config.globalProperties 直接註冊

```javascript
// main.js

import { useElMessageStore } from "./stores/element-plus/message";
const ElMessageStore = useElMessageStore();
app.config.globalProperties.$message = ElMessageStore.showMessage;

app.mount("#app");

export default app; // 記得 export
```

```javascript
// vue component

<script setup>
const { proxy } = getCurrentInstance();
const sayHello = () => proxy.$message("success", "This is a success");
</script>
```

<pre class="language-javascript"><code class="lang-javascript"><strong>// Pinia module 
</strong><strong>
</strong>import app from "@/main";

actions: {
  testMessage() {
    app.config.globalProperties.$message(
      "warning",
      "This is a warning message"
    );
  },
},
</code></pre>

⏩ exported function

```javascript
// src/utils/element-plus.js

import { ElMessage } from "element-plus";

class ShowMessage {
  constructor() {
    this.ElMessage = ElMessage;
  }

  success(message) {
    this.show("success", message);
  }

  warning(message) {
    this.show("warning", message);
  }

  info(message) {
    this.show("info", message);
  }

  error(message) {
    this.show("error", message);
  }

  show(type, message) {
    // 秀 message 之前先關閉所有的 message (一次只有一則)
    // 也可以將 grouping 設定為 true，讓相同的訊息群組起來，
    // grouping 的樣式為 badge，已處理好樣式
    this.ElMessage.closeAll();

    this.ElMessage({
      // 訊息內容
      message,
      // 關閉週期
      duration: 2000,
      // 顯示模式: success / info / warning / error
      type,
      // 群組，會將內容相同的訊息群組起來
      grouping: false,
    });
  }
}

export const showMessage = new ShowMessage();
```

<pre class="language-javascript"><code class="lang-javascript"><strong>// vue component
</strong><strong>
</strong><strong>import { showMessage } from "@/utils/element-plus";
</strong>
const messageType = ["success", "warning", "info", "error"];
const onShowMessage = (type) => showMessage[type](`This is a ${type} message`);
// showMessage.success("也可以這樣子寫！")
</code></pre>

最終決定，message 沒有複雜到需要透過 pinia module 去做管理，故改寫為 exported function。



### 追加 ElMessageBox

> 除了 ElMessage 之外，平時也滿常使用 ElMessageBox 中的 confirm，故一同處理掉 ( confirm/alert/prompt )

<pre class="language-javascript"><code class="lang-javascript"><strong>// src/utils/element-plus.js
</strong>
import { ElMessageBox } from "element-plus";

<strong>class ShowMessageBox {
</strong>  constructor() {
    this.ElMessageBox = ElMessageBox;
  }

  alert(message, title, options) {
    this.ElMessageBox.alert(message, title, {
      confirmButtonText: "確定",
      callback: (action) => {
        showMessage.success(`已${action}`);
      },
      ...options,
    });
  }

  confirm(message, title, options) {
    this.ElMessageBox.confirm(message, title, {
      confirmButtonText: "確定",
      cancelButtonText: "取消",
      type: "warning",
      ...options,
    })
      .then(() => showMessage.success("已確認"))
      .catch(() => showMessage.info("已取消"));
  }

  prompt(message = "請輸入...", title = "請輸入六位數字", options) {
    this.ElMessageBox.prompt(message, title, {
      confirmButtonText: "確定",
      cancelButtonText: "取消",
      inputPattern: /\d{6}/,
      inputErrorMessage: "請輸入六位數字",
      ...options,
    })
      .then(({ value }) => showMessage.success(`輸入的值為: ${value}`))
      .catch(() => showMessage.info("已取消"));
  }
}

export const showMessageBox = new ShowMessageBox();
</code></pre>

<pre class="language-javascript"><code class="lang-javascript"><strong>// vue component
</strong><strong>
</strong><strong>import { showMessageBox } from "@/utils/element-plus";
</strong>
const messageBoxType = ["alert", "confirm", "prompt"];
const onShowMessageBox = (type) => {
  switch (type) {
    case "alert":
      showMessageBox.alert("你好呀", "Hello");
      break;
    case "confirm":
      showMessageBox.confirm("請確認是否刪除此筆資料", "警告");
      break;
    case "prompt":
      showMessageBox.prompt(); // 需要自己實作，需要的內容在 options
      break;
    default:
      break;
  }
};
// options 自行參考 Element Plus 官網
// showMessageBox.alert("內容！", "標題！", options)
</code></pre>

