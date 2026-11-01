# reduce

> دسته: JavaScript Basics (ES6+)

از متد `reduce` برای دسترسی به عناصر آرایه و دسترسی به مقدار قبلی که درون خود متد `return` شده استفاده میشود به این صورت که:

```jsx
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((prev, current) => prev + current, 0);
// sum = 10
```

همانند متد های `map` و `filter` میباشد و در ورودی یک تابع دریافت میکند و در ورودی تابع دو پارامتر تعریف میشود پارامتر اول (`prev`) توی اجرای اول، اگه مقدار اولیه بدی، همون مقدار اولیه‌ست, وگرنه اولین عنصر آرایه‌ست. توی اجراهای بعدی، مقدار `return` شده‌ی اجرای قبلیه.

**نکته‌ی مهم:** اگه مقدار اولیه ندی، `reduce` اولین عنصر آرایه رو `prev` می‌گیره و از دومین عنصر شروع می‌کنه. این می‌تونه باعث خطا بشه اگه آرایه خالی باشه (`TypeError: Reduce of empty array with no initial value`).

```jsx
const total = array.reduce(function (prev, current) {
  return prev + current.price;
}, 0); // ← مقدار اولیه
```

کد بالا از نظر سینتکس درسته، ولی اگه `array` آرایه‌ای از آبجکت‌ها باشه (مثل `[{price: 100}, {price: 200}]`)، `prev` + `current.price` کار می‌کنه چون `prev` از `0` شروع می‌شه. ولی اگه مقدار اولیه `0` رو نذاریم، `prev` اولین آبجکت می‌شه و `prev` + `current.price` می‌شه `"200[object Object]"` این همون دلیلیه که مقدار اولیه لازمه.

ترجیحا برای نام پارامتر ها از `prev`,`current` استفاده شود.

متد `reduce` در واقع چهار پارامتر به تابع میدهد

```jsx
array.reduce((prev, current, index, array) => {
  // prev: مقدار قبلی
  // current: عنصر فعلی
  // index: ایندکس فعلی
  // array: خود آرایه
}, initialValue);
```
