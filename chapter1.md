
# فصل ۱: The Problem of Delivering Software

مهم‌ترین مسئله‌ای که ما به‌عنوان متخصصین نرم‌افزار با آن مواجهیم این است: اگر کسی ایده‌ی خوبی ارائه کند، چگونه می‌توانیم آن را در کوتاه‌ترین زمان ممکن به دست کاربران برسانیم؟ این کتاب نشان می‌دهد چگونه این مشکل را حل کنیم.

ما روی فرایند **build**, **deploy**, **test** و **release** نرم‌افزار تمرکز می‌کنیم، موضوعی که کمتر به آن پرداخته شده است. این بدان معنا نیست که روش‌های توسعه نرم‌افزار مهم نیستند؛ بلکه بدون تمرکز روی سایر جنبه‌های چرخه‌ی عمر نرم‌افزار—جنبه‌هایی که اغلب حاشیه‌ای تلقی می‌شوند—امکان دستیابی به **reliable**, **rapid**, **low-risk** نرم‌افزارهای تولید‌شده و رساندن آن‌ها به دست کاربران به شکلی کارا وجود ندارد.

روش‌های متعددی برای توسعه نرم‌افزار وجود دارد که عموماً روی مدیریت نیازمندی‌ها تمرکز می‌کنند. کتاب‌های بسیار خوبی برای طراحی، توسعه و تست نرم‌افزار منتشر شده‌اند، اما همه‌ی آن‌ها تنها بخش کوچکی از جریان ارزش (value stream) ارائه‌ی نرم‌افزار را پوشش می‌دهند.

**Question** این است که پس از شناسایی نیازمندی‌ها، طراحی، توسعه و تست، چگونه این فعالیت‌ها را به‌صورت یکپارچه و کارآمد به هم متصل کنیم؟ چگونه توسعه‌دهندگان، تست‌کنندگان، تیم‌های build و operations را قادر سازیم به طور مؤثر با هم کار کنند؟ این کتاب یک الگوی مؤثر برای رساندن نرم‌افزار از مرحله‌ی توسعه تا **release** ارائه می‌دهد و تکنیک‌ها و best practices لازم برای اجرای این الگو را توضیح می‌دهد.

الگوی مرکزی این کتاب، **deployment pipeline** است. یک deployment pipeline در واقع پیاده‌سازی خودکار فرایند build، deploy، test و release نرم‌افزار است. هر سازمان ممکن است پیاده‌سازی‌های متفاوتی از این pipeline داشته باشد، اما اصول آن ثابت است.

---

> **شکل ۱.۱**: ساختار کلی Deployment Pipeline  
> هر تغییری در کد، پیکربندی، محیط یا داده‌ها، یک instance جدید از pipeline را راه‌اندازی می‌کند. پس از ساخت باینری‌ها و installers، مجموعه‌ای از تست‌ها اجرا می‌شود تا اطمینان حاصل شود این نسخه قابلیت انتشار دارد. هر تستی که با موفقیت پشت سر گذاشته شود، اعتماد ما را افزایش می‌دهد. در نهایت اگر همه‌ی تست‌ها موفق باشند، نسخه آماده‌ی release است.

---

هدف deployment pipeline سه‌گانه است:
1. **Visibility**: تمام مراحل build، deploy، test و release برای همه‌ی ذینفعان قابل رویت می‌شود.
2. **Feedback**: مشکلات هر چه زودتر شناسایی و رفع می‌شوند.
3. **Push-button Releases**: هر نسخه‌ای از نرم‌افزار را می‌توان به هر محیطی با یک ‌یا چند کلیک منتشر کرد.

### Some Common Release Antipatterns

#### Antipattern: Deploying Software Manually
- **نشانه‌ها**  
  - مستندسازی بسیار گسترده برای فرایند انتشار  
  - تکیه بر تست‌های دستی برای اطمینان از صحت انتشار  
  - تکرار خطاها و calls مکرر به تیم توسعه برای رفع مشکلات  
- **راهکار**  
  کلیه‌ی مراحل deployment باید خودکار شوند. تنها کار لازم انتخاب نسخه و محیط و کلیک روی دکمه‌ی deploy است.

#### Antipattern: Deploying to a Production-like Environment Only after Development Is Complete
- **نشانه‌ها**  
  - اولین بار انتشار به staging پس از پایان توسعه  
  - اختلاف زیاد بین توسعه و production  
- **راهکار**  
  از ابتدا همه‌ی تست‌ها و deployها به‌صورت خودکار و در محیط‌های production-like انجام شوند.

#### Antipattern: Manual Configuration Management of Production Environments
- **نشانه‌ها**  
  - تغییرات پیکربندی مستقیماً در سرورها  
  - عدم امکان بازگشت خودکار به تنظیمات قبلی  
- **راهکار**  
  همه‌ی محیط‌ها (تست، staging، production) با استفاده از اسکریپت‌ها و ابزارهای خودکار و از نسخه کنترل‌شده پیکربندی شوند.

---

## Can We Do Better?
قطعاً. هدف ما ترکیب **deployment pipeline**، خودکارسازی گسترده‌ی تست و deployment و **configuration management** جامع برای ارائه‌ی **push-button releases** در همه‌ی محیط‌هاست.

---

## How Do We Achieve Our Goal?

1. **Every Change Should Trigger the Feedback Process**  
   - تغییر در کد، پیکربندی، محیط یا داده باید pipeline را اجرا کند.  
2. **Fast Feedback**  
   - تست‌ها باید سریع اجرا شوند (کمی < ۵ دقیقه) و مراحل گران‌قیمت‌تر در سخت‌افزارهای ارزان‌تر اجرا شوند.  
3. **Act on Feedback**  
   - تمام ذینفعان (توسعه، تست، عملیات، DBA) باید مرتباً بازخورد را بررسی و اعمال کنند.

---

### Does This Process Scale?
تکنیک‌های lean و DevOps نشان داده‌اند که این الگو حتی در پروژه‌های بزرگ نیز مقیاس‌پذیر است.

### What Are the Benefits?
- **Empowering Teams**: هر کس می‌تواند خود نسخه‌های مختلف را در محیط دلخواه deploy کند.
- **Reducing Errors**: با مدیریت version control و automation، خطاها به شدت کاهش می‌یابند.
