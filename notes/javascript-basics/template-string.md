# Template string

> دسته: JavaScript Basics (ES6+)

که اسم استاندارد آن `template literal` است

از `template literal` برای ساخت رشته (`string`) استفاده می‌شه، ولی خواناتر از `+` و` "..."` هست.

```jsx
console.log(`id:${15 + 15} \nname: ${name} \nage:${age}`);
```

برای استفاده از این روش، متن رو بین دو بک‌تیک (<code>`</code>) و هر جایی که لازم بود از عبارت‌های <code>JavaScript</code> استفاده بشه <code>{}$</code> استفاده میشود بجای <code>+</code>

نکته ی جالب در مورد آن این است که برای رفتن به خط بعدی میتوان هم از `\n` استفاده کرد و هم `enter` بدون اینکه خطایی ایجاد شود

<p align="right" dir="rtl">
<code>template literal</code> توی <code>JSX</code>:
</p>

```jsx
<div className={`btn ${isActive ? "active" : ""}`}>
```
