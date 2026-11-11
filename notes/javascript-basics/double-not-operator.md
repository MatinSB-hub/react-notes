# Double NOT operator

> دسته: JavaScript Basics (ES6+)

`!` عملگر `NOT` هست که مقدار رو برعکس می‌کنه و به بولین تبدیل می‌کنه. `!!` یعنی دو بار `NOT`:

اولین `!`: مقدار رو به بولین تبدیل می‌کنه و برعکسش می‌کنه.

دومین `!`: دوباره برعکسش می‌کنه (به حالت اصلی برمی‌گرده، ولی حالا بولینه).

```jsx
!!0; // = false
!!1; // = true
!!""; // = false
!!"hello"; // = true
!!null; // = false
!!undefined; // = false
!!NaN; // = false
!![]; // = true  (آرایه‌ی خالی truthy هست!)
!!{}; // = true  (آبجکت خالی truthy هست!)
```

مقادیر `falsy` در `JS` (که `!!` تبدیلشون می‌کنه به `false`):
`false`، `0`، `-0`، `0n`، `""`، `null`، `undefined`، `NaN`

بقیه‌ی مقادیر (حتی `[]` و `{}` و `"0"` و `"false"`) `truthy` هستن.


نکته: `!!value` معادل `Boolean(value)` هست , هر دو یه مقدار رو به بولین تبدیل می‌کنن. `!!` کوتاه‌تره، `Boolean()` خواناتره.

```jsx
{!!user && <Dashboard />}
```
این کاربرد خیلی رایجه (چون اگه `user` یه `object` باشه، `user` `&&` ... ممکنه مقدار `object` رو رندر کنه).

```jsx
const name = user.name || "ناشناس";      // falsy = ناشناس
const age = user.age ?? 0;              // null/undefined = 0
const isActive = !!user.isActive;       // = بولین
```