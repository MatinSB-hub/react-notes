# clsx

> دسته: Useful Packages & Tools

از این پکیج برای اسم گذاری راحت تر کلاس ها استفاده میشود

```jsx
import clsx from 'clsx'

function Home() {

  const isHidden = false

  return (

    <div className={clsx("text-5xl text-yellow-500", isHidden ?
"bg-blue-400" : "bg-red-500")}>Home</div>

  )

}

export default Home
```

قبل از استفاده باید `clsx` رو `import` کنی.

و مانند دستور بالا میتوان به `clsx` اسم کلاس های دلخواه را داد و هر کجا که نیاز به شرط بود از شرط استفاده کنیم

یک جور ساختار شرطی هم وجود دارد:

`Conditional Class Names`

```jsx
<button

  onClick={() => changePageHandler(currentPage - 1)}

  disabled={currentPage === 1}

  className={clsx("pagination-prev-button select-none", {

    "pages-ended active-tab": currentPage === 1, 👈

  })}


>
قبلی
</button>
```

این شرط باید حتما داخل {} قرار بگیرد

به این صورت کار میکند که اگر شرط بعد از : برقرار بود `class` هایی که تعیین کرده را اعمال میکند در غیر این صورت نادیده گرفته میشوند.
