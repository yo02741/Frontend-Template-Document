# Global CSS

html、body、 scrollbar style、vue transition、etc.

```scss
:root {
  // 若要改 base 字體大小，記得也要改 FontSizeController 的 fontSizeDict
  --base-font-size: 16px;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

body,
html {
  font-size: var(--el-font-size-base);
  font-family: Arial, "Noto Sans TC", "Noto Sans", sans-serif;
  color: var(--el-text-color-primary);
  height: 100vh;
  overflow: hidden;
}

#app {
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow: hidden;
}

/* width */
::-webkit-scrollbar {
  width: 15px;
  height: 15px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  border: 4px solid rgba(0, 0, 0, 0);
  background-clip: padding-box;
  border-radius: 9999px;
  background-color: #aaaaaa;
  &:hover {
    background-color: #adadad;
  }
}
::-webkit-scrollbar-corner {
  background-color: transparent;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.3s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

```
