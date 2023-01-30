---
title: "استفاده از کلید SSH برای گیتهاب"
url: "ssh-key-for-github"
date: 2023-01-30T20:45:36+03:30
categories: ["گیتهاب"]
tags: ["گیتهاب"]
draft: false
---
## چرا باید از ssh استفاده کنیم؟

هر باری که میخوایم که توی گیتهاب یک کامیتی رو push یا pull کنیم باید بصورت دستی یوزرنیم و پسورد رو وارد کنیم. میتونیم از ssh استفاده کنیم که لازم نباشه هر بار یوزرنیم و پسورد رو وارد کنیم.

کلید ssh بصورت یک جفت public که به گیتهاب میدیم، و یک کلید private که توی کامپیوتر ما ذخیره میشه و نباید اونو به کسی بدیم. اگه این دوتا کلید با هم دیگه همخوانی داشته باشن به گیتهاب دسترسی پیدا می‌کنیم.

رمزنگاری پشت ssh به ما این اطمینان رو میده که کسی نتونه از طریق کلید public، کلید private مارو مهندسی معکوس کنه.

### تولید کلید های SSH

اولین قدم اینکه کلید هامون رو تولید کنیم. ممکنه که همین الانم کلید هارو توی کامپیوترتون داشته باشید. برای چک کردن میتونید به دایرکتوری `.ssh` و یک `ls` بگیرید.

```bash
cd ~/.ssh
ls
```

اگه فایل `id_rsa.pub` رو داشتید دیگه لازم نیست کلید های جدیدی رو تولید کنید. ولی اگه این فایل رو نداشتید با استفاده از دستور زیر استفاده کنید که جفت هارو تولید کنید. و بجای `your@email.com` آدرس ایمیل خودتون رو بزارید.

```bash
ssh-keygen -o -t rsa -C "your@email.com"
```

اگه این دستور برای شما کار نکرد، دستور رو بدون فلگ -o اجرا کنید.


وقتی که دستور بالا رو زدید از شما میپرسه که کجا کلید هارو ذخیره کنه، اینتر بزنید که توی مکان پیشفرض ذخیره بشه.

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/username/.ssh/id_rsa):
```

در این مرحله ازمون میخواد که یه پسورد براش بزاریم که امنیتش بیشتر بشه که این قابلیت رو نمیخوایم پس با دوتا اینتر میزنیم که پسورد نداشته باشه.

```bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

و در نهایت که کارمون تموم شد باید خروجی شبیه به زیر رو داشته باشیم.

```bash
Your identification has been saved in /Users/username/.ssh/id_rsa.
Your public key has been saved in /Users/username/.ssh/id_rsa.pub.
The key fingerprint is:
01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your@email.com
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|        . E +    |
|       . o = .   |
|      . S =   o  |
|       o.O . o   |
|       o .+ .    |
|      . o+..     |
|       .+=o      |
+-----------------+
```

یه راه دیگش اینکه از تصویر رندمی که تولید شده استفاده کنیم ولی توی این روش ما اینکار رو انجام نمیدیم.

## اضافه کردن کلید public به گیتهاب

ما باید به گیتهاب کلید public مون رو بدیم. با استفاده از دستور `cat` محتوای فایل public رو نمایش میدیم.

```bash
$ cat ~/.ssh/id_rsa.pub
```

خروجیمون یه همچین چیزی میشه:

```bash
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA879BJGYlPTLIuc9/R5MYiN4yc/YiCLcdBpSdz
gK9Dt0Bkfe3rSz5cPm4wmehdE7GkVFXrBJ2YHqPLuM1yx1AUxIebpwlIl9f/aUHOts9eVnVh4
NztPy0iSU/Sv0b2ODQQvcy2vYcujlorscl8JjAgfWsO3W4iGEe6QwBpVomcME8IU35v5VbylM
9ORQa6wvZMVrPECBvwItTY8cPWH3MGZiK/74eHbSLKA4PY3gM4GHI450Nie16yggEg2aTQfWA
1rry9JYWEoHS9pJ1dnLqZU3k/8OWgqJrilwSoC5rGjgp93iu0H8T6+mEHGRQe84Nk1y5lESSW
Ibn6P636Bl3uQ== your@email.com
```

خروجی رو کپی میکنیم. و بعدش وارد [github.com](http://github.com) و به بخش تنظیمات میریم.

{{<figure src="images/gh-setting.png" alt="github settings">}}

و بعد وارد بخش SSH and GPG keys میشیم.

{{<figure src="images/gh-ssh-gpg-keys.png" alt="github ssh keys settings">}}

بعد روی `New SSH key` کلیک می‌کنیم. توی بخش title یه اسمی دلخواهی رو براش انتخاب می‌کنیم و در بخش key کلیدی رو که کپی کردیم رو اونجا پیست می‌کنیم.

{{<figure src="images/gh-new-ssh-key.png" alt="adding new ssh key to github">}}

و در نهایت `Add SSH key` رو میزنیم. و اگه ازتون پسورد خواست پسورد رو وارد میکنید و کار تمومه.

## استفاده از کلید SSH

برای clone کردن ریپوزیتوری ها بهتره از این به بعد اون هارو با ssh کلون کنید کافیه مثل تصویر زیر عمل کنید.

{{<figure src="images/gh-ssh-clone.png" alt="clone github repo with ssh">}}

و تمومه دیگه از این به بعد میتونید خیلی راحت از ssh به جای https برای clone, push, pull استفاده کنید. همچنین از ssh میشه به سرور هم وصل شد که تقریبا پروسه به همین شکله ولی دیگه به جای اینکه public key به گیتهاب اضافه کنید به سرورتون اضافه کنید.
