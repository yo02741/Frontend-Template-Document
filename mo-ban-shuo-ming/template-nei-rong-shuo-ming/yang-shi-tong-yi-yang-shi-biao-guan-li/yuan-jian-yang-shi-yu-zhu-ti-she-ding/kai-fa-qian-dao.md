# 開發前導

1. Frontend Template 中初步將常用到的元件修改為設計稿的樣式，但並沒有所有元件的樣式，未來會逐步的增加。
2. 若開發者有需求要使用其他的 Element-Plus 的元件，請參考其他元件修改樣式的作法，並抽出獨立的樣式表。
3. 調整 Element-Plus 元件樣式請盡量使用該元件的 class 去 target 到目標
4. 注意不要在獨立的樣式表調整公共或其他元件的樣式 （ Element-Plus 有時會一元件使用另一元件，有可能改壞其他樣式，e.g. el-table 裡的篩選是使用 el-checkbox ），。
5. 部份元件有結構上的不同，導致串連了很完整的 class 也沒有辦法把樣式覆蓋 （ 使用 additionalData 加入 Element-Plus 樣式表似乎在 main.js 載入 all.scss 之後，所以就算 Selector weight 相同樣式也沒辦法覆蓋 ），故在 `index.html` 中於 `id="app"` 的元素上再 bind 上 `class="tung"`，用來處理已經用盡方法但還是改不了樣式的情境。
6. 盡量不要用 !important 。
7. 在撰寫樣式表時，應思考這種樣式是只有這邊使用或是大概都會是這樣，再區分說哪些寫在公共樣式表，哪些寫在元件 scoped 住，這邊以 checkbox 為例：

\-> 大概都會是這樣，故以下樣式抽出後放在公共樣式表：

<figure><img src="../../../../.gitbook/assets/image (9).png" alt="" width="404"><figcaption><p>input 、label 樣式</p></figcaption></figure>

```scss
.el-checkbox {
    margin: 0;
    width: 100%;
    /* input style */
    .el-checkbox__input .el-checkbox__inner {
      width: 18px;
      height: 18px;
      border-radius: 4px;
      &::after {
        left: 5px;
        width: 4px;
        height: 8px;
        border-width: 2px;
      }
    }
    /* check all feature*/
    .el-checkbox__input.is-indeterminate .el-checkbox__inner::before {
      top: 50%;
      transform: translateY(-50%) scale(0.5);
      height: 5px;
    }
    /*
      label style
      label 若太長則截斷，並在最後面加上省略號
    */
    .el-checkbox__label {
      font-size: var(--el-font-size-base);
      font-weight: normal;
      line-height: 36px;
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
    }
  }
```

\-> 只有這邊使用，故以下樣式寫在元件 scoped 住：

<figure><img src="../../../../.gitbook/assets/image (10).png" alt="" width="426"><figcaption><p>要使其項目幾個為一列，且 input 於 label 最上方且對齊</p></figcaption></figure>

```scss
/* checkbox-group style ( with grid ) */

/* 每個 row 有幾個直行 */
$checkbox-group-column: 4;

.el-form-item.checkbox-group .el-checkbox-group {
  width: 100%;
  display: grid;
  grid-template-columns: repeat($checkbox-group-column, minmax(0, 1fr));
  grid-gap: 10px;
  overflow: hidden;
  /*
    配合 label 換行，故須處理多行的樣式
  */
  :deep(.el-checkbox) {
    display: flex;
    align-items: flex-start;
    height: auto;
    min-height: 36px;
    margin: 0;
    .el-checkbox__input {
      top: 0;
      transform: translateY(8px);
    }
    /*
      label style
      label 若太長則換行繼續顯示
    */
    .el-checkbox__label {
      white-space: normal;
    }
  }
}
```

