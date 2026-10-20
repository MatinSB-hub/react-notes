# Fragment

> دسته: React Fundamentals

<p dir="rtl">
<code>JSX</code> فقط یک عنصر والد قبول می‌کنه. اگه بخوایم چند عنصر رو با هم <code>return</code> کنیم ولی نخوایم یه عنصر اضافی (مثل <code>div</code>) توی <code>DOM</code> داشته باشیم، از <code>Fragment</code> استفاده می‌کنیم.
</p>

چون `div` یه عنصر اضافی توی `DOM` ایجاد می‌کنه که می‌تونه `layout` یا سمنتیک `HTML` رو به‌هم بزنه (مثلاً `<div>` داخل `<ul>` مجاز نیست).

وقتی `Fragment` استفاده می‌کنی، توی `DevTools` هیچ عنصر اضافی نمی‌بینی — فقط فرزندانش هستن.

<p dir="rtl">
<code>Fragment</code> فقط <code>key</code> رو قبول می‌کنه، نه <code>className</code>، نه <code>style</code>، نه هیچ <code>prop</code> دیگه‌ای. اگه به <code>prop</code> نیاز داری، باید از <code>div</code> استفاده کنی.
</p>

به دو صورت قابل استفاده است:

```jsx
return (
  <React.Fragment>
    <li>About Us</li>
    <li>Contact Us</li>
  </React.Fragment>
);
```

```jsx
return (
  <>
    <li>About Us</li>
    <li>Contact Us</li>
  </>
);
```

**نکته:** برای پاس دادن `key` به `Fragment` در `map،` باید حتماً از `React.Fragment` استفاده کنیم.

```jsx
{
  items.map((item) => (
    <React.Fragment key={item.id}>
      {" "}
      👈
      <li>{item.name}</li>
      <li>{item.price}</li>
    </React.Fragment>
  ));
}
```
