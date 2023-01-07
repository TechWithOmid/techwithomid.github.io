---
title: مدیریت درایور مرورگر برای استفاده از سیلینیوم پایتون
author: امید
description: "برای سلینیوم لازمه که درایور مورد نیاز رو بصورت دستی نصب کنید اما با استفاده از این آموزش دیگه نیازی به این کار نیست."
type: post
date: 2021-05-13T15:32:14+00:00
url: /manage-selenium-browser-driver/
categories:
  - پایتون
tags:
  - web scripting
  - پایتون
  - سلینیوم

---
یه مدت پیش داشتم روی پروژه‌ی کوچیکی <a href="https://github.com/techwithomid/shad-bot" data-type="URL" data-id="https://github.com/techwithomid/shad-bot" target="_blank" rel="noreferrer noopener">(این پروژه)</a> کار میکردم که یه بات بود که میتونست توی کلاس های شاد توی یه زمان مشخص یه پیغامی رو بفرسته میتونید از گیت‌هاب پروژه رو بصورت رایگان استفاده کنید و مشارکت کنید.

شروع کردم به نوشتن پروژه و همچی خوب پیش میرفت و از اونجایی که سلینیوم لازم داره که درایور یکی از مرورگر ها رو داشته باشه بصورت دستی رفتم درایور کروم رو دانلود کردم و در مسیری از سیستم‌ عامل قرار دادم و اون رو به سلینیوم دادم. بعدش توی گیت‌هاب یه ‌issue گرفتم که مشکل این بود که درایور نبود و کاربر باید میرفت اون رو دستی دانلود میکرد خواستم و چون هیچ ایده‌ای نداشتم چه جوری این کار رو بصورت اتوماتیک انجام بدم خواستم یه اسکریپت دیگه بنویسم که بصورت خودکار بره و درایور رو دانلود کنه و خب برای اینکار لازم داشتم بگردم و مرورگری که رو سیستم کاربر نصب هست رو پیدا کنم بعد برم درایور رو دانلود کنم ولی فهمیدم که یه پکیج خیلی خوب و کاربردی برای اینکار وجود داره و منطقی نیست که دوباره چرخ رو اختراع کنیم. و از اونجایی که برای خودم مفید بود میخوام اونم اینجا بزارم و نحوه‌ی استفادش رو براتون توضیح بدم.

در حالت عادی ما باید چنین کاری رو انجام بدیم:

<pre class="wp-block-code"><code>driver = webdriver.Chrome(executable_path="/path/to/binary/chromedriver")</code></pre>

یا اگه از فایرفاکس استفاده می‌کنید:

<pre class="wp-block-code"><code>driver = webdriver.Firefox(executable_path="/path/to/binary/firefoxdriver")</code></pre>

ولی اگه درایور وجود نداشته باشه و کاربر اطلاعی نداشته باشه ازش دردسر میشه و ارور میگره و برنامه کار نمیکنه برای همین از پکیجی به اسم webdriver_manager استفاده میکنیم.که کارش اینکه عملیات دانلود داریور و قابل استفاده کردن اون(executeable کردنش) رو اتوماتیک کنه.



برای استفاده کافیه که با استفاده از دستور زیر اون رو نصب کنید:

<pre class="wp-block-code"><code>pip install webdriver_manager</code></pre>

حالا که پکیج رو نصب کردیم کافیه که به باتوجه به مرورگر مورد استفاده از یکی از روش های زیر استفاده کنید.

کروم:

<pre class="wp-block-code"><code>from webdriver_manager.chrome import ChromeDriverManager
from selenium import webdriver

driver = webdriver.Chrome(executable_path=ChromeDriverManager().install())
driver.get("http://www.google.com/")
print(driver.title)
driver.quit()</code></pre>

فایرفاکس:

<pre class="wp-block-code"><code>from webdriver_manager.firefox import GeckoDriverManager
from selenium import webdriver

driver = webdriver.Firefox(executable_path=GeckoDriverManager().install())
driver.get("http://www.google.com/")
print(driver.title)
driver.quit()</code></pre>

مرورگر Edge:

<pre class="wp-block-code"><code>from webdriver_manager.firefox import GeckoDriverManager
from selenium import webdriver

driver = webdriver.Firefox(executable_path=GeckoDriverManager().install())
driver.get("http://www.google.com/")
print(driver.title)
driver.quit()</code></pre>

مرورگر IE:

<pre class="wp-block-code"><code>from webdriver_manager.microsoft import IEDriverManager
from selenium import webdriver

driver = webdriver.Ie(executable_path=IEDriverManager().install())
driver.get("http://www.google.com/")
print(driver.title)
driver.quit()</code></pre>

الته باید به این نکته توجه کرد که پکیج webdriver_manager بصورت پیشفرض آخرین نسخه درایور رو دانلود میکنه و برای اینکه مشخص کنید که چه ورژنی رو دانلود کنه از روش زیر استفاده می‌کنیم:

<pre class="wp-block-code"><code>webdriver.Chrome(executable_path=ChromeDriverManager("2.42").install())</code></pre>

و در آخر یک تشکر برای Sergey Pirogov برای نوشتن این پکیج کاربردی که این عملیات کسل کننده و بعضی اوقات دردسر ساز رو برامون حل کردن.