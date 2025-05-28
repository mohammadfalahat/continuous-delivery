# فصل ۱۴: Advanced Version Control

## ۱۴.۱ سه دلیل branching
تیم‌های توسعه ممکن است برای مدیریت وضعیت کد و کنترل هم‌زمان تغییرات به دلایل زیر نیاز به **branch** کردن داشته باشند:
1. **Release branches**: وقتی نسخه‌ای از نرم‌افزار را منتشر می‌کنید، با باز کردن یک branch مجزا امکان اعمال **bug fix**ها بر روی نسخه‌ای پایدار فراهم می‌شود، در حالی که توسعه ویژگی‌های جدید در **mainline** ادامه می‌یابد. پس از رفع اشکالات، تغییرات را به **mainline** و pipeline اصلی merge می‌کنند fileciteturn52file0.  
2. **Spike branches**: برای آزمایش سریع یک ایده یا پیاده‌سازی موقت (مثلاً proof of concept)، ایجاد یک **spike branch** پیشنهاد می‌شود. این branch پس از آزمون و تصمیم‌گیری discard می‌شود.  
3. **Large refactorings**: در موارد نادر که نمی‌توان تغییرات گسترده را به صورت incremental یا با استفاده از **branch by abstraction** انجام داد، یک branch کوتاه‌مدت برای تطبیق کلی ساختار ایجاد می‌شود و سپس merge خواهد شد fileciteturn52file0.

## ۱۴.۲ تاریخچه مختصر Revision Control
پدر version controlها، **SCCS** (Source Code Control System)، در سال ۱۹۷۲ توسط Marc J. Rochkind توسعه یافت. سپس سیستم‌های **RCS** و **CVS** از آن مشتق شدند و هنوز هم کاربرد دارند. این سیستم‌ها امکان ذخیره تاریخچه فایل‌ها و تاریخچه تغییرات را فراهم می‌کنند fileciteturn52file0.

### ۱۴.۲.۱ CVS
**CVS** (Concurrent Versions System) که از RCS پیروی می‌کند، برای اولین بار در اواسط دههٔ ۱۹۸۰ عرضه شد. ویژگی‌های کلیدی آن عبارت‌اند از:
- مدل client-server برای ردیابی تغییرات  
- پشتیبانی از branching و tagging  
- **Concurrent** بودن به معنی برداشت قفل روی فایل‌ها و تمرکز بر **optimistic lock** fileciteturn52file0.  
با این حال، مشکلاتی از جمله حجم زیاد در branching و conflicts مصنوعی در merge دارد.

## ۱۴.۳ Version Control Systems متمرکز و توزیع‌شده
**Subversion** (SVN) نمونه‌ای از سیستم‌های متمرکز است که برخی محدودیت‌ها دارد:
- نیاز به اتصال آنلاین برای commit  
- metadata محلی در دایرکتوری‌های **.svn** پراکنده می‌شود  
- عملیات کلاینتی غیراتمی و امکان ناسازگاری در working copy  
- شمارهٔ revision محدود به یک repository خاص است fileciteturn51file14.  
در مقابل، **DVCS** (مانند **Git** و **Mercurial**) امکان commit آفلاین، clone کامل repository و merge هوشمند را فراهم می‌کنند.

## ۱۴.۴ Commercial Version Control Systems
برخی ابزارهای تجاری توصیه‌شده:
- **Perforce**: مقیاس‌پذیری و performance بالا  
- **AccuRev**: پشتیبانی از stream-based development بدون پیچیدگی ClearCase  
- **BitKeeper**: نخستین DVCS تجاری  
- **TFS** (Team Foundation Server): ادغام با Visual Studio (اما در مقایسه با Perforce محدودتر است) fileciteturn51file0.

## ۱۴.۵ Switch Off Pessimistic Locking
در صورت پشتیبانی سیستم نسخه‌بندی از **optimistic locking**، بهتر است قفل‌های انحصاری (pessimistic locks) را غیرفعال کنید. این کار از تاخیر در توسعه جلوگیری کرده و conflicts خودکار را به حداقل می‌رساند fileciteturn51file0.

## ۱۴.۶ استفاده از Version Control
- **عدم ذخیره باینری‌ها**: خروجی کامپایل نباید در repository نگهداری شود؛ چرا که قابل‌تولید مجدد است و حجم زیادی دارد fileciteturn52file6.  
- **Check in منظم** به **trunk**: ورود تغییرات کوچک و پیوسته به mainline از پیچیدگی merge و ریسک افزایش زمان build می‌کاهد. توصیه می‌شود از ایجاد branch برای کارهای روزمره پرهیز کنید، مگر در سه موقعیت توضیح داده‌شده در ابتدای فصل fileciteturn52file7.  
