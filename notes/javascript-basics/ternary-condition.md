# Ternary Condition

> دسته: JavaScript Basics (ES6+)

از این دستور برای نوشتن شرط های تک خطی استفاده میشود

ساختار دستور :

<p alighn="right" dir="ltr">
شرط ? مقدار_true : مقدار_false
</p>



```jsx
const result = num1 + num2 === 13 ? "درسته" : "غلطه";
```


کاربرد اصلی در `React`: توی JSX نمی‌تونی `if`/`else` بنویسی، پس `ternary` خیلی رایجه:

```jsx
<div>
  {isLoggedIn ? <Dashboard /> : <Login />}
</div>
```

اگه فقط می‌خوای در صورت true بودن چیزی نشون بدی (بدون حالت false) ، `&&` خواناتره:

```jsx
{isLoggedIn && <Dashboard />}
```