# Spread Syntax

> دسته: JavaScript Basics (ES6+)

<p align="right" dir="rtl">
<code>spread syntax</code> (سه نقطه <code>...</code>) یه <code>iterable</code> (مثل آرایه، رشته، <code>Set</code>) رو به عناصر جداگانه باز می‌کنه. یعنی <code>...</code> عناصر رو پخش می‌کنه.
</p>

```jsx
const array = [5, 8, 6, 1, 3, 4, 7, 9, 2];

console.log(...array);
```

**نکته:** `Rest` و `Spread` هر دو از `...` استفاده می‌کنن، ولی کارشون فرق داره:

<p align="right" dir="rtl">
<code>Spread</code>: عناصر رو پخش می‌کنه (توی فراخوانی تابع یا ساخت آرایه/آبجکت). <br/>
<code>Rest</code>: باقی عناصر رو جمع می‌کنه و به‌صورت آرایه برمی‌گردونه (توی پارامتر تابع یا <code>destructuring</code>).
</p>

کاربرد های دیگر:

```jsx
const copy = [...array]; // کپی آرایه

// ادغام آرایه‌ها
const merged = [...arr1, ...arr2];

// اضافه کردن به آرایه
const newArr = [...array, 10];

// کپی آبجکت
const newObj = { ...obj };

// ادغام آبجکت‌ها
const merged = { ...obj1, ...obj2 };

// پاس دادن آرایه به تابعی که آرگومان جدا می‌خواد
Math.max(...array); //  9
```

```jsx
[..."hello"]; //  ["h", "e", "l", "l", "o"]
[...new Set([1, 1, 2])]; //  [1, 2]
```

**نکته:** `Spread` کپی سطحی می‌ده

```jsx
const nested = [{ a: 1 }];
const copy = [...nested];
copy[0].a = 2;
console.log(nested[0].a); //  2 (چون سطحی کپی شده!)
```
