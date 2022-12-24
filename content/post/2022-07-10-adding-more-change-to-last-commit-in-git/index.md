---
title: اضافه کردن تغییرات بیشتر در git به کامیت قبلی
author: امید
type: post
date: 2022-07-09T19:46:39+00:00
excerpt: با استفاده از دستور git amend میتونید تغییراتی که ایجاد کردید رو به کامیت قبلی git اضافه کنید. که در ادامه بیشتر در این مورد توضیح دادم...
url: /adding-more-change-to-last-commit-in-git/
categories:
  - git
  - برنامه نویسی
tags:
  - git
  - گیتهاب

---
امروز داشتم کار میکردم که تغییرات رو توی git کامیت کردم و دوباره یکسری تغییرات ایجاد کردم که خواستم روی کامیت قبلی بره و نمیخواستم یه کامیت دیگه بزنم برای همین یه سرچ زدم و برام جالب بود که git این قابلیت رو هم داره. همینطور که <a href="https://fa.wikipedia.org/wiki/%D9%84%DB%8C%D9%86%D9%88%D8%B3_%D8%AA%D9%88%D8%B1%D9%88%D8%A7%D9%84%D8%AF%D8%B2" target="_blank" rel="noreferrer noopener">لینوس توروالدز</a> توسعه دهنده git میگه حتی خودمم کامل git رو بلد نیستم.

برای اینکار لازم نیست که کار خیلی پیچیده‌ای انجام بدید. فقط کافیه که تغییراتی که لازم دارید رو انجام بدید و وقتی که میخواید کامیت کنید، از یکی دو فلگ اضافه‌تر استفاده می‌کنید که این پایین براتون توضیح میدم که چی به چیه.

سناریو رو اینجوری در نظر میگیریم که داریم رو پروژه کار می‌کنیم و کامیت هامون به شکل زیره(کامیت های قدیمی‌تر بالاتر قرار دارن):

<pre class="wp-block-code"><code>f7f3f6d create file_a class and methods
310154e improve SomeOtherClass code
a5f4a0d update changelog file</code></pre>

ولی ما یادمون رفته که یه خطی رو به کامیت آخر، یعنی این کامیت a5f4a0d انجام اضافه کنیم. راه حل اولی که به ذهن خودم رسید این بود که تغییراتی که لازم بود انجام بدم و یادم رفته بود رو اضافه کنم و یه کامیت جدید بزنم که کار جالبی نبود. و کامیت هامون به شکل زیر در میومد:

<pre class="wp-block-code"><code>f7f3f6d create file_a class and methods
310154e improve SomeOtherClass code
a5f4a0d update changelog file
a4gx124 add missing line to changelog</code></pre>

تغییرات دوتا کامیت آخر در واقع یکیه و ممکنه در طولانی مدت یادتون بده و بگید اینجا چیکار کردم بجای این میتونید از دستور **amend** توی git استفاده کنید.

## مقدمات دستور git amend

اول از همه فایلی که میخوایم تغییر بدیم رو به git اضافه می‌کنیم:

<pre class="wp-block-code"><code>git add changelog.md</code></pre>

و بعد از اون amendش می‌کنیم:

<pre class="wp-block-code"><code>git commit --amend</code></pre>

بعد از اینکه این دستور رو اجرا کردید فایلی شبیه به فایل زیر براتون توی ویم یا ادیتور که خودتون انتخاب کردید باز میشه:

<pre class="wp-block-code"><code>update changelog file
# Please enter the commit message for your changes. Lines starting
# with ‘#’ will be ignored, and an empty message aborts the commit.
#
# Author: John Doe &lt;john@doe.com&gt;
# Date: Thu Apr 21 22:40:30 2016 -0300
#
# On branch some_branch
# Your branch is up-to-date with ‘origin/some_branch’.
#
# Changes to be committed:
# modified: changelog.md</code></pre>

اینجا میتونید یسری تغییرات بدید و message کامیت خودتون رو تغییر بدید و اگه نخواستید فایل رو سیو کنید و خارج بشید. 

ولی اگه نمیخواید message کامیت رو عوض کنید دیگه لازم نیست فایل رو باز کنید و ذخیره کنید و خارج بشید، کافیه فقط دستور زیر رو کپی کنید:

<pre class="wp-block-code"><code>git commit --amend --no-edit</code></pre>

و تمام.

## پوش کردن کامیت amend

اگه کامیت قبلی رو پوش نکرده باشید خیلی سادست لازم نیست کار اضافه‌ای رو انجام بدید فقط پوش کنید. اما اگه کامیت قبلی رو پوش کردید، یعنی این کامیت a5f4a0d و از اونجایی که کامیت رو تغییر دادید باید از فلگ -f استفاده کنید.

<pre class="wp-block-code"><code>git push -f origin main</code></pre>

## تغییر دادن message کامیت

کار ساده‌ای کافیه از روش زیر استفاده کنید.

<pre class="wp-block-code"><code>git commit --amend -m "Your new commit message"</code></pre>



اگه می‌خواید بیشتر درمورد git amend بخونید میتونید سری به داکیومنت خود [گیت][1] در این مورد بزنید.

 [1]: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History