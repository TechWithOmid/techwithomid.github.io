---
title: فعال کردن قابلیت tap to touch در i3
author: امید
type: post
date: 2022-06-27T12:33:07+00:00
description: یکی از اولین کار هایی که وقتی یه لینوکس جدید نصب میکنم انجام میدم فعال کردن قابلیت tap to touch هستش، که بصورت پیشفرض ممکنه بسته به توزیعی که استفاده می‌کنید، فعال یا غیرفعال باشه. و از اونجایی که از آرچ استفاده می‌کنم این قابلیت بصورت پیشفرض فعال نیست
url: /enable-tap-to-touch-in-i3/
categories:
  - i3
  - لینوکس
tags:
  - i3

---
یکی از اولین کار هایی که وقتی یه لینوکس جدید نصب میکنم انجام میدم فعال کردن قابلیت tap to touch هستش، که بصورت پیشفرض ممکنه بسته به توزیعی که استفاده می‌کنید، فعال یا غیرفعال باشه. و از اونجایی که از آرچ استفاده می‌کنم این قابلیت بصورت پیشفرض فعال نیست. علاوه بر آرچ اگر از مدیریت پنجره‌هاییs مثل i3, awesome, bspwm و&#8230; استفاده می‌کنید باید این قابلیت رو خودتون فعال &nbp;کنید. توی محیط های گرافیکی خیلی سادست از توی تنظیمات اینکار رو انجام میدی، ولی از اونجایی که من از محیط i3 استفاده میکنم مراحلش کمی متفاوت تره.

دو روش برای اینکار وجود داره روش اول از طریق تنظیمات خود i3 هستش و روش دوم از طریق xorg هستش که من توی این پست روش اول رو که ساده تره رو میگم.

## حال ندارید کل مطلب رو بخونید؟

فقط کافیه که دستور زیر رو به کانفیگ i3 خودتون یا معادلش رو برای awesome یا bspwm استفاده کنید.

<pre class="wp-block-code"><code>exec xinput set-prop "AlpsPS/2 ALPS GlidePoint" "libinput Tapping Enabled" 1</code></pre>



## استفاده از xinput برای فعال کردن tap to touch

براش شروع باید xinput رو توی ترمینال اجرا کنید که بفهمید که چه دیواس هایی دارید. اگه از آرچ استفاده می‌کنید می‌تونید دستور رو مستقیم در ترمینال اجرا کنید. اما اگه از فدورا اسفاده می‌کنید، باید اول از همه xinput رو با دستور زیر نصب کنید:

<pre class="wp-block-code"><code>sudo dnf install xinput</code></pre>

خروجی این دستوری برای لپتاپ من شبیه به اینه.<figure class="wp-block-image size-full">

<img decoding="async" loading="lazy" width="747" height="313" src="https://techwithomid.ir/wp-content/uploads/2022/06/xinput-min.png" alt="خروجی دستور xinput" class="wp-image-144" srcset="https://techwithomid.ir/wp-content/uploads/2022/06/xinput-min.png 747w, https://techwithomid.ir/wp-content/uploads/2022/06/xinput-min-300x126.png 300w" sizes="(max-width: 747px) 100vw, 747px" /> </figure> 

تاچ پد من توی این لیست دومین آیتمه. یعنی AlpsPS/2 ALPS GlidePoint. الان باید تمام پراپرتی هاش رو لیست کنیم برای اینکار دستور زیر رو میزنیم و بجای AlpsPS/2 ALPS GlidePoint اسم تاچ پدی که برای شما هست رو بزنید.

<pre class="wp-block-code"><code>xinput list-props "AlpsPS/2 ALPS GlidePoint"</code></pre>

و خروجی این دستور برای من.<figure class="wp-block-image size-full">

<img decoding="async" loading="lazy" width="743" height="629" src="https://techwithomid.ir/wp-content/uploads/2022/06/listprop-min.png" alt="خروجی دستور xinput list-prop" class="wp-image-146" srcset="https://techwithomid.ir/wp-content/uploads/2022/06/listprop-min.png 743w, https://techwithomid.ir/wp-content/uploads/2022/06/listprop-min-300x254.png 300w" sizes="(max-width: 743px) 100vw, 743px" /> </figure> 

چیزی که توی این خروجی برای ما مهمه اینه. درواقع این نشون میده که قابلیت tap to touch خاموشه.

<pre class="wp-block-code"><code>libinput Tapping Enabled (322):	0</code></pre>

الان با اجرای دستور زیر این قابلیت میتونه فعال بشه.

<pre class="wp-block-code"><code>xinput set-prop "AlpsPS/2 ALPS GlidePoint" "libinput Tapping Enabled" 1</code></pre>

توجه کنید بجای AlpsPS/2 ALPS GlidePoint اسم تاچ پد خودتون رو بزارید.

درسته که الان تاچ پد کار میکنه ولی اگه یبار سیستم رو ریستارت کنید باید همه‌ی این مراحل رو اجرا کنید. پس کاری که انجام میدیم اینکه کد زیر رو توی کانفیگ i3 میزارید (.config/i3/config):

<pre class="wp-block-code"><code>exec xinput set-prop "AlpsPS/2 ALPS GlidePoint" "libinput Tapping Enabled" 1</code></pre>

همچنین میتونید این پست رو توی <a href="https://virgool.io/@omidmmadi/%D9%81%D8%B9%D8%A7%D9%84-%DA%A9%D8%B1%D8%AF%D9%86-%D9%82%D8%A7%D8%A8%D9%84%DB%8C%D8%AA-tap-to-touch-%D8%AF%D8%B1-i3-ya7umqby8ngi" target="_blank" rel="noreferrer noopener">ویرگول</a> من هم بخونید.