BLOG_PAPERMOD
---------------------------------------
ㅤ content/\
ㅤ └── posts/\
ㅤ ㅤ ㅤ └── autosar/\
ㅤ ㅤ ㅤ ㅤ ㅤ ├── index.md\
ㅤ ㅤ ㅤ ㅤ ㅤ ├── image_1.png\
ㅤ ㅤ ㅤ ㅤ ㅤ └── image_2.png


``📝`` Tên folder bài viết phải khác tên file markdown (autosar ≠ index).

______
\
Khi truy cập blog từ Facebook, một "fbclid" sẽ được tự động thêm vào sau URL, chẳng hạn:

```
bbtd.dev/?fbclid=IwAR06KXR17RgOlmz4PMcFuE8fNiqdOvfiVJVl8sW6PQpRIqxB1YXQDzSWKKw
```

Để bỏ đi phần râu ria này, trong **layouts/_default/baseof.html**, thêm một đoạn JS để check URL vào \<body>:
```html
<script>
(function() {
    if (window.location.search.includes("fbclid")) {
    const url = new URL(window.location);
    url.searchParams.delete("fbclid");
    window.history.replaceState(
        {},
        document.title,
        url.pathname + (url.search ? "?" + url.searchParams.toString() : "") + url.hash
    );
    }
})();
</script>
```

Để Google xem URL dù có fbclid hay không đều cùng là một URL, thêm một *Canonical Tag* vào \<head> :
```html
<link rel="canonical" href="{{ .Permalink }}">
```