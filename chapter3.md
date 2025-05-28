
# فصل ۳: Continuous Integration

Continuous Integration (CI) روشی است که با اجرای خودکار فرایند **build** و اجرای تست‌های اتوماتیک روی هر تغییر در کد، اطمینان حاصل می‌کند که نرم‌افزار همیشه در وضعیت عملیاتی قرار دارد fileciteturn4file1.

## ۳.۱ پیش‌نیازها

### Version Control
کلیه‌ی موارد پروژه شامل code، tests، اسکریپت‌های پایگاه‌داده، build و deployment باید در یک مخزن **version control** قرار گیرند fileciteturn4file2.

### An Automated Build
امکان اجرای فرایند build و تست از خط فرمان باید وجود داشته باشد. این اسکریپت‌ها باید مستقل از IDE باشند و بتوانند به صورت خودکار اجرا شوند fileciteturn4file3.

### Agreement of the Team
Continuous Integration یک **practice** است، نه صرفاً ابزار. تیم باید متعهد باشد commitهای کوچک و مکرر به **mainline** داشته باشد و اولویت اول، رفع فوری هرگونه failure در build باشد fileciteturn4file8.

## ۳.۲ پیاده‌سازی سیستم پایه‌ی Continuous Integration

سیستم CI به طور دوره‌ای یا پس از هر commit، مخزن version control را poll کرده، کد را checkout می‌کند، build و تست‌های commit stage را اجرا می‌کند و نتیجه را گزارش می‌دهد fileciteturn4file7.

### روند ساده
1. بررسی کنید آیا build در حال اجراست؛ اگر بله، منتظر بمانید تا تمام شود.
2. در صورت شکست build، ابتدا مشکل را روی local ماشین خود رفع کنید.
3. پس از گذشتن تست‌ها، کد را pull کرده و local build و تست‌ها را اجرا کنید.
4. در صورت موفقیت، commit کنید و منتظر اجرای build روی CI شوید.
5. اگر CI build شکست خورد، بلافاصله رفع خطای لازم را انجام دهید و مجدداً اقدام کنید fileciteturn4file18.

## ۳.۳ Suggested Practices

### Check In Regularly
commitهای کوچک و مکرر در **mainline** باعث کاهش خطر conflict و تسهیل rollback می‌شود fileciteturn4file19.

### Test-Driven Development
برای دستیابی به **coverage** بالا و **fast feedback**، Test-Driven Development را به کار ببرید fileciteturn4file9.

### XP Practices
با استفاده از **refactoring** و **shared code ownership**، Continuous Integration مؤثرتر می‌شود fileciteturn4file10.

## ۳.۴ کار در تیم‌های توزیع‌شده
برای تیم‌های چندمکانی، باید از ابزارهایی مانند VoIP و IM برای هماهنگی استفاده کرد. CI همچنان یکسان است، ولی **discipline** بیشتری نیاز دارد fileciteturn4file11.

## ۳.۵ Centralized Continuous Integration
سیستم CI می‌تواند به صورت یک سرویس متمرکز ارائه شود تا تیم‌های بزرگ خود سرویس CI را **self-service** کنند. استفاده از **virtualization** جهت Provision خودکار VM‌ها مفید است fileciteturn4file17.

## ۳.۶ مسائل فنی و رویکردهای جایگزین
- مشکلات **bandwidth** بین مراکز توسعه: استفاده از DVCS یا تقسیم پروژه به **components** می‌تواند کمک کند fileciteturn4file4.
- رویکرد جایگزین: CI و VCS محلی در شرایط اضطراری، اما کمتر توصیه می‌شود fileciteturn4file13.

## ۳.۷ پیشینه Continuous Integration
قبل از CI، **nightly builds** و **rolling builds** مرسوم بود که مشکلات traceability داشتند fileciteturn4file16.
