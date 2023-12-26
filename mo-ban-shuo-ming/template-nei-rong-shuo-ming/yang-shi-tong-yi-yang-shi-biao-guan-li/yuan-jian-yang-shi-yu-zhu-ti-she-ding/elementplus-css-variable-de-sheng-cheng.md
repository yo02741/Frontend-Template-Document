# Element-Plus CSS Variable 的生成

Element-Plus 會將變數輸出 CSS Variable，使應用程式中的元件能夠讀這些樣式變數，來進行畫面渲染。

trace Element-Plus 的 source code 前往 `element-plus/theme-chalk/src/main.scss`，可以看到生成 CSS Variable 的源頭：

```scss
@use 'mixins/mixins' as *;
@use 'mixins/var' as *;
@use 'common/var' as *;

@include b(main) {
  @include set-component-css-var('main', $main);

  display: block;
  flex: 1;
  flex-basis: auto;
  overflow: auto;
  box-sizing: border-box;
  padding: getCssVar('main-padding');
}
```

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption><p>應用程式加入了許多變數</p></figcaption></figure>

### 補充說明

至 `element-plus/theme-chalk/src/common/var.scss` 可以看到以下程式碼

```scss
// https://sass-lang.com/documentation/values/maps#immutability
// mix colors with white/black to generate light/dark level
@mixin set-color-mix-level(
  $type,
  $number,
  $mode: 'light',
  $mix-color: $color-white
) {
  $colors: map.deep-merge(
    (
      $type: (
        '#{$mode}-#{$number}':
          mix(
            $mix-color,
            map.get($colors, $type, 'base'),
            math.percentage(math.div($number, 10))
          ),
      ),
    ),
    $colors
  ) !global;
}

// $colors.primary.light-i
// --el-color-primary-light-i
// 10% 53a8ff
// 20% 66b1ff
// 30% 79bbff
// 40% 8cc5ff
// 50% a0cfff
// 60% b3d8ff
// 70% c6e2ff
// 80% d9ecff
// 90% ecf5ff
@each $type in $types {
  @for $i from 1 through 9 {
    @include set-color-mix-level($type, $i, 'light', $color-white);
  }
}

// --el-color-primary-dark-2
@each $type in $types {
  @include set-color-mix-level($type, 2, 'dark', $color-black);
}
```

雖然這邊 `light` 的模式是寫 `1-9`，但在另一個檔案 `element-plus/theme-chalk/src/mixins/_var.scss 又寫了以下程式碼：`

```scss
@mixin set-css-color-type($colors, $type) {
  @include set-css-var-value(('color', $type), map.get($colors, $type, 'base'));

  @each $i in (3, 5, 7, 8, 9) {
    @include set-css-var-value(
      ('color', $type, 'light', $i),
      map.get($colors, $type, 'light-#{$i}')
    );
  }

  @include set-css-var-value(
    ('color', $type, 'dark-2'),
    map.get($colors, $type, 'dark-2')
  );
}
```

因此，當你開啟開發者應用工具時，你只會看到以下變數：

<figure><img src="../../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

於是我們才需要自行定義 light-1 \~ light-9 中被遺漏的變數，但由於這些顏色都是根據比例調配，若設計師硬性規定色票一致，那也只好改了，沒有辦法做到要容易擴充又要精準的。
