---
title: "چگونه اسم پروژه جنگو را تغییر دهیم؟"
date: 2021-3-30T17:48:58+03:30
draft: false
categories:
    - "جنگو"
    - "آموزش"
    - "لینوکس"
tags:
    - "جنگو"
    - "آموزش"
    - "لینوکس"
---
همین چند روز پیش داشتم روی یه پروژه کار میکردم که لازم شد اسم پروژه رو عوض کنم. اولش با خودم گفتم که یه پروژه‌ی جدید بسازم بعد همه‌ی کدها رو اونجا پیست کنم ولی اصلا کار عاقلانه‌ای نبود و یادم افتاد که خیلی قبل تر توی یکی از آموزش‌های جنگویی که توی یوتوب دیده بودم مدرس گفت که میشه اسم پروژه رو تغییر داد.

در ادامه با هم دیگر این کار را انجا میدهیم و کار سختی نیست.

ساختار پروژه رو به شکل زیر در نظر بگیریم:
{{< figure src="images/1.png" >}}

خب اینجا اسم testVirgol رو در دوجا میبینم یکیش رو میشه به راحتی و بدون هیچ اضافه کاری عوض کرد (اولین testVirgol که می‌بینید. که در واقع دایرکتوری هست که شامل فایل‌های پروژست) و testVirgol دیگر شامل تنظیمات پروژه مثل فایل‌های settings ,init, urls و wsgi است که برای تغییر اسم این دایرکتوری لازمه چند خط کد رو تغییر بدیم. برای اینکه گیج نشید و رفع ابهام بشه testVirgol اول که گفتیم مشکلی پیش نمیاره عوض کردم و الان ساختار پروژه به این شکله:
{{< figure src="images/2.png" >}}

تنها کاری که انجام دادم عوض کردن اسم دایرکتوری بود که پروژه توش بود.

حالا بیایم و اسم testVirgol رو تغییر بدیم اگه اسم دایرکتوری رو عوض کنیم با این خطا مواجه میشیم:

```python
ModuleNotFoundError: No module named 'testVirgol'
```

تنها کاری که لازمه انجام بدیم تغییر ۴ خط کد توی فایل هایی هست که مشخص کردم و لازم نیست که داخل app هایی که داریم تغییری ایجاد کنیم.

```python
# settings.py
ROOT_URLCONF = ‘virgool.urls’
WSGI_APPLICATION = ‘virgool.wsgi.application’

# wsgi.py
os.environ.setdefault(“DJANGO_SETTINGS_MODULE”, “virgool.settings”)

# manage.py
os.environ.setdefault(“DJANGO_SETTINGS_MODULE”, “virgool.settings”)
```
کار پیچیده‌ای انجام ندادیم در فایل settings.py مسیر فایل WSGI, URL پروژه رو مشخص کردیم.

در فایل wsgi.py مسیر فایل settings را مشخص میکنیم.

و در فایل manage.py نیز مسیر فایل settings را مشخص می‌کنیم.

بعد از انجام این تغییرات با اجرا کردن سرور باید پیغام موفقیت زیر رو ببینیم:

```python
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
April 06, 2021 - 19:16:10
Django version 2.2, using settings 'virgool.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
و در نهایت ساختار پروژه به شکل زیر می‌آید:
{{< figure src="images/3.png" >}}
اگر مشکلی در هر یک از مراحل داشتید و یا نظری دارید در بخش نظرات بگید خوشحال میشم که بتونیم با کمک هم مشکل رو حل کنیم 

