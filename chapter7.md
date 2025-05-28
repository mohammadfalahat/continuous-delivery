
# فصل ۷: The Commit Stage

## ۷.۱ مقدمه
Commit Stage اولین گام رسمی در **deployment pipeline** است که کیفیت را فراتر از حوزه‌ی یک توسعه‌دهنده‌ی منفرد می‌برد. در این مرحله، تغییرات وارده با خط اصلی (mainline) ادغام شده و یک «ویراستاری خودکار» روی نرم‌افزار اجرا می‌شود تا خطاها هر چه زودتر شناسایی شوند. برای رعایت اصل **fail fast**، Commit Stage باید بیشترین خطاهای احتمالیِ معرفی‌شده توسط توسعه‌دهندگان را شکار کند، اما در عین حال در صورت امکان تا انتها اجرا شده و گزارشی از تمام خطاها ارائه دهد fileciteturn17file3.

## ۷.۲ چه چیزهایی باید باعث شکست Commit Stage شوند؟
به‌طور سنتی، Commit Stage در شرایط زیر شکست می‌خورد:
- **خطا در کامپایل**: اگر کد نتواند کامپایل شود.
- **شکست تست‌ها**: شامل commit tests (بیشتر unit tests) و تست‌های اختصاصی این مرحله.
- **مشکل محیطی**: مانند عدم دسترسی به منابع موردنیاز یا خطای پیکربندی.  
علاوه بر این موارد پایه، می‌توان کیفیت کد را نیز معیار شکست یا هشدار قرار داد. برای مثال:
- کاهش پوشش تست (test coverage) زیر یک آستانه‌ی مشخص.
- افزایش تعداد warnings یا تکرار کد (+code duplication).  
- افزایش ccyclomatic complexity یا نقض قواعد code style  
می‌توان این معیارها را با **threshold** تعریف کرد تا در صورت نقض، Commit Stage به حالت Amber یا حتی Red برود fileciteturn17file4.

## ۷.۳ نگهداری دقیق Commit Stage
اسکریپت‌های مربوط به Commit Stage باید همواره به‌روز و قابل نگهداری باشند:
- ترکیب build scripts و تست‌های خودکار (commit tests) یکپارچه باشد.
- تغییرات در انواع خطاهای شایعِ شناسایی‌شده در مراحل بعدی pipeline را مدام به فاز commit اضافه کنید تا مشکلات زودتر شناسایی شوند.
- تضمین fast feedback با اجرای سریع Commit Stage در کمتر از ۵ دقیقه (حداکثر ۱۰ دقیقه) fileciteturn17file11.

## ۷.۴ اصول و بهترین شیوه‌های Commit Stage
1. **Compile the code**  
   اولین گام کامپایل آخرین تغییرات است. در صورت شکست، Commit Stage فورا متوقف می‌شود و هشدار صادر می‌شود.
2. **Run commit tests**  
   اجرای مجموعه‌ای از تست‌های سریع شامل unit tests و تست‌های ضروری دیگر برای افزایش سطح اطمینان fileciteturn17file7.
3. **Create binaries**  
   تولید باینری‌های مورد نیاز برای مراحل بعدی، بدون اجرای مجدد پروسه‌ی build در هر محیط.
4. **Code analysis**  
   آنالیز غیرفعال (static analysis) برای ارزیابی معیارهایی مانند test coverage، duplicated code، complexity و امنیت.
5. **Prepare artifacts**  
   تولید و ذخیره‌ی آرشیو‌های deployable برای محیط‌های subsequent stages.  
6. **Time constraint**  
   کل Commit Stage باید در کمتر از ۵ دقیقه اجرا شود تا feedback دیرهنگام نباشد fileciteturn17file11.

### Commit Stage Best Practices
- **Stop the line on failure**: در صورت شکست هر گام، تیم باید فوراً توجه کرده و خطا را رفع کند.
- **Only build binaries once**: از باینری تولیدشده در تمام مراحل استفاده کنید.
- **Separate configuration**: پیکربندی محیط را از باینری‌ها جداسازی کنید.
- **Visible feedback**: نتایج Commit Stage را روی داشبوردهای عمومی نمایش دهید تا همه در جریان باشند.
- **Self-service commits**: توسعه‌دهندگان باید بتوانند قبل از commit اصلی، تست‌های Commit Stage را روی **build grid** اجرا کنند.

Commit Stage نقطه‌ی آغاز **deployment pipeline** است و تضمین می‌کند که هر تغییر سریع و باکیفیت به مراحل بعد منتقل شود.
