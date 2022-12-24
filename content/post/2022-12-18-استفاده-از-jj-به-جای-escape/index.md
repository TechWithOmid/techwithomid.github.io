---
title: 'ویم تیپ: استفاده از jj به‌جای escape در ویم'
author: امید
type: post
date: 2022-12-17T20:51:06+00:00
url: /استفاده-از-jj-به-جای-escape/
categories:
  - ویم/vim

---
همونطور که توی <a href="https://techwithomid.ir/why-i-use-vim/" target="_blank" rel="noreferrer noopener">پست چرا از ویم استفاده میکنم</a> گفتم من ویم رو خیلی دوست دارم و خب تصمیم گرفتم هر از چندگاهی پست های تحت عنوان ویم تیپ منتشر کنم که در این سری از پست ها تیپ‌هایی برای استفاده بهتر از ویم رو میگم که شما هم بتونید ازش استفاده کنید.

اگه از ویم استفاده می‌کنید میدونید که کلید escape خیلی مهمه چون مارو از حالت insert به حالت نرمال برمیگردونه ولی مشکلی که داره اینکه یکمی دوره و ممکنه کمی ازیت بشید. گرچه مشکل خیلی بزرگی نیست و اگه بهش عادت کنید دیگه مهم نیست براتون ولی خب میتونید با یه تغییر کوچیک توی فایل .vimrc تون خیلی راحت از jj به جای escape استفاده کنید. <figure class="wp-block-image size-large">

<img decoding="async" loading="lazy" width="1024" height="634" src="https://techwithomid.ir/wp-content/uploads/2022/12/image-1024x634.png" alt="" class="wp-image-205" srcset="https://techwithomid.ir/wp-content/uploads/2022/12/image-1024x634.png 1024w, https://techwithomid.ir/wp-content/uploads/2022/12/image-300x186.png 300w, https://techwithomid.ir/wp-content/uploads/2022/12/image-768x475.png 768w, https://techwithomid.ir/wp-content/uploads/2022/12/image-1536x950.png 1536w, https://techwithomid.ir/wp-content/uploads/2022/12/image.png 1647w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

خب تنها کاری که باید بکنید اینکه اگه از ویم استفاده میکنید خط زیر رو به فایل .vimrc اضافه کنید. 

<pre class="wp-block-code"><code>imap jj &lt;Esc></code></pre>

البته میتونید به جای jj از kk یا ترکیب های دیگه استفاده کنید.

الان کافیه که فایل کانفیگ رو سیو کنید و ویم رو دوباره اجرا کنید میبینید که الان میتونید خیلی راحت از jj استفاده کنید و لذت ببرید.