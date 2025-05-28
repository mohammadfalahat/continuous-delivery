
# فصل ۱۱: مدیریت زیرساخت و محیط‌ها

## ۱۱.۱ مقدمه

مهم‌ترین گام در برنامه‌ریزی انتشار، گردآوری نمایندگان تمام بخش‌های درگیر در فرایند delivery—تیم‌های build، infrastructure، operations، تست، DBA و پشتیبانی—در یک جلسه است. این افراد باید در طول پروژه به‌طور منظم دور هم جمع شوند و همواره برای بهینه‌سازی delivery process همکاری کنند fileciteturn41file0.

## ۱۱.۲ مراحل سه‌گانه‌ی استقرار

همان‌طور که در Chapter 1 توضیح دادیم، سه مرحله اصلی برای deploy نرم‌افزار وجود دارد:
1. **ایجاد و مدیریت infrastructure** که نرم‌افزار روی آن اجرا می‌شود (شامل hardware, networking, middleware و external services)  
2. **نصب نسخه‌ی صحیح نرم‌افزار** روی آن  
3. **پیکربندی application**، شامل هر داده یا state موردنیاز  

این فصل به مرحله‌ی اول می‌پردازد. از آنجا که هدف ما این است که تمام testing environments (از جمله CI environments) production-like باشند، به‌طور ضمنی مدیریت environments تستی نیز در همین فصل بررسی خواهد شد fileciteturn41file0.

## ۱۱.۳ تعریف Environment

در اینجا، environment به تمام منابع موردنیاز برای اجرای application و تنظیمات آن گفته می‌شود. ویژگی‌های یک environment عبارت‌اند از:
- **سخت‌افزار**: تعداد و نوع CPU، میزان حافظه، تعداد spindles، NICها و شبکه‌ی متصل‌کننده‌ی آنها  
- **پیکربندی OS و middleware**: مانند messaging systems, application servers, web servers, database servers  
- **زیرساخت سازمانی (infrastructure)**: سرویس‌هایی مانند DNS, firewalls, routers, version control, storage, monitoring, mail servers و غیره fileciteturn41file0.

## ۱۱.۴ اصول مدیریت Holistic زیرساخت

فرایند آماده‌سازی و مدیریت محیط‌ها پس از deploy بر دوش مدیریت جامع infrastructure است که بر اساس اصول زیر بنا شده:
1. **Desired State** زیرساخت باید با configuration version-controlled مشخص شود.  
2. **Autonomic Infrastructure**: زیرساخت باید خودکار خود را به وضعیت مطلوب برساند.  
3. **Instrumentation & Monitoring**: وضعیت واقعی زیرساخت همیشه با مانیتورینگ رصد شود.  
4. **Automated Provisioning**: امکان بازتولید سریع یک known-good configuration در صورت بروز خطا فراهم باشد fileciteturn41file0.

## ۱۱.۵ مدیریت موارد کلیدی

برای کاهش ریسک استقرار در production-like environments باید موارد زیر را به‌دقت مدیریت کرد:
- **Operating System و پیکربندی آن** در همه‌ی environments  
- **Middleware software stack** و تنظیمات آن (application servers, messaging, databases)  
- **Infrastructural software** مانند مخازن version control, directory services و monitoring systems  
- **نقاط یکپارچه‌سازی خارجی** (external systems & services)  
- **شبکه** (routers, firewalls, switches, DNS, DHCP و غیره)  
- **تعامل تیم Development با تیم Infrastructure**  

برای حل مشکلات، این دو تیم باید از ابتدای پروژه در همه‌ی فعالیت‌های مدیریت environment و deployment همکاری کنند fileciteturn41file0.

## ۱۱.۶ DevOps و تولید محیط‌های تست شبیه production

تمرکز بر collaboration جزو اصول DevOps است—جهت آوردن رویکرد agile به system administration و IT operations. همچنین استفاده از تکنیک‌های autonomic infrastructure و behavior-driven monitoring از دستاوردهای این حرکت است. تست environments باید مشابه production بوده و تکنیک‌های مدیریت آنها یکسان باشد fileciteturn41file0.

## ۱۱.۷ ابزارها و تکنیک‌ها

در حالی که این کار ممکن است پرهزینه و پیچیده باشد، ابزارهایی مانند virtualization و automated data center management می‌توانند به تسریع آن کمک کنند. مزایای catching مشکلات پیکربندی و integration در مراحل اولیه، ارزش این تلاش را چندین برابر می‌کند.

## ۱۱.۸ یادداشت پایانی

گرچه فرض شده که تولید (production) زیرنظر operations team است، اصول مشابه برای **software products** نیز کاربرد دارد. برای مثال، backup و recovery برای کاربران نهایی اهمیت دارد و نیازمند توجه به non-functional requirements مانند recoverability، supportability و auditability است fileciteturn41file0.
