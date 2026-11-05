# useNavigate

> دسته: React Router

از این `hook` برای منتقل کردن کاربر به یک کامپوننت خاص استفاده میشود ( از نظر نتیجه مثل کامپوننت `Link،` ولی `useNavigate` برای جاهایی هست که می‌خوای برنامه‌نویسی‌شده (`programmatic`) کاربر رو منتقل کنیم, مثلاً بعد از `submit` فرم یا بعد از یه `validation`. `Link` برای لینک‌های قابل کلیک توی `UI` هست. )

```jsx
const navigate = useNavigate()

const goToHomeHandler = () => {

  navigate("/home")

};
```

به این صورت که یک متغیر از نوع `useNavigate` میسازیم و چون به ما یک تابع برمیگردونه به شکل تابع ازش استفاده میکنیم و سپس داخل پرانتز تابع `route` مورد نظر رو میگیم

کاربرد این روش این هست که قبل از منتقل شدن کاربر به `route` مورد نظر میتونیم یکسری اعتبارسنجی هایی رو انجام بدیم

از هوک `useNavigate` برای جابه جایی لوکیشن کاربر همانند لوکیشن در `js` خام هم استفاده میشود

برای مثال از دستور زیر برای بک زدن یا ارسال کاربر به صفحه قبلی که درونش بود استفاده میشود

```jsx
const navigate = useNavigate()

const goBackHandler = () => {

  navigate(-1)

};
```

عدد منفی به معنای `back` و عدد مثبت به معنای `forward`

نکته: مثلا زمانی هست که درون صفحه `notFound` هستیم و میخواهیم کاربر رو به صفحه `home` منتقل کنیم ولی نمیخواهیم کاربر بتونه با دکمه `back` برگرده به صفحه `notFound` در این حالت از از دستور زیر استفاده میکنیم

```jsx
const navigate = useNavigate()

const goBackHandler = () => {

  navigate("/home",{replace:true})

};
```

بعد از آدرس صفحه، توی یه `object` مقدار `replace: true` رو قرار می‌دیم.

این کار باعث میشه که صفحه ای که قرار است بهش منتقل بشیم درون همین صفحه جایگزین شود و در نتیجه دیگه امکان برگشت به صفحه `notFound` با استفاده از دکمه `back` وجود نخواهد داشت

البته مفهوم `replace` فقط زمانی کاربرد دارد که از ادرس `route` استفاده شود نه اعداد (-1,-2,...) در غیر این صورت `replace` عملکردی ندارد

برای ارسال کاربر به `route` داینامیک از دستور زیر استفاده میشود:

```jsx
navigate({
  pathname: `/product/${id}`,
  // یا با پارامترهای جدا:
  pathname: "/product",
  search: `?id=${id}`,
});

navigate("/product", { state: { id } });
```

یعنی بخش های مختلف `route` رو بصورت یک `object` مشخص میکنیم

از دستور زیر هم برای زمانی استفاده میشود که نمیخواهیم وقتی کاربر به `route` جدید منتقل میشود صفحه به بالا اسکرول شود و میخواهیم در صفحه جدید هم کاربر در همان نقطه اسکرول صفحه قبل قرار بگیرد.

```jsx
const navigate = useNavigate()

const goBackHandler = () => {

  navigate("/home",{preventScrollReset:true})

};
```
**نکته:** `preventScrollReset` فقط با `Data Router` (یعنی `<createBrowserRouter` + `<RouterProvider`) کار می‌کنه.

<p align="right" dir="rtl">
<code>navigate</code> می‌تونه آرگومان دوم بگیره با این گزینه‌ها:
</p>

```jsx
navigate("/home", {
  replace: false,
  state: { ... },
  preventScrollReset: false,
  relative: "route",  // "route" | "path"
});
```

```jsx
navigate("../home", { relative: "path" });  // نسبت به URL فعلی
navigate("../home", { relative: "route" }); // نسبت به route فعلی
```