# useMutation

> دسته: Useful Packages & Tools

برای تغییر داده (`POST`/`PUT`/`PATCH`/`DELETE`).

خودش کش نمیکنه ولی `state` درخواست رو مدیریت میکنه (`pending`/`error`/`success`) و `onSuccess`/`onError`/`onSettled` داره.

معمولاً بعدش کش `useQuery` ها رو `invalidate` میکنیم
میتونی روش `optimistic update` هم بذاری

```jsx
const mutation = useMutation({
  mutationFn: createPost,
  onSuccess: () => console.log("Success"),
});
```

<p dir="rtl"><code>onSuccess</code> فقط وقتی <code>mutation</code> موفق باشه</p>

<p dir="rtl"><code>onError</code> فقط وقتی <code>mutation</code> خطا بده</p>

<p dir="rtl"><code>onSettled</code> همیشه، چه موفق چه ناموفق (بعد از <code>success</code>/<code>error</code>)</p>

<p dir="rtl"><code>onMutate</code> قبل از <code>mutationFn</code> اجرا می‌شه. برای <code>Optimistic Update</code> استفاده می‌شه. می‌تونی مقدار برگردونی (<code>context</code>) که در <code>onError</code>/<code>onSuccess</code>/<code>onSettled</code> در دسترسه.</p>

<p dir="rtl">
<code>mutationFn</code>: تابعی که درخواست <code>API</code> رو انجام می‌ده. این تابع باید یه <code>Promise</code> برگردونه. پارامترهایی که به <code>mutate()</code> پاس می‌دی، به این تابع می‌رسن
</p>

```jsx
const mutation = useMutation({
  mutationFn: (newPost) => {
    return fetch("/api/posts", {
      method: "POST",
      body: JSON.stringify(newPost),
    });
  },
});

mutation.mutate({ title: "Hello", body: "World" });
```

<p dir="rtl"><code>mutate(data)</code> درخواست رو اجرا می‌کنه، ولی <code>Promise</code> برنمی‌گردونه.</p>
<p dir="rtl"><code>mutateAsync(data)</code> مثل <code>mutate</code>، ولی <code>Promise</code> برمی‌گردونه (برای <code>await</code> کردن).</p>

```jsx
const mutation = useMutation({ mutationFn: createPost });

mutation.mutate(newPost);

await mutation.mutateAsync(newPost);
```

<br/>
<p dir="rtl"><code>invalidate</code> کردن کش:</p>

```jsx
import { useQueryClient } from "@tanstack/react-query";

const queryClient = useQueryClient(); 👈

const mutation = useMutation({
    mutationFn: createPost,
  onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ["posts"] }); 👈
  },
});
```

<p dir="rtl"><code>invalidateQueries</code> باعث می‌شه <code>useQuery</code> های مربوطه دوباره <code>fetch</code> کنن.</p>

**نکته:**

<p dir="rtl"><code>useMutation</code> به‌طور پیش‌فرض <code>retry</code> نمی‌کنه (برخلاف <code>useQuery</code>). می‌تونی دستی فعالش کنی:</p>

```jsx
useMutation({ mutationFn, retry: 3 });
```