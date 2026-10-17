# 📘 آموزش جامع Git از صفر تا حرفه‌ای

> **نسخه‌ها:** [English edition](./Git-Zero-to-Hero-EN.md) · [صفحه‌ی اصلی پروژه](./README.md)


> یک راهنمای فارسی و کاربردی برای یادگیری Git؛ از اولین ریپازیتوری تا کار تیمی، حل تعارض‌ها، بازنویسی تاریخچه و خودکارسازی گردش‌کار توسعه.
>
> **تهیه و تنظیم: Royatvand**

این راهنما برای یادگیری مرحله‌به‌مرحله نوشته شده است. بهتر است دستورها را در یک پروژه‌ی آزمایشی اجرا کنید و به‌خصوص پیش از استفاده از دستورهای مخرب، وضعیت ریپازیتوری را بررسی کنید.

---

## 📑 فهرست مطالب

1. [Git چیست؟](#1-git-چیست)
2. [نصب و پیکربندی](#2-نصب-و-پیکربندی)
3. [مفاهیم اصلی Git](#3-مفاهیم-اصلی-git)
4. [ساخت اولین ریپازیتوری](#4-ساخت-اولین-ریپازیتوری)
5. [چرخه‌ی روزانه‌ی کار](#5-چرخهی-روزانهی-کار)
6. [دیدن تغییرات و تاریخچه](#6-دیدن-تغییرات-و-تاریخچه)
7. [مدیریت فایل‌های نادیده‌گرفته‌شده](#7-مدیریت-فایلهای-نادیدهگرفتهشده)
8. [بازگردانی تغییرات](#8-بازگردانی-تغییرات)
9. [Branch یا شاخه](#9-branch-یا-شاخه)
10. [ادغام شاخه‌ها با Merge](#10-ادغام-شاخهها-با-merge)
11. [حل Merge Conflict](#11-حل-merge-conflict)
12. [آشنایی با Rebase](#12-آشنایی-با-rebase)
13. [کار با Remote](#13-کار-با-remote)
14. [Clone، Fetch، Pull و Push](#14-clone-fetch-pull-و-push)
15. [ذخیره‌ی موقت تغییرات با Stash](#15-ذخیرهی-موقت-تغییرات-با-stash)
16. [مدیریت نسخه‌ها با Tag](#16-مدیریت-نسخهها-با-tag)
17. [انتقال Commit با Cherry-pick](#17-انتقال-commit-با-cherry-pick)
18. [بازیابی با Reflog](#18-بازیابی-با-reflog)
19. [پیداکردن Commit مشکل‌ساز با Bisect](#19-پیداکردن-commit-مشکلساز-با-bisect)
20. [آشنایی با Submodule](#20-آشنایی-با-submodule)
21. [خودکارسازی با Git Hooks](#21-خودکارسازی-با-git-hooks)
22. [ساختار داخلی Git](#22-ساختار-داخلی-git)
23. [نوشتن پیام Commit مناسب](#23-نوشتن-پیام-commit-مناسب)
24. [گردش‌کارهای تیمی](#24-گردشکارهای-تیمی)
25. [Pull Request و Code Review](#25-pull-request-و-code-review)
26. [آشنایی مقدماتی با GitHub Actions](#26-آشنایی-مقدماتی-با-github-actions)
27. [دستورهای کاربردی پیشرفته](#27-دستورهای-کاربردی-پیشرفته)
28. [اشتباهات متداول](#28-اشتباهات-متداول)
29. [برگه‌ی تقلب دستورات](#29-برگهی-تقلب-دستورات)
30. [مسیر پیشنهادی ادامه‌ی یادگیری](#30-مسیر-پیشنهادی-ادامهی-یادگیری)

---

## 1. Git چیست؟

Git یک **سیستم کنترل نسخه‌ی توزیع‌شده** است. با آن می‌توان تغییرات فایل‌های یک پروژه را در طول زمان ثبت کرد، نسخه‌های قبلی را بررسی کرد و با اطمینان بیشتری به‌صورت تیمی توسعه داد.

با Git می‌توانید:

- بفهمید چه چیزی تغییر کرده و تغییر در کدام Commit ثبت شده است.
- در صورت نیاز به نسخه‌ی قبلی پروژه برگردید.
- روی یک قابلیت جدید در شاخه‌ای جداگانه کار کنید.
- تغییرات چند توسعه‌دهنده را با هم ترکیب کنید.
- تاریخچه‌ی توسعه را بررسی و اشکال‌زدایی کنید.

### Git با GitHub چه تفاوتی دارد؟

| مورد | Git | GitHub |
|---|---|---|
| ماهیت | ابزار کنترل نسخه | سرویس میزبانی ریپازیتوری و همکاری |
| محل استفاده | معمولاً روی سیستم شخصی | سرویس آنلاین |
| اینترنت | بسیاری از عملیات‌ها بدون اینترنت ممکن‌اند | برای امکانات آنلاین به اینترنت نیاز دارد |
| نمونه‌ی جایگزین | Mercurial | GitLab، Bitbucket و Gitea |

**خلاصه:** Git تاریخچه‌ی تغییرات را مدیریت می‌کند؛ GitHub راهی برای میزبانی و همکاری روی پروژه‌های Git فراهم می‌کند.

---

## 2. نصب و پیکربندی

### نصب در سیستم‌عامل‌های مختلف

**Windows:** Git را از [سایت رسمی Git](https://git-scm.com/download/win) دریافت و نصب کنید. پس از نصب می‌توانید از Git Bash، ترمینال VS Code یا PowerShell استفاده کنید.

**Ubuntu / Debian:**

```bash
sudo apt update
sudo apt install git
```

**Fedora:**

```bash
sudo dnf install git
```

**macOS با Homebrew:**

```bash
brew install git
```

برای بررسی نصب:

```bash
git --version
```

### تعیین نام و ایمیل

Git نام و ایمیل نویسنده را در Commitها ذخیره می‌کند:

```bash
git config --global user.name "Royatvand"
git config --global user.email "you@example.com"
```

ایمیل نمونه را با ایمیل خودتان جایگزین کنید. اگر می‌خواهید تنظیم فقط روی یک پروژه اعمال شود، داخل همان ریپازیتوری `--global` را حذف کنید.

### تنظیمات مفید

```bash
# نام پیش‌فرض شاخه‌ی جدید
git config --global init.defaultBranch main

# رنگی‌کردن خروجی
git config --global color.ui auto

# مشاهده‌ی تنظیمات
 git config --list

# مشاهده‌ی مقدار یک تنظیم خاص
git config user.name
```

برای ساخت میان‌بر:

```bash
git config --global alias.st status
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.lg "log --oneline --graph --all --decorate"
```

پس از آن `git st` معادل `git status` خواهد بود.

---

## 3. مفاهیم اصلی Git

در ابتدا سه بخش مهم را بشناسید:

```text
Working Directory  --git add-->  Staging Area  --git commit-->  Repository
     فایل‌ها                         تغییرات آماده             تاریخچه‌ی ثبت‌شده
```

### Working Directory

پوشه‌ی واقعی پروژه است؛ همان فایل‌هایی که در VS Code باز می‌کنید و ویرایش می‌کنید.

### Staging Area

منطقه‌ی آماده‌سازی Commit است. با `git add` مشخص می‌کنید کدام تغییرات در Commit بعدی قرار بگیرند.

### Repository

تاریخچه‌ی ثبت‌شده‌ی پروژه در پوشه‌ی `.git` نگهداری می‌شود. `git commit` وضعیت آماده‌شده را به‌عنوان نقطه‌ای در تاریخچه ثبت می‌کند.

### اصطلاحات پرکاربرد

| اصطلاح | معنی ساده |
|---|---|
| Repository / Repo | پروژه‌ای که Git تاریخچه‌اش را دنبال می‌کند |
| Commit | ثبت یک وضعیت از پروژه در تاریخچه |
| Branch | مسیر جداگانه برای توسعه |
| HEAD | نشان می‌دهد در حال حاضر روی کدام Commit یا شاخه هستید |
| Remote | نسخه‌ای از ریپازیتوری در مکان دیگر، مانند GitHub |
| Origin | نام رایج Remote اصلی |
| Merge | ترکیب تاریخچه‌ی دو شاخه |
| Conflict | تعارضی که نیاز به انتخاب یا ترکیب دستی تغییرات دارد |
| Hash | شناسه‌ی Commit یا شیء Git |
| Working tree | فایل‌ها و پوشه‌های فعلی پروژه |

---

## 4. ساخت اولین ریپازیتوری

### شروع پروژه از صفر

```bash
mkdir first-git-project
cd first-git-project
git init
```

`git init` پوشه‌ی `.git` را می‌سازد و آن پوشه را به ریپازیتوری Git تبدیل می‌کند.

### افزودن فایل و ثبت اولین Commit

```bash
echo "# First Git Project" > README.md
git status
git add README.md
git commit -m "docs: add initial README"
```

### کپی‌کردن پروژه‌ی موجود

```bash
git clone https://github.com/OWNER/REPOSITORY.git
```

`OWNER` و `REPOSITORY` را با مالک و نام ریپازیتوری واقعی عوض کنید. معمولاً `clone` فایل‌ها، تاریخچه و تنظیم Remote به نام `origin` را ایجاد می‌کند.

---

## 5. چرخه‌ی روزانه‌ی کار

در بسیاری از پروژه‌ها، این چرخه بارها تکرار می‌شود:

1. وضعیت را بررسی کنید.
2. فایل‌ها را تغییر دهید.
3. تغییرات را بازبینی کنید.
4. موارد مناسب را Stage کنید.
5. یک Commit با پیام روشن بسازید.

### دستورهای اصلی

```bash
git status                  # وضعیت فایل‌ها
git add src/app.js          # آماده‌سازی یک فایل
git add .                   # آماده‌سازی تغییرات پوشه‌ی فعلی
git add -A                  # آماده‌سازی تغییرات کل ریپازیتوری
git commit -m "feat: add search form"
git log --oneline           # تاریخچه‌ی خلاصه
```

`git add .` و `git add -A` را با توجه به پوشه‌ای که در آن هستید و دامنه‌ی تغییرات انتخاب کنید. قبل از Commit، اجرای `git status` عادت خوبی است.

### Commit چه فایده‌ای دارد؟

Commitهای کوچک و معنادار باعث می‌شوند تاریخچه قابل فهم‌تر باشد و پیدا کردن علت یک باگ آسان‌تر شود. بهتر است هر Commit یک تغییر منطقی را ثبت کند.

---

## 6. دیدن تغییرات و تاریخچه

```bash
git diff                  # تغییرات Stage نشده
git diff --staged         # تغییرات آماده‌ی Commit
git show HEAD              # جزئیات Commit فعلی
git log                    # تاریخچه‌ی کامل
git log --oneline          # تاریخچه‌ی خلاصه
git log --oneline --graph --all --decorate
git log --follow -- src/app.js   # تاریخچه‌ی فایل، حتی پس از تغییر نام
```

برای مقایسه‌ی دو Commit:

```bash
git diff COMMIT_A COMMIT_B
```

برای بررسی اینکه هر خط آخرین بار در کدام تغییر آمده است:

```bash
git blame src/app.js
```

`git blame` لزوماً نشان نمی‌دهد چه کسی از نظر مسئولیت مقصر بوده است؛ فقط اطلاعات ثبت‌شده‌ی خط‌ها را نمایش می‌دهد.

---

## 7. مدیریت فایل‌های نادیده‌گرفته‌شده

فایل‌هایی مانند وابستگی‌های نصب‌شده، خروجی Build، لاگ‌ها و کلیدهای محلی معمولاً نباید وارد Git شوند. برای آن‌ها فایل `.gitignore` بسازید.

نمونه برای پروژه‌های JavaScript و Python:

```gitignore
# Dependencies
node_modules/

# Python
__pycache__/
.venv/
venv/

# Build output
dist/
build/

# Environment secrets
.env
.env.*
!.env.example

# Logs and operating-system files
*.log
.DS_Store
Thumbs.db
```

**نکته‌ی امنیتی:** `.gitignore` به‌تنهایی فایلی را که قبلاً Track شده از Git خارج نمی‌کند. برای حذف از فهرست Track، بدون حذف فایل محلی:

```bash
git rm --cached path/to/file
```

اگر رمز یا کلید محرمانه‌ای قبلاً Push شده است، صرفاً حذف آن از Commit کافی نیست؛ کلید را باطل یا تعویض کنید و در صورت نیاز تاریخچه را طبق روال امن پاک‌سازی کنید.

---

## 8. بازگردانی تغییرات

دستور مناسب بستگی دارد به اینکه تغییرات در کدام مرحله باشند. قبل از اجرای دستورهای بازگردانی، `git status` و در صورت نیاز `git diff` را اجرا کنید.

### دور انداختن تغییرات فایلِ Stage نشده

```bash
git restore src/app.js
```

این دستور تغییرات ثبت‌نشده‌ی فایل را به نسخه‌ی موجود در Index برمی‌گرداند؛ در حالت معمول، تغییرات محلی آن فایل از دست می‌رود.

### خارج‌کردن فایل از Staging

```bash
git restore --staged src/app.js
```

فایل از Staging خارج می‌شود، اما تغییرات آن در Working Directory باقی می‌ماند.

### لغو آخرین Commit محلی

نگه‌داشتن تغییرات به‌صورت Stage شده:

```bash
git reset --soft HEAD~1
```

نگه‌داشتن تغییرات، اما خارج‌کردن آن‌ها از Staging:

```bash
git reset --mixed HEAD~1
```

حذف Commit و تغییرات فایل‌ها:

```bash
git reset --hard HEAD~1
```

> ⚠️ `reset --hard` می‌تواند تغییرات محلی را از بین ببرد. فقط وقتی اجرا کنید که دقیقاً می‌دانید چه چیزی حذف می‌شود و نسخه‌ی پشتیبان لازم را دارید.

### برگرداندن Commit منتشرشده

برای ایجاد Commit جدیدی که تغییرات یک Commit قبلی را معکوس کند:

```bash
git revert COMMIT_HASH
```

در شاخه‌های مشترک، `revert` اغلب انتخاب امن‌تری از بازنویسی تاریخچه با `reset` است.

---

## 9. Branch یا شاخه

شاخه راهی برای پیش‌برد توسعه‌ی مستقل از مسیر اصلی پروژه است. می‌توانید روی یک قابلیت یا رفع باگ کار کنید و پس از بررسی، تغییرات را ادغام کنید.

```bash
git branch                       # شاخه‌های محلی
git branch -a                    # شاخه‌های محلی و Remote
git branch feature/profile       # ساخت شاخه
git switch feature/profile       # رفتن به شاخه
git switch -c feature/search     # ساخت و جابه‌جایی هم‌زمان
git branch -m old-name new-name  # تغییر نام شاخه
git branch -d feature/profile    # حذف شاخه‌ی ادغام‌شده
```

روش قدیمی‌تر `git checkout` نیز وجود دارد:

```bash
git checkout feature/profile
git checkout -b feature/search
```

نام‌گذاری شاخه‌ها را روشن و یکدست نگه دارید:

```text
feature/login-page
fix/navbar-overlap
hotfix/payment-error
refactor/api-client
```

برای حذف اجباری یک شاخه‌ی ادغام‌نشده، `git branch -D` وجود دارد؛ اما قبل از آن مطمئن شوید Commitهای مورد نیاز را از دست نمی‌دهید.

---

## 10. ادغام شاخه‌ها با Merge

وقتی کار یک شاخه آماده شد، می‌توانید آن را در شاخه‌ی مقصد ادغام کنید:

```bash
git switch main
git merge feature/search
```

دو حالت متداول:

- **Fast-forward:** اگر شاخه‌ی مقصد Commit جدید مستقلی نداشته باشد، اشاره‌گر آن جلو می‌رود.
- **Three-way merge:** اگر هر دو شاخه تغییرات مستقل داشته باشند، Git از نقطه‌ی مشترک و دو سر شاخه برای ادغام استفاده می‌کند و ممکن است Merge Commit بسازد.

برای حفظ یک Merge Commit حتی در حالت Fast-forward:

```bash
git merge --no-ff feature/search
```

بعد از ادغام موفق، شاخه‌ی موقت را در صورت عدم نیاز می‌توان حذف کرد:

```bash
git branch -d feature/search
```

---

## 11. حل Merge Conflict

Conflict زمانی رخ می‌دهد که Git نتواند تغییرات را بدون تصمیم انسانی ترکیب کند. در فایل متعارض ممکن است نشانه‌هایی شبیه این ببینید:

```text
<<<<<<< HEAD
نسخه‌ی شاخه‌ی فعلی
=======
نسخه‌ی شاخه‌ی ادغام‌شونده
>>>>>>> feature/search
```

مراحل حل:

1. با `git status` فایل‌های متعارض را پیدا کنید.
2. فایل را باز کنید و تصمیم بگیرید کدام تغییر یا چه ترکیبی از تغییرات لازم است.
3. نشانگرهای تعارض را حذف و محتوای نهایی را ذخیره کنید.
4. تست مناسب را اجرا کنید.
5. فایل حل‌شده را Stage کنید و عملیات را کامل کنید.

```bash
git add src/app.js
git commit
```

اگر Merge هنوز تکمیل نشده و می‌خواهید آن را لغو کنید:

```bash
git merge --abort
```

در حل تعارض صرفاً یکی از طرفین را به‌صورت خودکار انتخاب نکنید؛ ممکن است هر دو طرف بخشی از منطق مورد نیاز را داشته باشند.

---

## 12. آشنایی با Rebase

`rebase` Commitهای شاخه‌ی جاری را بر پایه‌ی جدیدی دوباره اعمال می‌کند. این کار می‌تواند تاریخچه‌ای خطی‌تر ایجاد کند، اما شناسه‌ی Commitهای بازنویسی‌شده عوض می‌شود.

```bash
git switch feature/search
git fetch origin
git rebase origin/main
```

اگر Conflict ایجاد شد، فایل‌ها را اصلاح و سپس اجرا کنید:

```bash
git add src/app.js
git rebase --continue
```

برای لغو Rebase در حال اجرا:

```bash
git rebase --abort
```

### Rebase یا Merge؟

- برای به‌روزکردن شاخه‌ی شخصی و منتشرنشده، Rebase می‌تواند تاریخچه را مرتب نگه دارد.
- برای ادغام شاخه‌ی تیمی، سیاست پروژه را دنبال کنید.
- تاریخچه‌ی شاخه‌ای را که دیگران بر اساس آن کار می‌کنند، بدون هماهنگی بازنویسی نکنید.

اگر پس از Rebase لازم شد تاریخچه‌ی شاخه‌ی Remote را به‌روزرسانی کنید، ابتدا اثر آن را بررسی کنید. `--force-with-lease` از `--force` محتاطانه‌تر است، اما همچنان باید با آگاهی استفاده شود.

---

## 13. کار با Remote

Remote نسخه‌ای از ریپازیتوری است که معمولاً روی سرویس میزبانی قرار دارد.

```bash
git remote -v
```

افزودن Remote:

```bash
git remote add origin https://github.com/OWNER/REPOSITORY.git
```

تغییر نشانی:

```bash
git remote set-url origin https://github.com/OWNER/NEW-REPOSITORY.git
```

حذف Remote از تنظیمات محلی:

```bash
git remote remove origin
```

این دستور فقط پیوند Remote را از تنظیمات ریپازیتوری محلی حذف می‌کند؛ ریپازیتوری روی سرویس میزبانی را حذف نمی‌کند.

### اتصال پروژه‌ی محلی به GitHub

1. در GitHub یک ریپازیتوری بسازید.
2. داخل پوشه‌ی پروژه دستورهای زیر را اجرا کنید:

```bash
git init
git add .
git commit -m "chore: initial commit"
git branch -M main
git remote add origin https://github.com/OWNER/REPOSITORY.git
git push -u origin main
```

اگر پروژه از قبل تاریخچه یا Remote دارد، پیش از اجرای این مراحل وضعیتش را بررسی کنید تا تاریخچه‌ی ناخواسته یا تکراری ایجاد نشود.

---

## 14. Clone، Fetch، Pull و Push

### Clone

کپی‌کردن یک ریپازیتوری موجود روی سیستم:

```bash
git clone https://github.com/OWNER/REPOSITORY.git
```

### Fetch

گرفتن اطلاعات جدید Remote بدون ادغام آن‌ها در شاخه‌ی فعلی:

```bash
git fetch origin
```

پس از آن می‌توانید اختلاف شاخه‌ی محلی و Remote را بررسی کنید:

```bash
git log --oneline main..origin/main
git diff main origin/main
```

### Pull

معمولاً اطلاعات Remote را می‌گیرد و با شاخه‌ی جاری ادغام می‌کند:

```bash
git pull origin main
```

برای استفاده از Rebase به‌جای Merge در Pull:

```bash
git pull --rebase origin main
```

### Push

ارسال Commitهای محلی به Remote:

```bash
git push origin main
```

برای انتشار اولین بار یک شاخه و تنظیم Upstream:

```bash
git push -u origin feature/search
```

بعد از تنظیم Upstream، اغلب `git push` کافی است.

---

## 15. ذخیره‌ی موقت تغییرات با Stash

`stash` برای نگه‌داشتن موقت تغییرات نیمه‌تمام مفید است؛ مثلاً وقتی باید به شاخه‌ی دیگری بروید ولی هنوز تغییرات را نمی‌خواهید Commit کنید.

```bash
git stash push -m "WIP: search component"
git stash list
git stash apply             # اعمال تغییرات و نگه‌داشتن stash
git stash pop               # اعمال و حذف stash در صورت موفقیت
git stash drop stash@{0}    # حذف یک stash مشخص
```

برای شامل‌کردن فایل‌های Untracked:

```bash
git stash push -u -m "WIP including new files"
```

پیش از اجرای `drop` یا `clear` مطمئن شوید دیگر به تغییرات ذخیره‌شده نیاز ندارید.

---

## 16. مدیریت نسخه‌ها با Tag

Tag معمولاً برای علامت‌گذاری یک نسخه‌ی مشخص نرم‌افزار استفاده می‌شود.

```bash
git tag v1.0.0
```

تگ توضیح‌دار:

```bash
git tag -a v1.0.0 -m "First stable release"
```

دیدن تگ‌ها و اطلاعات آن‌ها:

```bash
git tag
git show v1.0.0
```

انتشار یک تگ به Remote:

```bash
git push origin v1.0.0
```

انتشار همه‌ی تگ‌ها:

```bash
git push origin --tags
```

حذف تگ محلی:

```bash
git tag -d v1.0.0
```

برای حذف تگ منتشرشده نیز باید دستور جداگانه‌ی Remote را اجرا کنید و مطمئن باشید حذف آن با سیاست پروژه سازگار است.

---

## 17. انتقال Commit با Cherry-pick

`cherry-pick` تغییرات یک یا چند Commit مشخص را روی شاخه‌ی جاری اعمال می‌کند؛ بدون اینکه کل شاخه‌ی مبدأ ادغام شود.

```bash
git switch main
git cherry-pick COMMIT_HASH
```

برای چند Commit:

```bash
git cherry-pick HASH_1 HASH_2
```

در صورت تعارض، فایل‌ها را حل و Stage کنید، سپس:

```bash
git cherry-pick --continue
```

لغو عملیات جاری:

```bash
git cherry-pick --abort
```

از Cherry-pick برای انتقال تغییر مستقل، مثلاً یک رفع باگ مشخص، استفاده کنید. برای ادغام همه‌ی کار یک شاخه، Merge یا Rebase معمولاً خواناتر است.

---

## 18. بازیابی با Reflog

`git reflog` تغییرات اشاره‌گرهای محلی مانند `HEAD` را ثبت می‌کند. اگر پس از Reset یا جابه‌جایی اشتباه، Commitی از تاریخچه‌ی عادی ناپدید شد، Reflog می‌تواند به پیدا کردن آن کمک کند.

```bash
git reflog
```

ابتدا شناسه‌ی Commit موردنظر را پیدا کنید و پیش از دست‌کاری تاریخچه، می‌توانید یک شاخه‌ی پشتیبان از آن بسازید:

```bash
git branch recovery-branch COMMIT_HASH
```

اگر پس از بررسی تصمیم گرفتید به آن وضعیت برگردید، روش مناسب را انتخاب کنید. `git reset --hard` فایل‌های فعلی را تغییر می‌دهد؛ بدون بررسی وضعیت فعلی آن را اجرا نکنید.

Reflog محلی است و برای همیشه تضمین نمی‌شود؛ بنابراین جایگزین نسخه‌ی پشتیبان نیست.

---

## 19. پیداکردن Commit مشکل‌ساز با Bisect

وقتی می‌دانید یک نسخه‌ی قدیمی سالم بوده و نسخه‌ی فعلی مشکل دارد، `bisect` به‌صورت جست‌وجوی دودویی محدوده را کوچک می‌کند.

```bash
git bisect start
git bisect bad                 # نسخه‌ی فعلی مشکل دارد
git bisect good v1.0.0         # نسخه‌ی قدیمی سالم است
```

Git به Commit میانی می‌رود. تست را اجرا کنید و نتیجه را اعلام کنید:

```bash
git bisect good
# یا
git bisect bad
```

این روند تا پیدا شدن Commit مشکل‌ساز ادامه می‌یابد. در پایان:

```bash
git bisect reset
```

اگر پروژه تستی خودکار و قابل‌اعتماد داشته باشد، امکان استفاده از `git bisect run` هم وجود دارد.

---

## 20. آشنایی با Submodule

Submodule یک ریپازیتوری Git دیگر را در مسیر مشخصی از ریپازیتوری اصلی ثبت می‌کند. این روش زمانی کاربرد دارد که پروژه به کدی وابسته باشد که تاریخچه‌ی مستقل خودش را دارد.

```bash
git submodule add https://github.com/OWNER/LIBRARY.git vendor/library
```

برای Cloneکردن پروژه‌ای که Submodule دارد:

```bash
git clone --recurse-submodules https://github.com/OWNER/PROJECT.git
```

اگر پروژه قبلاً Clone شده است:

```bash
git submodule update --init --recursive
```

Submoduleها به کمی دقت اضافه نیاز دارند؛ برای وابستگی‌های معمول برنامه، ابتدا بررسی کنید آیا Package Manager زبان پروژه گزینه‌ی مناسب‌تری است یا نه.

---

## 21. خودکارسازی با Git Hooks

Hook اسکریپتی است که در زمان مشخصی از عملیات Git اجرا می‌شود؛ مثلاً قبل از Commit یا Push. از آن می‌توان برای اجرای تست، فرمت‌کردن کد یا بررسی پیام Commit استفاده کرد.

Hookهای محلی معمولاً در مسیر زیر هستند:

```text
.git/hooks/
```

چند نمونه‌ی رایج:

| Hook | کاربرد متداول |
|---|---|
| `pre-commit` | بررسی یا تست قبل از Commit |
| `commit-msg` | اعتبارسنجی پیام Commit |
| `pre-push` | اجرای بررسی‌ها قبل از Push |
| `post-merge` | اجرای اقداماتی پس از Merge |

Hookها را می‌توان برای کاهش خطا به کار برد، اما نباید تنها سد امنیتی پروژه باشند. از آنجا که پوشه‌ی داخلی `.git/hooks` معمولاً همراه پروژه Clone نمی‌شود، برای اشتراک‌گذاری Hookها از ابزارها یا تنظیمات پروژه‌ای مناسب استفاده کنید.

---

## 22. ساختار داخلی Git

Git فقط فهرستی از نسخه‌های کامل فایل‌ها نیست؛ ساختار داخلی آن از چند نوع شیء اصلی تشکیل شده است:

| شیء | نقش |
|---|---|
| Blob | محتوای فایل |
| Tree | فهرست فایل‌ها و پوشه‌های یک وضعیت از پروژه |
| Commit | اشاره به Tree، اطلاعات ثبت و Commitهای والد |
| Tag | اشاره‌ی نام‌گذاری‌شده به یک شیء، معمولاً یک Commit |

چند دستور برای کنجکاوی بیشتر:

```bash
git cat-file -t HEAD
git cat-file -p HEAD
git ls-tree HEAD
```

`HEAD` معمولاً به شاخه‌ی جاری و از طریق آن به Commit فعلی اشاره می‌کند. در حالت **Detached HEAD**، HEAD مستقیماً به یک Commit اشاره می‌کند، نه به شاخه. اگر در این حالت می‌خواهید کار تازه‌ای را ادامه دهید، ساخت یک شاخه‌ی جدید راه امن‌تری است:

```bash
git switch -c experiment-from-old-commit
```

---

## 23. نوشتن پیام Commit مناسب

پیام Commit باید خلاصه و قابل‌فهم باشد. به‌جای پیام‌های کلی مثل `update` یا `fix`، دقیقاً بگویید چه تغییری انجام شده است.

نمونه‌های بهتر:

```text
feat: add article search
fix: prevent empty form submission
docs: explain local setup
refactor: simplify API client
test: cover login validation
```

### الگوی Conventional Commits

```text
<type>(<scope اختیاری>): <توضیح کوتاه>
```

نوع‌های رایج:

| نوع | کاربرد |
|---|---|
| `feat` | قابلیت جدید |
| `fix` | رفع خطا |
| `docs` | مستندات |
| `style` | تغییرات قالب‌بندی بدون تغییر منطق |
| `refactor` | بازآرایی کد |
| `test` | تست‌ها |
| `chore` | کارهای نگه‌داری |
| `perf` | بهبود عملکرد |

قاعده‌ی تیم را رعایت کنید؛ پیام‌های خوب باید درک تغییر را ساده کنند، نه اینکه صرفاً از یک قالب پیروی کنند.

---

## 24. گردش‌کارهای تیمی

سه الگوی شناخته‌شده عبارت‌اند از:

### GitHub Flow

- شاخه‌ی اصلی باید در وضعیت مناسب انتشار باقی بماند.
- برای قابلیت یا رفع باگ، شاخه‌ی کوتاه‌عمر بسازید.
- تغییرات را در قالب Pull Request بررسی کنید.
- پس از تأیید و گذراندن بررسی‌های لازم، ادغام کنید.

### Git Flow

در پروژه‌هایی با چرخه‌ی انتشار مشخص، ممکن است شاخه‌هایی مانند `main`، `develop`، `feature/*`، `release/*` و `hotfix/*` استفاده شوند. این مدل ساختارمندتر است، اما مدیریت بیشتری می‌خواهد.

### Trunk-Based Development

توسعه‌دهندگان تغییرات کوچک و پرتکرار را روی شاخه‌ی اصلی یا شاخه‌های بسیار کوتاه‌عمر ادغام می‌کنند. این مدل به تست خودکار قوی و هماهنگی تیمی نیاز دارد.

**انتخاب مدل باید با اندازه‌ی تیم، روش انتشار و کیفیت تست‌ها متناسب باشد.** هیچ گردش‌کاری برای همه‌ی پروژه‌ها بهترین نیست.

---

## 25. Pull Request و Code Review

Pull Request (PR) راهی برای پیشنهاد، بحث و بررسی تغییرات پیش از ادغام در شاخه‌ی مقصد است. PR قابلیت پلتفرم‌هایی مانند GitHub و GitLab است و جزو دستورهای پایه‌ی Git محسوب نمی‌شود.

یک روند معمول:

```bash
git switch -c feature/profile
# پیاده‌سازی و تست تغییرات
git add .
git commit -m "feat: add profile page"
git push -u origin feature/profile
```

سپس در پلتفرم میزبانی، Pull Request ایجاد کنید.

### PR خوب چه چیزهایی دارد؟

- عنوان مشخص و توضیح علت تغییر
- خلاصه‌ی راه‌حل
- دستورها یا نتیجه‌ی تست‌ها
- تصویر یا ویدئو، وقتی ظاهر رابط کاربری تغییر کرده است
- اشاره به Issue مرتبط در صورت وجود

### بررسی کد

در Code Review، روی درستی منطق، خوانایی، امنیت، تست‌پذیری و اثر تغییر تمرکز کنید. هدف یافتن راه‌حل بهتر است، نه فقط اصلاح سلیقه‌ای سبک کدنویسی.

روش‌های رایج ادغام PR:

- **Merge commit:** تاریخچه‌ی شاخه و Commitهای آن حفظ می‌شود.
- **Squash and merge:** تغییرات شاخه در یک Commit جمع می‌شوند.
- **Rebase and merge:** Commitها به‌صورت خطی روی شاخه‌ی مقصد اعمال می‌شوند.

روش مناسب را طبق استاندارد پروژه انتخاب کنید.

---

## 26. آشنایی مقدماتی با GitHub Actions

GitHub Actions به اجرای گردش‌کار خودکار در واکنش به رویدادهایی مانند Push و Pull Request کمک می‌کند. برای نمونه، می‌توان تست‌ها را روی هر PR اجرا کرد.

فایل گردش‌کار معمولاً در مسیری شبیه این قرار می‌گیرد:

```text
.github/workflows/ci.yml
```

نمونه‌ی ساده برای اجرای دستورهای بررسی یک پروژه‌ی Node.js:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  checks:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test
```

این نمونه فرض می‌کند پروژه فایل Lock و اسکریپت `test` مناسب دارد. نسخه‌ی Actionها و نسخه‌ی Node.js را با نیازهای فعلی پروژه هماهنگ کنید.

---

## 27. دستورهای کاربردی پیشرفته

### پیدا کردن Commit با پیام یا نویسنده

```bash
git log --grep="search"
git log --author="Royatvand"
git log --since="2 weeks ago"
```

### بررسی تفاوت شاخه‌ها

```bash
git diff main...feature/search
git log --oneline main..feature/search
```

### تغییر نام فایل تحت مدیریت Git

```bash
git mv old-name.js new-name.js
git commit -m "refactor: rename module"
```

### پاک‌سازی فایل‌های Untracked

ابتدا فقط پیش‌نمایش بگیرید:

```bash
git clean -n
```

حذف واقعی فایل‌های Untracked:

```bash
git clean -f
```

این دستور می‌تواند فایل‌های محلی را حذف کند. پیش از استفاده، خروجی پیش‌نمایش را کامل بررسی کنید.

### دیدن تنظیمات یک Remote

```bash
git remote show origin
```
---

## 28. اشتباهات متداول

### «چرا فایل در GitHub دیده نمی‌شود؟»

```bash
git status
git add path/to/file
git commit -m "docs: add missing file"
git push
```

مطمئن شوید فایل در `.gitignore` قرار نگرفته و Commit روی همان شاخه‌ای است که منتشر می‌کنید.

### «چرا Push رد می‌شود؟»

ممکن است Remote Commitهایی داشته باشد که محلی ندارید. ابتدا تغییرات را دریافت و بررسی کنید:

```bash
git fetch origin
git log --oneline --graph --all
git pull --rebase origin main
```

این مثال برای زمانی است که شاخه‌ی شما `main` است و Rebase با گردش‌کار پروژه سازگار است؛ در صورت داشتن تغییرات محلی، قبل از ادغام وضعیت را بررسی کنید.

### «Commit اشتباهی زدم»

- اگر هنوز منتشر نشده، `git reset` با گزینه‌ی مناسب ممکن است کمک کند.
- اگر Commit منتشر شده یا دیگران از آن استفاده می‌کنند، `git revert` معمولاً گزینه‌ی امن‌تری است.

### «فایل حساس را Commit کرده‌ام»

- کلید، رمز یا Token را فوراً باطل یا تعویض کنید.
- فایل حساس را از رهگیری خارج کنید و `.gitignore` را اصلاح کنید.
- در صورت نیاز، با برنامه‌ریزی و اطلاع‌رسانی تاریخچه را پاک‌سازی کنید.
- حذف فایل از یک Commit جدید، به‌تنهایی اطلاعات محرمانه را از تاریخچه‌ی قبلی پاک نمی‌کند.

### «روی شاخه‌ی اشتباه Commit زدم»

قبل از اجرای دستورهای انتقال، شناسه‌ی Commit را پیدا کنید و وضعیت شاخه‌ها را بررسی کنید. گاهی `cherry-pick` برای انتقال همان Commit کافی است. از اجرای سریع Reset یا حذف شاخه بدون نسخه‌ی پشتیبان خودداری کنید.

---

## 29. برگه‌ی تقلب دستورات

| کار | دستور |
|---|---|
| بررسی وضعیت | `git status` |
| دیدن تغییرات | `git diff` |
| Stageکردن فایل | `git add FILE` |
| ثبت Commit | `git commit -m "message"` |
| تاریخچه‌ی خلاصه | `git log --oneline --graph` |
| ساخت شاخه | `git switch -c BRANCH` |
| تغییر شاخه | `git switch BRANCH` |
| Mergeکردن | `git merge BRANCH` |
| دریافت اطلاعات Remote | `git fetch` |
| دریافت و ادغام | `git pull` |
| ارسال Commitها | `git push` |
| ذخیره‌ی موقت | `git stash push` |
| بازگردانی Commit منتشرشده | `git revert HASH` |
| مشاهده‌ی Reflog | `git reflog` |
| ساخت Tag توضیح‌دار | `git tag -a v1.0.0 -m "message"` |
| بررسی Remoteها | `git remote -v` |

### چرخه‌ی ساده‌ی روزانه

```bash
git status
git diff
git add .
git diff --staged
git commit -m "feat: describe the change"
git push
```

این ترتیب یک الگوی عمومی است؛ پیش از `git add .` مطمئن شوید فایل‌های ناخواسته یا محرمانه را وارد Staging نمی‌کنید.

---

## 30. مسیر پیشنهادی ادامه‌ی یادگیری

برای یادگیری ماندگار، صرفاً دستورها را حفظ نکنید؛ آن‌ها را در یک ریپازیتوری آزمایشی تمرین کنید.

### مرحله‌ی اول: پایه‌ها

- `init`، `status`، `add`، `commit` و `log`
- `diff` و `.gitignore`
- ساخت شاخه، جابه‌جایی و Merge ساده

### مرحله‌ی دوم: همکاری با Remote

- `clone`، `fetch`، `pull` و `push`
- ساخت شاخه‌ی قابلیت و Push آن
- ایجاد Pull Request و بررسی تغییرات

### مرحله‌ی سوم: مدیریت موقعیت‌های دشوار

- حل Conflict
- تفاوت `reset`، `restore` و `revert`
- تمرین `stash`، `reflog` و `cherry-pick`
- آشنایی با Rebase و خطر بازنویسی تاریخچه‌ی مشترک

### تمرین نهایی

1. یک پروژه‌ی کوچک بسازید و آن را با Git مدیریت کنید.
2. یک شاخه برای قابلیت جدید بسازید و چند Commit کوچک ثبت کنید.
3. یک تغییر متفاوت در `main` ایجاد کنید و آن را با شاخه‌ی قابلیت ادغام کنید.
4. عمداً یک Conflict ساده بسازید و آن را حل کنید.
5. پروژه را روی GitHub منتشر و برای تغییرات یک Pull Request ایجاد کنید.
6. یک فایل CI ساده برای اجرای تست‌ها اضافه کنید.

---

## ✅ جمع‌بندی

Git فقط مجموعه‌ای از دستورها نیست؛ ابزاری برای ثبت تصمیم‌های فنی، مدیریت ریسک تغییرات و همکاری مؤثر است. پایه‌ها را خوب تمرین کنید، Commitهای کوچک و خوانا بسازید و دستورهای مخرب را فقط پس از بررسی کامل وضعیت ریپازیتوری اجرا کنید.

اگر این راهنما برایتان مفید بود، می‌توانید آن را در قالب یک ریپازیتوری آموزشی توسعه دهید و با مثال‌ها، تمرین‌ها و اصلاحات جدید کامل‌تر کنید.