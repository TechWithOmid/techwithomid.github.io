---
title: چگونه اسم پروژه جنگو را تغییر دهیم؟
author: امید
type: post
date: 2021-04-30T15:16:27+00:00
url: /how-to-chage-django-project-name/
categories:
  - پایتون
  - جنگو
tags:
  - برنامه نویسی وب
  - بک اند
  - جنگو

---
همین چند روز پیش داشتم روی یه پروژه کار میکردم که لازم شد اسم پروژه رو عوض کنم. اولش با خودم گفتم که یه پروژه‌ی جدید بسازم بعد همه‌ی کدها رو اونجا پیست کنم ولی اصلا کار عاقلانه‌ای نبود و یادم افتاد که خیلی قبل تر توی یکی از آموزش‌های جنگویی که توی یوتوب دیده بودم مدرس گفت که میشه اسم پروژه رو تغییر داد.

_در ادامه با هم دیگر این کار را انجا میدهیم و کار سختی نیست._

ساختار پروژه رو به شکل زیر در نظر بگیریم:<figure class="is-layout-flex wp-block-gallery-2 wp-block-gallery has-nested-images columns-default is-cropped"> <figure class="wp-block-image size-large">

{{< figure src="1.png">}}
خب اینجا اسم testVirgol رو در دوجا میبینم یکیش رو میشه به راحتی و بدون هیچ اضافه کاری عوض کرد (اولین testVirgol که می‌بینید. که در واقع دایرکتوری هست که شامل فایل‌های پروژست) و testVirgol دیگر شامل تنظیمات پروژه مثل فایل‌های settings ,init, urls و wsgi است که برای تغییر اسم این دایرکتوری لازمه چند خط کد رو تغییر بدیم. برای اینکه گیج نشید و رفع ابهام بشه testVirgol اول که گفتیم مشکلی پیش نمیاره عوض کردم و الان ساختار پروژه به این شکله:<figure class="is-layout-flex wp-block-gallery-4 wp-block-gallery has-nested-images columns-default is-cropped"> <figure class="wp-block-image size-large">

{{<figure src="2.png">}}
تنها کاری که انجام دادم عوض کردن اسم دایرکتوری بود که پروژه توش بود.

حالا بیایم و اسم testVirgol رو تغییر بدیم اگه اسم دایرکتوری رو عوض کنیم با این خطا مواجه میشیم:

<pre class="wp-block-code"><code>ModuleNotFoundError: No module named 'testVirgol'</code></pre>

تنها کاری که لازمه انجام بدیم تغییر ۴ خط کد توی فایل هایی هست که مشخص کردم و لازم نیست که داخل app هایی که داریم تغییری ایجاد کنیم.

<p class="has-text-align-left">
  settings.py
</p>

<pre class="wp-block-code"><code>ROOT_URLCONF = ‘virgool.urls’
WSGI_APPLICATION = ‘virgool.wsgi.application’</code></pre>

<p class="has-text-align-left">
  wsgi.py
</p>

<pre class="wp-block-code"><code>os.environ.setdefault(“DJANGO_SETTINGS_MODULE”, “virgool.settings”)</code></pre>

<p class="has-text-align-left">
  manage.py
</p>

<pre class="wp-block-code"><code>os.environ.setdefault(“DJANGO_SETTINGS_MODULE”, “virgool.settings”)</code></pre>

کار پیچیده‌ای انجام ندادیم در فایل settings.py مسیر فایل WSGI, URL پروژه رو مشخص کردیم.

در فایل wsgi.py مسیر فایل settings را مشخص میکنیم.

و در فایل manage.py نیز مسیر فایل settings را مشخص می‌کنیم.

بعد از انجام این تغییرات با اجرا کردن سرور باید پیغام موفقیت زیر رو ببینیم:

<pre class="wp-block-code"><code>Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
April 06, 2021 - 19:16:10
Django version 2.2, using settings 'virgool.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.</code></pre>

و در نهایت ساختار پروژه به شکل زیر می‌آید:<figure class="is-layout-flex wp-block-gallery-6 wp-block-gallery has-nested-images columns-default is-cropped"> <figure class="wp-block-image size-large">

{{< figure src="3.png" >}}
اگر مشکلی در هر یک از مراحل داشتید و یا نظری دارید در بخش نظرات بگید خوشحال میشم که بتونیم با کمک هم مشکل رو حل کنیم 🙂