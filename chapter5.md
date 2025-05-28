
# فصل ۵: Anatomy of the Deployment Pipeline

در این فصل، الگوی **deployment pipeline** بررسی می‌شود، که یک فرایند خودکار برای انتقال هر تغییر از **check-in** تا **release** است fileciteturn9file0.

## ۵.۱ What Is a Deployment Pipeline?
**deployment pipeline** یک پیاده‌سازی خودکار از فرایند ساخت، استقرار، تست، و تحویل نرم‌افزار است. این خط تولید شامل چند مرحله اصلی است:
- **Commit Stage**: اطمینان از صحت فنی سیستم با **build** و اجرای تست‌های خودکار (عمدتاً unit tests) و تحلیل کد fileciteturn9file1.
- **Automated Acceptance Tests**: تأیید کارکردهای functional و nonfunctional بر اساس نیازمندی‌های کاربران و مشتری.
- **Manual Test Stages**: ارزیابی usability و کشف باگ‌های باقی‌مانده از طریق exploratory testing، integration testing، و UAT.
- **Release Stage**: تحویل نهایی به کاربران به صورت بسته نرم‌افزاری یا استقرار در محیط staging/production fileciteturn9file1.

## ۵.۲ A Basic Deployment Pipeline
شکل زیر نمایی ساده از یک deployment pipeline را نشان می‌دهد:
1. **Commit**: توسعه‌دهندگان تغییرات را به مخزن نسخه کنترل ارسال می‌کنند.  
2. **Build & Unit Tests**: CI server کد را کامپایل و تست‌های سریع را اجرا می‌کند.  
3. **Artifact Repository**: باینری‌ها و نصب‌کننده‌ها (installers) در یک مخزن artifact ذخیره می‌شوند fileciteturn9file7.  
4. **Automated Acceptance Tests**: تست‌های طولانی‌تر برای تضمین کارکرد صحیح اجرا می‌شوند.  
5. **Branch to Environments**: امکان استقرار خودکار یا دستی در محیط‌های UAT، capacity testing، و production فراهم می‌شود fileciteturn9file6.

## ۵.۳ بک‌آوت و بازگردانی (Back-out)
در صورت بروز مشکل در production، بهترین گزینه این است که نسخه قبلی و معتبر را از ابتدا مجدداً مستقر کنید.  
هرگز از فرآیندهای incremental rollback استفاده نکنید، زیرا تست‌شده نیستند و شکننده‌اند. همیشه یا نسخه قبلی را مجدداً deploy کنید یا از دکمه بازگشت (rollback) خودکار استفاده کنید fileciteturn9file2.

## ۵.۴ Building on Success
هر گاه یک release candidate آماده شود، باید مطمئن باشیم که:
- **کد کامپایل می‌شود**.  
- **Unit tests** پاس شده‌اند.  
- **Acceptance tests** پاس شده‌اند.  
- **پیکربندی محیط** به‌درستی مدیریت شده است.  
- **سیستم استقرار** قبلاً در محیط‌های dev و test مورد استفاده قرار گرفته است.  
- **نسخه کنترل** تمام اطلاعات لازم برای استقرار را نگه می‌دارد fileciteturn9file3.

## ۵.۵ Implementing a Deployment Pipeline
برای پیاده‌سازی تدریجی:
1. **Model Your Value Stream & Create a Walking Skeleton**: نقشه‌برداری از مراحل از check-in تا release fileciteturn9file11.  
2. **Automate Build & Deployment**: اتوماسیون فرآیند build و deploy به محیط UAT اولیه fileciteturn9file12.  
3. **Automate Unit Tests & Code Analysis**: افزودن تست‌های خودکار و تحلیل کد به commit stage fileciteturn9file16.  
4. **Automate Acceptance Tests**: اجرای خودکار acceptance tests پس از هر commit fileciteturn9file19.  
5. **Automate Releases**: امکان deploy خودکار یا دستی به staging و production با احراز هویت مناسب fileciteturn9file17.

## ۵.۶ Deployment Pipeline Practices
- **Only Build Your Binaries Once**: یک‌بار build کنید و همان باینری‌ها را در همه مراحل استفاده کنید fileciteturn9file7.  
- **Separate Configuration from Binaries**: تنظیمات محیط را از کد و باینری‌ها جدا نگه دارید fileciteturn9file8.  
- **Instant Propagation**: هر تغییری فوراً pipeline را از ابتدا تا انتها راه‌اندازی کند fileciteturn9file5.  
- **Stop the Line on Failure**: در صورت خطا در هر مرحله، pipeline بلافاصله متوقف شود fileciteturn9file6.  
- **Self-Service Deployments**: تسترها و عملیات بتوانند builds تاییدشده را به‌دلخواه deploy کنند.  
- **Visible Feedback**: داشبوردهای همیشه فعال برای نمایش وضعیت build و هر مرحله از pipeline fileciteturn9file6.
