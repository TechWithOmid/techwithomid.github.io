---
title: "مهاجرت از وردپرس به هیوگو"
date: 2022-12-30T21:50:35+03:30
draft: false
categories:
  - wordpress
  - hugo
tags:
  - hugo
  - wordpress
---
مدتی بود که تصمیم داشتم دور وردپرس رو به دلیل سنگینی زیاد و سرعت لود پایینش خط بکشم به هیوگو رو آوردم و مشکلی که داشتم حدود ۲۰ تا پست توی وردپرس نوشته بودم و کپی کردنشون و تغییر دادنشون به مارکداون حوصله سر بر بود و وقت زیادی می‌خواست، با کمی سرچ به یه ابزار به اسم [wordpress-to-hugo-exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter) برخوردم و ابزار فوق علاده‌ای گفتم که توی بلاگ درمورد نحوه استفاده‌ش بنویسم.

این ابزار یک پلاگین وردپرسیه که کار کردن باهاش خیلی سادست. کافیه که مراحل زیر رو دنبال کنید.

اول از همه پلاگین رو از گیتهاب دانلود می‌کنیم، بعد اون رو داخل این مسیر کپی می‌کنیم:

```jsx
/wp-content/plugins
```

از قسمت پلاگین های وردپس افزونه رو فعال می‌کنیم. و بعد از منوی Tools گزینه `Eport to Hugo` رو انتخاب می‌کنیم.

{{<figure src="images/migrate-wordpress-to-hugo.png" alt="نحوه کار افزونه wordpress-to-hugo-exporter">}}

با انتخاب این گزینه همه‌ی پست‌ها، صفحات رو به همراه تنظیمات و فایل config.yml رو بصورت zip ارائه میده که میتونید با استفاده از اون خیلی راحت از وردپرس به هیوگو مهاجرت کنید.