
# فصل ۹: Testing Nonfunctional Requirements

## ۹.۱ مقدمه
ما از این زیرساخت برای انجام انواع فعالیت‌ها استفاده کرده‌ایم:
- بازتولید خطاهای پیچیده‌ی production  
- شناسایی و رفع memory leaks  
- longevity testing  
- ارزیابی تأثیر garbage collection  
- tuning garbage collection  
- tuning application configuration parameters  
- tuning third-party application configuration (مانند operating system، application server و database configuration)  
- شبیه‌سازی سناریوهای پاتولوژیک (worst-day scenarios)  
- ارزیابی راه‌حل‌های مختلف برای مسائل پیچیده  
- شبیه‌سازی integration failures  
- ارزیابی مقیاس‌پذیری application در چند اجرا با پیکربندی‌های سخت‌افزاری متفاوت  
- load-testing ارتباطات با سیستم‌های خارجی، حتی اگر capacity tests اولیه صرفاً برای stubbed interfaces طراحی شده باشند  
- تمرین rollback از deploymentهای پیچیده  
- از کار انداختن انتخابی بخش‌هایی از application برای ارزیابی graceful degradation of service  
- اجرای real-world capacity benchmarks بر روی hardwareهای production موقتی برای محاسبه فاکتورهای scaling دقیق‌تر جهت یک محیط capacity test بلندمدت  
fileciteturn37file0

## ۹.۲ طراحی برای برآورده کردن Nonfunctional Requirements
طراحی سیستم‌ها برای برآورده کردن nonfunctional requirements موضوعی پیچیده است. ماهیت crosscutting بسیاری از NFRها مدیریت ریسک‌شان را دشوار می‌کند و این می‌تواند به دو رفتار فلج‌کننده منجر شود: عدم توجه کافی از ابتدای پروژه یا در سوی دیگر، معماری تدافعی و over-engineering.  
به‌عنوان کارشناسان فنی، معمولاً به‌سمت راه‌حل‌های کامل و بسته گرایش داریم—سیستم‌هایی که برای بیشترین حالت‌های ممکن fully automated باشند. با این حال، باید با مشتریان و کاربران همکاری نزدیک داشته باشیم تا sensitivity points سیستم را تعیین کرده و detailed nonfunctional requirements را بر پایه‌ی real business value تعریف کنیم. fileciteturn37file0

## ۹.۳ ایجاد و نگهداری Automated Tests برای Nonfunctional Requirements
پس از تعیین nonfunctional requirements، تیم delivery باید automated tests مناسبی ایجاد و نگهداری کند تا اطمینان حاصل شود این نیازمندی‌ها برآورده شده‌اند. این تست‌ها باید هر بار که تغییر در application، infrastructure یا configuration از stages قبلی pipeline گذر کرد اجرا شوند. بهترین استراتژی این است که از acceptance tests به‌عنوان نقطه‌ی شروع برای broader scenario-based testing of NFRs استفاده کنید تا پوشش جامع و maintainable از ویژگی‌های سیستم فراهم آید. fileciteturn37file0
