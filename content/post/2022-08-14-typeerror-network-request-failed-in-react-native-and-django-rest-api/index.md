---
title: حل مشکل TypeError – Network Request Failed در ارتباط ریکت نیتیو با django rest
author: امید
type: post
date: 2022-08-14T17:15:32+00:00
url: /typeerror-network-request-failed-in-react-native-and-django-rest-api/
categories:
  - جنگو
  - دسته‌بندی نشده
tags:
  - بک اند
  - پایتون
  - جنگو

---
این مدت داشتم با ریکت نیتیو کار می‌کردم و تصمیم گرفتم خودم یه api با django rest framework بنویسم و از اون api توی اپ react native استفاده کنم، ولی وقتی میخواستم که api رو fetch بکنم ارور TypeError &#8211; Network Request Failed رو میگرفتم و درک نمیکردم چیه. اول فکر کردم که مشکل از ریکت نیتیوه و از کد هایی که نوشته بودم رو بررسی کردم ولی مشکلی پیدا نکردم و بعد از کمی سرچ کردن فهمیدم که مشکل از اونجا نیست و مشکل از سمت سروره و بعد که کمی فکر کردم فهمیدم که django داره روی لوکال هاست اجرا میشه و هر ریکت نیتیو روی دیوایسی که داره اجرا میشه میخواد به لوکال هاست اون دیوایس وصل بشه و چون چیزی پیدا نمی کرد ارور میداد.

بستگی به پلتفرمی که دارید ممکنه کمی این مراحل متفاوت باشه ولی راه حل کلی اینکه ip لوکال سیستمی که روش جنگو داره روش ران میشه رو پیدا کنید و وقتی که runserver میکنید ip رو اونجا بزارید. برای من که از لینوکس استفاده می‌کنم مراحل به این شکله:

مرحله اول گرفتن ip آدرس که اگه نگاهی به کنسولی که داره اپ ریکت نیتیو روش اجرا میشه به این صورت میتونید ip رو ببینید و ازش استفاده کنید:<figure class="wp-block-image">

<img decoding="async" src="https://lh6.googleusercontent.com/izgOR5YHyh62femDmiHZya-aF7Q1-HGa6M9CM0EQmWn2MUgihbdIXLL0YlU15lDxMAg6Q2uKdH-0BJ224C_4oukBQ9qivYwcQwqFX0lApISSaeQQ5eZTYC6Na-p_Nu-3A1mnelmTPc7h8LTsyUvRiso" alt="" /> </figure> 

و یا اینکه اگه از لینوکس استفاده می‌کنید دستور زیر رو توی ترمینال اجرا کنید و ip رو اونجا میتونید پیدا کنید.

<pre class="wp-block-code"><code>ip addr</code></pre>

و بعدش کافیه که سرور جنگو رو به این شکلی ران کنید(که برای من باید از sudo استفاده میکردم).

<pre class="wp-block-code"><code>python manage.py runserver 192.168.1.103:80</code></pre>

و مشکل به همین سادگی حل شد.