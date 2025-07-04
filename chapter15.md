# فصل ۱۵ مدیریت Continuous Delivery

## مقدمه
این کتاب عمدتاً برای مجریان ابزارها و فرآیندهای Continuous Delivery نوشته شده است. با این حال، پیاده‌سازی continuous delivery بیش از خرید ابزار و انجام خودکارسازی است. این امر وابسته به همکاری مؤثر میان همهٔ افراد درگیر در فرایند تحویل، حمایت حامیان اجرایی و تمایل تیم برای اعمال تغییرات است. این فصل راهنمایی‌هایی برای عملیاتی‌سازی continuous delivery در سازمان ارائه می‌دهد. ابتدا مدل بلوغ (maturity model) برای مدیریت Configuration و Release را معرفی می‌کنیم. سپس به برنامه‌ریزی چرخه عمر پروژه، از جمله فرایند release می‌پردازیم. پس از آن، روش مدیریت ریسک build و release شرح داده می‌شود. در پایان، به ریسک‌ها و ضدالگوهای سازمانی رایج در استقرار نگاه می‌کنیم و الگوها و بهترین شیوه‌ها برای اجتناب از آن‌ها ارائه می‌دهیم. fileciteturn54file0

## مدل بلوغ برای مدیریت Configuration و Release
### مدل بلوغ
برای ارزیابی سازمان‌ها در حوزهٔ مدیریت Configuration و Release مدلی تدوین شده است که مراحل بلوغ را نشان می‌دهد (شکل ۱۵.۱). این مدل کمک می‌کند موقعیت فعلی سازمان را مشخص کرده و گام‌های پیشرفت را تعریف کنیم. fileciteturn55file0

### نحوه استفاده از مدل
برای بهره‌برداری از این مدل:
- چرخهٔ PDCA (Plan-Do-Check-Act) را اجرا کنید.
- سطح بلوغ سازمان را در هر دسته‌بندی مشخص کنید.
- حوزه‌ای را انتخاب کنید که کمبود بلوغ آن بیشترین درد را ایجاد می‌کند.
- با نقشه‌برداری جریان ارزش (value stream mapping) نقاط بهبود را شناسایی کنید.
- تغییرات موردنیاز را برنامه‌ریزی، اولویت‌بندی و معیارهای پذیرش تعریف کنید.
- تغییرات را به صورت incremental پیاده‌سازی کرده و اثر آن‌ها را اندازه‌گیری کنید.
- با بازخوردگیری و بازنگری مداوم مدل را بهبود دهید. fileciteturn55file0

## چرخهٔ عمر پروژه
### شناسایی (Identification)
در سازمان‌های متوسط و بزرگ یک استراتژی حاکمیتی وجود دارد که اهداف استراتژیک را تعیین و پروژه‌های مرتبط را تعریف می‌کند. آغاز پروژه بدون **business case** باعث شکست می‌شود؛ چرا که تعریف «موفقیت» بدون برآورد سود و هزینه غیرممکن است. همچنین باید فهرستی از ذی‌نفعان (stakeholders) تهیه شود، به‌ویژه یک حامی کسب‌وکار (senior responsible owner) که در Scrum به آن Product Owner گفته می‌شود. fileciteturn56file19

### آغاز (Inception)
در فاز inception، deliverableهای زیر باید آماده شوند:
- **Release plan** شامل برنامه زمان‌بندی و برآورد هزینه‌ها
- **Testing strategy**
- **Release strategy**
- **ارزیابی معماری** برای انتخاب پلتفرم و فریم‌ورک
- **Risk and issue log**
- **توصیف چرخه عمر توسعه**
- **برنامهٔ اجرایی** برای deliverableها  
این اسناد باید به اندازه‌ای دقیق باشند که در عرض سه تا شش ماه (ترجیحاً کمتر) اولین نسخه قابل ارائه آماده شود. این مدارک به مرور تغییر می‌کنند و باید در version control ثبت شوند. fileciteturn56file0

### تاسیس (Initiation)
در این فاز (معمولاً یک تا دو هفته) باید زیرساخت پایه پروژه فراهم شود:
- تأمین سخت‌افزار و نرم‌افزار موردنیاز تیم
- آماده‌سازی فضای کاری (اینترنت، وایت‌برد، کاغذ و خودکار، پرینتر، خوراکی)
- ایجاد حساب‌های ایمیل و دسترسی‌ها
- راه‌اندازی version control
- راه‌اندازی محیط basic Continuous Integration
- توافق بر نقش‌ها، ساعات کاری و جلسات روزانه
- آماده‌سازی محیط تست ساده و دادهٔ تست
- انجام spikes برای کاهش ریسک‌های تحلیل، توسعه و تست  
برای پایان این فاز باید یک داستان ساده («Hello World» معماری) با اسکریپت build و چند تست قابل اجرای CI تولید شود. fileciteturn56file0

### توسعه و انتشار (Develop & Release)
پس از initiation، پروژه به صورت iterative و incremental توسعه می‌یابد. در هر iteration باید یک increment از قابلیت‌های باارزش به تولید برسد و قابلیت انتشار را حفظ کند. بهترین بازخورد از کاربران واقعی حاصل می‌شود؛ بنابراین هر چه زودتر امکان انتشار به محیط واقعی فراهم شود، زودتر می‌توان واکنش نشان داد. fileciteturn55file6

## فرایند مدیریت ریسک (A Risk Management Process)
مدیریت ریسک به معنای:
1. شناسایی ریسک‌های اصلی پروژه
2. تعریف استراتژی‌های کاهش (mitigation) مناسب
3. پایش مستمر ریسک‌ها در طول پروژه  
است. این فرایند باید:
- ساختار استاندارد گزارش‌دهی داشته باشد
- به‌روزرسانی‌های منظم از تیم پروژه
- داشبورد برای مدیران برنامه
- ممیزی‌های دوره‌ای توسط ناظری بیرونی  
fileciteturn55file6

### مبانی مدیریت ریسک (Risk Management 101)
- ریسک‌ها بر اساس **شدت (impact)** و **احتمال (likelihood)** طبقه‌بندی می‌شوند.
- شدت = impact × likelihood
- مبلغ مالی معادل شدت ریسک مبنای تصمیم‌گیری برای هزینهٔ mitigation است.  
fileciteturn55file6

### جدول زمانی مدیریت ریسک (Risk Management Timeline)
- **پایان Inception**: بررسی Release strategy و فرایندهای مرتبط با آن
- **پایان Initiation**: آغاز اجرای طرح و بررسی برنامه اولیه  
سپس در فازهای Development و Deployment، مدیریت ریسک به‌طور مداوم تکرار می‌شود. fileciteturn55file6
