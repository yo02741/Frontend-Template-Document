# 環境設置

#### Node

> Vite requires Node.js version 14.18+ / 16+
>
> Vue 3 requires Node.js version 16+

經測試後，雖然 14.18 也可以跑的起來 Vue 3 的專案， 但我們依照建議安裝 node 16

***

**檢視版本**

```
node -v
// v16.x.x
```

若你的 node 版本在 >= 16 版，這階段就完成了！

***

若你的 node 版本在 16 版以下，請確認是否有安裝 nvm

```
nvm -v
```

沒有安裝 nvm，建議安裝 nvm 並做 Node 版本切換。

有安裝 nvm，請安裝 Node 16。

```
nvm install 16
nvm use 16
```

***

> NVM Install For Windows

[GitHub - coreybutler/nvm-windows: A node.js version management utility for Windows. Ironically written in Go.](https://github.com/coreybutler/nvm-windows)

> NVM Install For Linux OR macOS

[GitHub - nvm-sh/nvm: Node Version Manager - POSIX-compliant bash script to manage multiple active node.js versions](https://github.com/nvm-sh/nvm)

***

不想裝 nvm，也可以直接下載 node 16 安裝

> Node Install

[Node v16.20.2 (LTS) | Node.js](https://nodejs.org/en/blog/release/v16.20.2)

#### VSCode

> Vue Language Features (Volar)
>
> 讓 VSCode 看得懂 .vue 檔
>
> [https://marketplace.visualstudio.com/items?itemName=Vue.volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
