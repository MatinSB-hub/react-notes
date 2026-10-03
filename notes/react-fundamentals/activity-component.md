# Activity Component

> دسته: React Fundamentals

از کامپوننت `Activity` برای نمایش یا مخفی کردن کامپوننت ها یا کد های `JSX` استفاده میشود
مشابه `conditional rendering`

تفاوت اصلی: برخلاف `conditional rendering` (که کامپوننت رو کاملاً `unmount` می‌کنه و `state` ‌ش رو از دست می‌ده)، `Activity` با `mode="hidden"`:

1_کامپوننت رو `unmount` نمی‌کنه فقط از دید پنهانش می‌کنه.

2_مقدار `state‌` حفظ می‌شه.

3_اثراتش (`effects`) متوقف می‌شن (`cleanup` اجرا می‌شه).

4_دفعه‌ی بعد که `visible` شد، همون `state` قبلی برمی‌گرده.

این دقیقاً دلیل وجود `Activity` هست.

```jsx

return (
  <Activity mode={isOpen ? "visible" : "hidden"}>
    <div…
    </div>
  </Activity>
);

```

پراپ `mode` یکی از دو مقدار `"visible"` یا `"hidden"` را می‌گیرد و بر اساس آن تصمیم می‌گیرد که `children` را نمایش دهد یا مخفی کند.
