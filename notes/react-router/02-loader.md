# Loader

> دسته: React Router

لودر در `route` ها قبل از اینکه المانی که تعیین کردیم برای روت اجرا بشه اجرا میشه

**نکته:** `loader` فقط با `Data Router` کار می‌کنه یعنی باید از `createBrowserRouter` و `<RouterProvider>` استفاده کنی، نه `<BrowserRouter>`.

```jsx

children: [
      {
        path: "moderator",
        children: [
          { index: true , loader: () => redirect("home") },

          { path: "home", element: <div>home page</div> },

          { path: "orders", element: <div>orders page</div> },

          { path: "products", element: <div>products page</div> },
        ],
      },
    ],
```

از لودر برای [`Route Protection`](route-protection.md) هم استفاده میشود

دقت کن که برای `redirect` کردن باید حتما `return` شود

درضمن مقدار `return` شده درون کامپوننت مربوط به همان `route` با استفاده از هوک `useLoaderData` بدون ورودی قابل دسترسی هست

اگر نیاز به دادهای لودر از مسیر های دیگه داریم باید از `useRouteLoaderData(routeId)`

استفاده کنیم که `routeId` درواقع آیدی هست که برای همان `route` در نظر گرفته ایم (`id` یه `prop` جداست که باید صریحاً توی تعریف `route` بدی (مثل "`id`: "`moderator-root`). اگه `id` نداشته باشی، `useRouteLoaderData` کار نمی‌کنه)
