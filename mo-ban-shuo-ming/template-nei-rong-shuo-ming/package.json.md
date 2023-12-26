# package.json

### **name**

記得要改為自己的專案名稱

![](https://hackmd.io/\_uploads/HJc5VPfKn.png)

### **version**

[前端版本管理](https://hackmd.io/0PMbCc4FQ-OAIIKrjvGjQA)

![](https://hackmd.io/\_uploads/Sk0wSvzt2.png)

### **scripts**

可以根據需求添加 script。

如這邊我多加了 `dev:stage` 測試 `mode: stage` 的運作是否正常，也可以添加 `build:stage`之類的，或是說之後寫測試，可以添加 `"coverage": "vitest run --coverage"` 產出覆蓋率報告。

![](https://hackmd.io/\_uploads/Hyh5rPfY3.png)

### **dependencies / devDependencies**

是否鎖 lib 版號議題結論：

1. _**template**_ _**不鎖定版本號**_
2. _**project create from template 視專案週期性決定是否導入依賴管理**_&#x20;

* template 鎖版號：會導致更新版本頻率太低，長久下來仍須更新，更增加了維護成本。
* template 不鎖版本：使用者在不同時期 install，其中各 Library 版本都不相同，難以預料會發生什麼問題; 但原則上就算不鎖版號，minor / patch 不一致也不會造成多大的問題。

例外：vue-router 4.1.3 -> 4.1.4 小版本中，將推送 params 的方式做了調整，平常的撰寫方式在這邊遇到了問題。（ 但 vue-router 使用 param 傳遞資料本身就不是一個適合的作法，官方有提出更適合的 History API ）
