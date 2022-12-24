---
title: فایل gitignore برای پروژه های جنگو
author: امید
type: post
date: 2021-06-10T18:35:25+00:00
url: /gitignore-file-for-django-projects/
categories:
  - git
  - پایتون
  - جنگو
tags:
  - git
  - پایتون
  - جنگو

---
اگه از گیت به عنوان ورژن کنترل استفاده کرده باشید به فایلی به اسم .gitignore برخورد کردید یا حداقل اسمش رو جایی شنیدید یا دیدید. کار فایل gitignore اینکه فایل هایی که مهم نیستند و نباید داخل repository گیت باشند رو نادیده بگیره و اون هارو به گیت اضافه کنه. مثل فایل های virtural environmet و فایل های .pyc این فایل ها اهمیتی ندارند و هر وقت پروژه رو جایی بخواید اجرا کنید این فایل ها هم ایجاد میشه. برای همین لزومی نداره که داخل repository باشن.

فایل‌ها و دایرکتوری‌های زیادی هستن که لازم نیستن یا نباید داخل repository باشند، برای مثال تنظیمات vscode (البته اگه ازشون استفاده کنید) یا فایل env (برای ذخیره متغییر های محیطی که دارای اطلاعات حساسی هستن). من اینجا لیستی رو تهیه کردم که می‌تونید به فایل .gitignore خودتون اضافه کنید.

<pre class="wp-block-code"><code># Django #
*.log
*.pot
*.pyc
__pycache__
db.sqlite3
media

# Backup files # 
*.bak 

# If you are using PyCharm # 
.idea/**/workspace.xml 
.idea/**/tasks.xml 
.idea/dictionaries 
.idea/**/dataSources/ 
.idea/**/dataSources.ids 
.idea/**/dataSources.xml 
.idea/**/dataSources.local.xml 
.idea/**/sqlDataSources.xml 
.idea/**/dynamic.xml 
.idea/**/uiDesigner.xml 
.idea/**/gradle.xml 
.idea/**/libraries 
*.iws /out/ 

# Python # 
*.py&#91;cod] 
*$py.class 

# Distribution / packaging 
.Python build/ 
develop-eggs/ 
dist/ 
downloads/ 
eggs/ 
.eggs/ 
lib/ 
lib64/ 
parts/ 
sdist/ 
var/ 
wheels/ 
*.egg-info/ 
.installed.cfg 
*.egg 
*.manifest 
*.spec 

# Installer logs 
pip-log.txt 
pip-delete-this-directory.txt 

# Unit test / coverage reports 
htmlcov/ 
.tox/ 
.coverage 
.coverage.* 
.cache 
.pytest_cache/ 
nosetests.xml 
coverage.xml 
*.cover 
.hypothesis/ 

# Jupyter Notebook 
.ipynb_checkpoints 

# pyenv 
.python-version 

# celery 
celerybeat-schedule.* 

# SageMath parsed files 
*.sage.py 

# Environments 
.env 
.venv 
env/ 
venv/ 
ENV/ 
env.bak/ 
venv.bak/ 

# mkdocs documentation 
/site 

# mypy 
.mypy_cache/ 

# Sublime Text # 
*.tmlanguage.cache 
*.tmPreferences.cache 
*.stTheme.cache 
*.sublime-workspace 
*.sublime-project 

# sftp configuration file 
sftp-config.json 

# Package control specific files Package 
Control.last-run 
Control.ca-list 
Control.ca-bundle 
Control.system-ca-bundle 
GitHub.sublime-settings 

# Visual Studio Code # 
.vscode/* 
!.vscode/settings.json 
!.vscode/tasks.json 
!.vscode/launch.json 
!.vscode/extensions.json 
.history</code></pre>

انیجا متوجه میشید که migration هارو به این لیست اضافه نکردم چون معمولا میخوام migration هام با من باشن برای همین اینجا اونارو نذاشتم ولی میتونید که به انتهای لیست اونا رو اضافه کنید.

ولی فایل هایی با پسوند .pyc که پایتون هربار کد شمارو به بایت کد تبدیل میکنه که خروجی اون فایل هایی با پسوند .pyc هستش. با اون فایل ها کار زیادی نمی‌تونید بکنید برای همین نیازی بهشون نیست(البته میشه اون هارو اجرا کرد چون همون فایل پایتونی شما هستن که کامپایل شدن که در آینده درمورد این فایل صحبت می کنم).