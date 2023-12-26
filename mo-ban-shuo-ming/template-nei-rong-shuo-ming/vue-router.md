# Vue Router

在這邊設定路由與對應的 Component，身份驗證與權限驗證透過為路由的 `meta` 添加 `requiresAuthN` 與 `requiresAuthZ`，並在 `router.beforeEach` 或 `beforeEnter` 中設計相對應的行為。

```javascript
import { createRouter, createWebHistory } from "vue-router";
import LoginView from "../views/LoginView.vue";
import HomeView from "../views/HomeView.vue";
import SecretView from "../views/SecretView.vue";

import { useAppInfoStore } from "@/stores/appInfo";
import { useSidebarStore } from "@/stores/sidebar";
import { useUserInfoStore } from "@/stores/userInfo";

function checkRequiresAuthZ(to) {
  /**
   * 『 驗證授權 』 寫這邊
   *  透過使用者的 role 來判斷是否有權限
   */
  console.log(to);
  return false;
}

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      // 走到未定義的路徑時，導回首頁
      path: "/:pathMatch(.*)",
      redirect: "/dashboard",
    },
    {
      path: "/error",
      name: "Error",
      component: () => import("../views/ErrorView.vue"),
      beforeEnter: (to, from, next) => {
        const { isServerError } = useAppInfoStore();

        if (isServerError) {
          next();
          return;
        }
        next("/");
      },
    },
    {
      path: "/login",
      name: "Login",
      component: LoginView,
      beforeEnter: (to, from, next) => {
        // 若使用者已登入又導向登入頁面，則導回首頁
        const { userInfo } = useUserInfoStore();

        if (userInfo === null) {
          next();
          return;
        }

        next("/");
      },
    },
    {
      path: "/dashboard/:tab?",
      name: "Home",
      component: HomeView,
      meta: { requiresAuthN: true },
    },
    {
      path: "/secret",
      name: "Secret",
      component: SecretView,
      meta: { requiresAuthN: true, requiresAuthZ: true },
    },
  ],
});

router.beforeEach((to, from, next) => {
  const { userInfo } = useUserInfoStore();

  // 需要 『 驗證授權 』
  if (to.meta.requiresAuthZ && !checkRequiresAuthZ(to)) {
    alert("您沒有權限進入此頁面！");
    return next({ name: "Home" });
  }

  // 需要 『 身份驗證 』
  if (to.meta.requiresAuthN && !userInfo) {
    return next({ name: "Login" });
  }

  next();
});

export default router;

// 需要 『 身份驗證 』 requiresAuthN：使用者必須登入
// 需要 『 驗證授權 』 requiresAuthZ：使用者必須登入且必須有權限
```
