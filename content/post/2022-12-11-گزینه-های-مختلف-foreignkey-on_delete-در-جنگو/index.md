---
title: گزینه‌های مختلف ForeignKey on_delete در جنگو
author: امید
type: post
date: 2022-12-11T11:55:27+00:00
url: /گزینه-های-مختلف-foreignkey-on_delete-در-جنگو/
categories:
  - پایتون
  - جنگو
tags:
  - جنگو

---
<figure class="wp-block-image size-full"><img decoding="async" loading="lazy" width="650" height="414" src="https://techwithomid.ir/wp-content/uploads/2022/12/dj-fk.jpg" alt="on_delete در foreignkey" class="wp-image-199" srcset="https://techwithomid.ir/wp-content/uploads/2022/12/dj-fk.jpg 650w, https://techwithomid.ir/wp-content/uploads/2022/12/dj-fk-300x191.jpg 300w" sizes="(max-width: 650px) 100vw, 650px" /></figure> 

foreignkey مدل های جنگو لازمه که مقدار on_delete رو براشون تعریف کنی. و این برای **ForeignKey** و **OneToOne** و **ManyToMany** ها هم صادقه. توی این نوشته مقادیر مختلفی که میتونیم برای on_delete ست کنیم رو با مثال توضیح میدم.

دو تا مدل **Post** و **Comment** رو به شکل زیر تعریف کردم:

<pre class="wp-block-code"><code>class Post(models.Model):
	title = models.CharField(max_length=255)

class Comment(models.Model):
	content = models.TextField()  #👇🏻
	post = models.ForeignKey(Post, on_delete=&#91;?])</code></pre>

توی مثال بالا مدل **Comment** وقتی که **Post** رو حذف می‌کنیم بر اساس مقداری که برای **on_delete** ست کردیم عمل میکنه، و باید توجه داشته باشیم که این کار بصورت برعکس عمل نمیکنه یعنی اگر کامنتی حذف بشه تاثیری روی Post نداره.

حالا که متوجه شدیم جریان از چه قراره بریم که متد ها رو برسی کنیم.

## models.CASCADE

وقتی که این مقدار رو ست میکنیم مدلمون به شکل زیر در میاد:

<pre class="wp-block-code"><code>class Comment(models.Model):
	... 
	post = models.ForeignKey(Post, on_delete=models.CASCADE)</code></pre>

وقتی که ما **post.delete()** رو صدا بزنیم، میره و کامنت ها اون پست رو پاک میکنه.

## models.SET(function or value)

اولین مورد از سه گانه خانواده **models.SET[&#8230;]**. برای این مورد، رابطه **Post** و **Comment** با عقل جور در نمیاد که وقتی پستی پاک میشه کامنت هارو به پست دیگه ارجاع بدیم.

مثالی که بیشتر با عقل جور درمیاد یه **ForeignKey** از **Comment** به کاربر هستش. وقتی که یه کاربر رو حذف میکنیم، ممکنه که بخوایم کامنت هاشون رو حفظ کنیم که مشابهش رو ممکنه توی Reddit دیده باشید.<figure class="wp-block-image size-full">

<img decoding="async" loading="lazy" width="542" height="154" src="https://techwithomid.ir/wp-content/uploads/2022/12/red.png" alt="foreignkey on_delete in reddit deleted user" class="wp-image-194" srcset="https://techwithomid.ir/wp-content/uploads/2022/12/red.png 542w, https://techwithomid.ir/wp-content/uploads/2022/12/red-300x85.png 300w" sizes="(max-width: 542px) 100vw, 542px" /> </figure> 

میتونیم به همچین چیزی با استفاده از **models.SET** به دست بیاریم:

<pre class="wp-block-code"><code>def get_deleted_user_instance():
    return User.objects.get(username='deleted')

class Comment(models.Model):
    ...
    author = models.ForeignKey(User,
            on_delete=models.SET(get_deleted_user_instance))
    #                                 👆🏻 </code></pre>

حالا اگر کاربر رو حذف کنیم، مقدار &#8220;deleted&#8221; جایگزین اون کاربر میشه.

## models.SET_DEFAULT

اینم تقریبا مثل **SET** قبلی کار میکنه با این تفاوت که **SET_DEFAULT** مقدارش رو با **default** که توی مدل تعریف مکنیم جایگزین میکنه.

<pre class="wp-block-code"><code>ANONYMOUS_USER_ID = 1

class Comment(models.Model):
    ...
    author = models.ForeignKey(User, 
            default=ANONYMOUS_USER_ID, 
            on_delete=models.SET_DEFAULT)</code></pre>

## models.SET_NULL

حالا که با خانواده **SET** ها آشنا شدیم دیگه مشخصه که این یکی چیکار میکنه.

البته باید این نکته رم در نظر داشته باشیم که برای اینکه بتونیم از **SET_NULL** استفاده کنیم باید مقدار **null=True** رو برای مدلمون تعریف کرده باشیم.

## models.PROTECT

وقتی که بخوایم **Comment** رو حذف کنیم **PROTECT** برامون ارور بر میگردونه:

<pre class="wp-block-code"><code>class Comment(models.Model):
	... 
	post = models.ForeignKey(Post, on_delete=models.PROTECT)</code></pre>

اگه ما Post درست کنیم میتونیم بدون مشکل اون رو حذف کنیم. ولی اگه یه نفر یه **Comment** بزاره، وقتی که بخوایم کامنت رو حذف کنیم جنگو میاد و ارور **ProtectedError** رو برامون برمیگردونه.

## models.DO_NOTHING

از اسمش مشخصه که چیکار میکنه، هیچکاری نمیکنه. و به شکل زیر پیاده سازی شده که درواقع یه pass هستش:

<pre class="wp-block-code"><code># in django.db.models.deletion
def DO_NOTHING(collector, field, sub_objs, using):
    pass</code></pre>

این میتونه خیلی خطرناک و دردسر ساز باشه چون مدل ممکنه به چیزی اشاره نداشته باش. از این مورد پیشنهاد نمیشه که استفاده بشه مگر اینکه در سطح دیتابیس رابطه هارو تعریف کرده باشید.

## جمع بندی

امیدوارم که یکی دو چیز یادگرفته باشید. بیشتر چیزی که الان درمورد on_delete در foreignkey جنگو خوندید <a href="https://docs.djangoproject.com/en/3.0/ref/models/fields/#django.db.models.ForeignKey.on_delete" target="_blank" rel="noreferrer noopener">توی داکیونت های جنگو</a> نوشته شده ولی مقداری کمتر توضیح داده(همین عکسی که اول پست گذاشتم). و اگه میخواید بیشتر توی این موضوع عمیق بشید سورس کد <a href="https://github.com/django/django/blob/main/django/db/models/deletion.py" target="_blank" rel="noreferrer noopener">on_delete handler</a> جنگو رو یه نگاهی بندازید.