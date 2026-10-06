# Debounce

> دسته: Working with APIs (fetch, axios, patterns)

مفهوم `debounce` یعنی مثلا زمانی که داریم توی `search input` تایپ میکنیم با هر بار تایپ حرف جدید سرچ انجام نشه چون در این صورت برای هر حرف یکبار `API` درگیر میشه برای همین از `debounce` استفاده میشود که یعنی بعد از یک مدت زمان مشخص مثل 0.5 ثانیه اگر کاربر دیگه تایپی انجام نداد سرچ صورت بگیره.

```jsx
useEffect(() => {
  const timeoutId = setTimeout(() => {
    handleSearch();
  }, 500);
  return () => clearTimeout(timeoutId);
}, [searchValue, handleSearch]);
```

در دستور بالا در صورتی که 0.5 ثانیه از آخرین تایپ کاربر بگذرد تابع مربوط به فیلتر کردن محصولات فراخوانی میشود و اگه کاربر دوباره تایپ کنه، `searchValue` عوض می‌شه. چون `searchValue` توی آرایه‌ی `dependency` هست، `React` اول `cleanup` رندر قبلی رو صدا می‌زنه (یعنی `clearTimeout(timeoutId)`), و بعد `effect` جدید رو اجرا می‌کنه (یه `setTimeout` جدید). این‌طوری `timeout` قبلی لغو می‌شه و شمارش از نو شروع می‌شه.


معمولاً به‌جای پیاده‌سازی دستی، از `lodash.debounce` استفاده می‌شه:

```jsx

import { useMemo, useEffect, useState } from "react";
import debounce from "lodash.debounce";

function Search() {
  const [searchValue, setSearchValue] = useState("");

  const debouncedSearch = useMemo(
    () => debounce((value) => {
      console.log("Searching for:", value);
    }, 500),
    []
  );

  useEffect(() => {
    debouncedSearch(searchValue);
    return () => debouncedSearch.cancel();
  }, [searchValue, debouncedSearch]);

  return (
    <input
      value={searchValue}
      onChange={(e) => setSearchValue(e.target.value)}
    />
  );
}

```

**نکته:** `debounce` رو باید با `useMemo` بسازیم، وگرنه هر رندر یه نسخه‌ی جدید می‌سازه و `debounce` بی‌اثر می‌شه.

