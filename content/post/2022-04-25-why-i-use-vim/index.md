---
title: چرا از vim استفاده می کنم؟
author: امید
type: post
date: 2022-04-25T12:12:16+00:00
url: /why-i-use-vim/
description: "هر وقت که اسم vim میاد یه محیط سیاه رو تصور می‌کنید که وقتی واردش بشی دیگه بیرون اومدن ازش غیر ممکنه. و ممکنه براتون سوال باشه من چرا از vim استفاده می‌کنم"
tags:
  - لینوکس
  - ویم
categories:
  - لینوکس
  - ویم
---
<figure class="wp-block-image"><img decoding="async" src="https://files.virgool.io/upload/users/198151/posts/dwsmvdwe8ava/fohstvldnkov.png" alt="چرا از vim استفاده می‌کنم؟" /><figcaption class="wp-element-caption">کانفیگ vim من</figcaption></figure> 

هر وقت که اسم vim میاد یه محیط سیاه رو تصور می‌کنید که وقتی واردش بشی دیگه بیرون اومدن ازش غیر ممکنه. و ممکنه براتون سوال باشه من چرا از vim استفاده می‌کنم. برای اینکه تصورتون از vim عوض بشه که براتون یه محیط سیاست این کانفیگ vim منه البته از نئوویم(neovim) استفاده میکنم.&nbsp;البته میتونید توی <a href="https://www.reddit.com/r/vim/" target="_blank" rel="noreferrer noopener">reddit</a> کانفیگ‌های خفن تری رو ببینید ولی من با نیاز‌های خودم کانفیگ کردم و ازش راضیم.

_neovim درواقع یه فورک از vim با قابلیت های بیشتری مثل استفاده از lua و async_ داره _و بیشتر از و_یم _کامیونیتی محوره و این یعنی آپدیت های بیشتر و بهتر دریافت میکنه._

من اوایل هیچ علاقه‌ای به vim نداشتم و میگفتم تا vscode و pycharm هست چرا از ویم استفاده کنم. اما وقتی که داشتم چالش ۹۰روز کد رو توی اینستاگرام انجام میدادم با خودم گفتم که بیام و از ویم برای نوشتن اسکریپت‌های کوچیک ازشون استفاده کنم. به لطف کانفیگ‌هایی لینوکسی و نصب آرچ فقط استفاده بیسیک ازش رو میدونستم یعنی اینکه واردش بشم یه تکست رو بنویسم و خارج بشم. ولی بعد از یکمی سرچ زدن توی گوگل و یوتوب فهمیدم که vim خیلی بیشتر از این حرفاست و مهم نیست که چقدر با vim کار کرده باشید و چقدر توش خفن باشید در نهایت یه چیز جدید ازش میفهمی که انگشت به دهنت می‌کنه.

## چرا vim؟

**سادست چون از شر موس خلاص می‌شید**.

یکی از خصوصیات برنامه‌نویس خوب بودن گشاد بودنشه که همیشه دنبال ساده‌ترین راه برای یه کاری میگرده. و خب وقتی می‌خواید موس رو تکون بدید باید دست رو حدود ۲۰ سانتی‌متر تکون بدی و موس رو بگیری و تکون بدی و بعدش دوباره همون ۲۰ سانتی‌متر رو برگردی کار خیلی سختیه. ولی وقتی دستت روی کیبرده دیگه این وقت تلف نمیشه و راحت‌تر هستید. البته کمی زمان میبره تا عضلاتتون یادبگیرن که چی به چیه(بعد از مدتی استفاده از vim واقعا استفاده از ادیتور های معمولی براتون سخت میشه).

چرای بعدی قابلیت شخصی سازی فوق‌علاده‌ی ویم هستش. شما برای هر استفاده‌ای میتونید vim رو به لطف وجود vimscript که یه زبان برنامه نویسی برای شخصی سازی و ساختن پلاگین برای vimـه شخصی سازی کنید. سبک بودن یکی دیگه از ویژگی های vim هستش و برای کسایی که سخت افزار قویی ندادن انتخاب فوق علاده‌ای هستش. البته من دیگه از قابلیت هایی که vim داره و نمیتونید توی ادیتور‌های دیگه بهشون دسترسی داشته باشین مثل register ها و macro ها که ازشون رد میشیم.

نقطه‌ی قوت عجیبش اینکه وقتی وارد ویم میشید نمیتونید تایپ کردن رو شروع کنید. باید اول i رو بزنید بعد شروع کنید علت اینکار وجود سه حالت کلی **command mode** که همونه که اول واردش میشید توش هستید. که کارهایی مختلفی میتونید داخل این مود انجام بدید مثل حذف و بالا و پایین رفتن و کلی کار دیگه. حالت بعدی **insert mode** هست که میتونید توش تایپ کنید و حالت بعدی **visual mode** هست که میتونید متن رو انتخاب کنید.

## از کجا شروع کنم؟

از اونجایی که vim سال ۱۹۹۱ منتشر شد(البته خود vim نسخه‌ی ارتقا یافته‌ی vi که یه ادیتور unix بوده) منابع زیادی برای استفاده وجود داره. بهترین نقطه شروع vimtutor که هم میتونید از سایتش استفاده کنید هم اگه vim رو نصب داشته باشید میتونید ازش توی ترمینال استفاده کنید. همچنین میتونید از بازی <a href="https://vim-adventures.com/" target="_blank" rel="noreferrer noopener">vim adventure</a> استفاده کنید که اونم برای شروع بدک نیست.

اینا منابعی هستن که در طول زمان جمع آوری کردم (البته انگلیسین):

<a href="https://thevaluale.dev/vim-beginner/" target="_blank" rel="noreferrer noopener">Beginner guide</a>

<a href="https://vimhelp.org/" target="_blank" rel="noreferrer noopener">Online-version of the help page</a>

<a href="https://devhints.io/vim" target="_blank" rel="noreferrer noopener">Cheatsheet</a>

<a href="https://vim.fandom.com/wiki/Vim_Tips_Wiki" target="_blank" rel="noreferrer noopener">Tips Wiki</a>

<a href="https://vimawesome.com/" target="_blank" rel="noreferrer noopener">Plugin Database</a>

و میتونید از ویدیو های یوتوب ThePrimeagen و TJ DeVries و البته <a href="https://www.vimconf.live/" target="_blank" rel="noreferrer noopener">VimConf</a> استفاده کنید. اگه انگلیسیتون خوب نیست میتونید از <a href="https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjWn6DklK_0AhU8AhAIHdFGC5gQwqsBegQIBRAB&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DBnfJJtcVFPo&usg=AOvVaw19zSQ4XBbxtK4F0HjES3sP" target="_blank" rel="noreferrer noopener">دوره‌ی ویم جادی</a> استفاده کنید. شاید در آینده خودمم درمورد vim ویدیو ساختم.

همنطور که گفتم میتونید ویم رو شخصی سازی کنید میتونید از <a href="https://github.com/techwithomid/neovim-conf" target="_blank" rel="noreferrer noopener">کانفیگ نئوویم من</a> استفاده کنید.

## صحبت پایانی

من کسی نیستم که بخوام پند برنامه نویسی بدم ولی برنامه‌نویس باید چیز های جدید رو تجربه کنه و ابزارهایی که میتونن بهروری رو بیشتر کنن رو استفاده کنن و vim یکی از این ابزار هاست. مطمئن باشید از وقتی که برای vim میزارید اصلا پیشمون نمی‌شید. و لازم نیست حتما برای کارهای اصلیتون ازش استفاده کنید، برای اسکریپت‌های کوچیک ازش استفاده کنید. حتما لازم نیست بیایین و ادیتور تحت ترمینال ویم رو استفاده کنید!

پلاگین ویم برای همه‌ی ادیتور های و IDE ها وجود داره میتونید نصب کنید و یه مدتی ازش استفاده کنید. اگر فهمیدید واقعا کارکردن باهاش رو دوست ندارید میتونید بدون هیچ دردسری پلاگینش رو غیر فعال کنید و از ادیتور معمولیتون استفاده کنید.

ولی اگه با vim دستتون راه افتاد و دارید از لینوکس استفاده می‌کنید، پیشنهاد می‌کنم حتما از Tilling WM ها مثل i3 استفاده کنید. چون بهره‌وریتون خیلی بیشتر از قبل میشه و tmux رو هم فراموش نکنید که درمورد همه‌ی این ابزار‌ها در آینده بیشتر براتون میگم.

و در نهایت اینا ابزارن و فقط برای بیشتر کردن بهره وری و استفاده هستن. اگه وقتی ابزار بهتری بیاد(که فکر نمیکنم 🙂) از اونا استفاده میکنیم.