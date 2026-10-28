# Route Protection

> دسته: React Router

**نکته:** برای route protection چند روش استاندارد وجود داره که روش دوم پیشنهاد می‌شه.

روش اول:

برخی `route` هایی که قبل از نمایش داده شدنشون باید یکسری چیز بررسی بشه مثل لاگین بودن و.... رو داخل `route Protection` قرار می دهیم

```jsx
function PrivateRoute({ children }) {
  const [isLogin, setIsLogin] = useState(true);

  const navigate = useNavigate();

  useEffect(() => {
    if (!isLogin) {
      navigate("/access-denied");
    }
  }, [isLogin, navigate]);

  return children;
}
```

به این صورت که یک کامپوننت `PrivateRoute` ایجاد میکنیم و بررسی شرط ها را در داخلش انجام میدیم و مانند کد بالا اگر شرط برقرار نبود کاربر به یک `route` دیگه `navigate` میشه و اگر برقرار بود `children` , `return` میشود

و درون فایل `Routes` هم به صورت زیر استفاده میشود:

```jsx
{

path: "/adminpanel",

element: (

    <PrivateRoute>

      <AdminPanel />

    </PrivateRoute>

  ),

children: [

    { path: "download", element: <Download /> },

    { path: "setting", element: <Setting /> },

    { path: "*", element: <NotFoundAdmin /> },

  ],

},
```

یعنی `component` که باید `private` باشد را به عنوان `children` به `component` ,`PrivateRoute` پاس میدیم و درون `component`,`PrivateRoute` شرط ها بررسی میشوند و در نتیجه `children`, یا `return` میشود یا نمیشود

در این روش حتی از `NestedRoutes` هم محافظت میشود (در صورت وجود)

حالت دیگه استفاده هم به این صورت هست که از `children` استفاده نمیشه بلکه `PrivateRoute` به عنوان `element` اصلی `Route` مشخص میشه و `NestedRoute` ها به عنوان `outlet` ارسال میشن داخل `PrivateRoute` در این حالت بجای `return` کردن `children` باید `Outlet`,`return` بشه

روش دوم:

روش دوم پیشنهاد میشود چون در روش اول ممکن هست قبل تکمیل شدن اعتبارسنجی بخشی از `route` به سرعت `render` شده و در `DOM` نمایش داده شود

**مزیت اصلی `loader`**:

<p align="right" dir="rtl">
<code>React Router</code> قبل از رندر کامپوننت صبر می‌کنه تا <code>loader</code> تموم بشه. پس کاربر هیچ‌وقت محتوای محافظت‌نشده رو نمی‌بینه. این دقیقاً همون دلیلیه که روش دوم بهتره.
</p>

**نکته:** `loader` فقط با `Data Router` کار می‌کنه یعنی باید از `createBrowserRouter` و `<RouterProvider>` استفاده کنی، نه `<BrowserRouter>`.

استفاده از `loader`:

```jsx
{
  path: "moderator",
  //route protection
  loader: async () => {
    try {
      const { data } = await getMe();
      if (!data.user.roles.includes("ADMIN")) {
        return redirect("/forbidden");
      }

      return data.user;
    } catch (err) {
      return redirect("/auth");
    }
  },

  children: [
    { path: "home", element: <div>home page</div> },
    { path: "orders", element: <div>orders page</div> },
    { path: "products", element: <ModeratorsProducts /> },
    { path: "categories", element: <ModeratorCategories /> },
    { path: "users", element: <ModeratorUsers /> },
  ],
},
```

**نکته‌ی مهم:** `loader` می‌تونه داده رو `return` کنه و کامپوننت با `useLoaderData` بهش دسترسی داشته باشه

```jsx
import { useLoaderData } from "react-router-dom";

function ModeratorPanel() {
  const user = useLoaderData();
  return <div>Welcome, {user.name}</div>;
}
```

اگه `loader` خطا بده، می‌تونیم `errorElement` بدیم:

```jsx
{
  path: "moderator",
  loader: ...,
  errorElement: <ErrorPage />,
  children: [...]
}
```
