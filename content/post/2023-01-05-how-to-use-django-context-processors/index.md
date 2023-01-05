---
title: context processor ها در جنگو
author: امید
description: "گاهی اوقات لازم داریم که یه متغییر توی همه‌ی تمپلیت‌هامون در دسترس باشه.

برای اینکار دو روش وجود داره:

۱. روش سخت:‌ متغییری که لازم داریم رو توی همه‌ی view ها بزاریم

۲. روش آسون: یه custom context processor بسازیم"
type: post
draft: false
date: 2023-01-05T20:26:35+03:30
categories:
  - جنگو
tags:
  - بک اند
  - جنگو
---

گاهی اوقات لازم داریم که یه متغییر توی همه‌ی تمپلیت‌هامون در دسترس باشه.

برای اینکار دو روش وجود داره:

۱. روش سخت:‌ متغییری که لازم داریم رو توی همه‌ی view ها بزاریم

۲. روش آسون: یه custom context processor بسازیم

منطقیه که از روش دوم که هم آسون تره و در نهایت کد تمیز تری داریم استفاده کنیم.

## چطور میشه از روش آسون اینکار رو بکینم؟

فرض کنیم که توی موقعیتی هستیم که لازمه یه عکس بنر رو توی تک تک صفحات وبسایت نمایش بدیم که این عکس بنر از دیتابیس گرفته میشه.

فایل [models.py](http://models.py) این شکلیه:

```python
# models.py
class BannerImage(models.Model):
	image = models.ImageField(upload_to="img")
```

حالا با استفاده از custom context processor که می‌نویسیم می‌تونیم بهش دسترسی داشته باشیم.

یه فایل به اسم context_processors.py توی دایرکتوری(پوشه)‌ app مورد نظرمون میسازیم و داخلش یه فانکشن می‌نویسم که در نهایت یه دیکشنری برامون بر می‌گردونه.

```python
# context_processors.py
from .models import BannerImage

def access_banner_image(request):
	bannerImage = BannerImage.object.latest('-id') # query the latest banner image 
	return {
	'bannerImage': bannerImage,
	}
```

فانکشن access_banner_image یه context processor که خودمون ساختیم و برای اینکه بتونیم استفادش کنیم باید context processor خودمون رو به فایل [settings.py](http://settings.py) بخش TEMPLATE هاش اضافه کنیم و بعد از اون متغییر bannerImage برامون توی تمام تمپلیت‌ها قابل دسترس میشه.

```python
#settings.py
TEMPLATES = [
    {
        #under OPTIONS key
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
	               #context processor written by us.
                'appname.context_processors.access_banner_image'
],
        },
    },
]
```

 و تمامممم، الان bannerImage توی کل تمپلیت‌ها قابل دسترسه.

## و حالا چطوری توی تمپلیت‌هامون ازش استفاده کنیم:

```python
<img src="{{bannerImage.image.url}}" alt=''/>
```
با استفاده از context proccessor ها خیلی راحت تر و البته تمیز تر میتونیم کارهامون رو انجام بدیم.