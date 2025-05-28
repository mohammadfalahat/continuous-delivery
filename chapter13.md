# فصل سیزدهم: مدیریت کامپوننت‌ها و Dependencies

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <parent>
    <groupId>com.continuousdelivery</groupId>
    <artifactId>parent</artifactId>
    <version>1.0.0</version>
  </parent>
  <artifactId>simple</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>demo</name>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
    </dependency>
  </dependencies>
</project>
```

این پیکربندی از **parent pom** استفاده می‌کند، به‌طوری که نسخه‌های وابستگی‌ها (مانند junit و commons-collections) بدون مشخص کردن صریح نسخه، از parent به ارث برده می‌شوند fileciteturn49file0.

می‌توانید build خود در **Maven** را refactor کنید تا تکثیر وابستگی‌های متداول حذف شود. به جای تولید یک JAR، می‌توانید یک pom با `<packaging>pom</packaging>` بسازید و در پروژه‌های دیگر به آن وابسته کنید:

```xml
<project>
  ...
  <dependencies>
    <dependency>
      <groupId>com.thoughtworks.golive</groupId>
      <artifactId>parent</artifactId>
      <version>1.0</version>
      <type>pom</type>
    </dependency>
  </dependencies>
</project>
```

یکی از ویژگی‌های مفید **Maven** این است که با اجرای `mvn dependency:analyze` می‌تواند وابستگی‌های اعلان‌نشده و وابستگی‌های بدون‌استفاده را گزارش دهد fileciteturn49file0.

---

## Summary

در این فصل، تکنیک‌هایی بررسی شد تا تیم توسعه بتواند هم‌زمان با حفظ حالت **releasable** برنامه، بیشترین کارایی را در توسعه داشته باشد. اصل اساسی، اطمینان از **fast feedback** بر تأثیر تغییرات روی آمادگی انتشار بود fileciteturn49file0. دو راهبرد کلیدی:

1. **Incremental changes**: شکستن تغییرات به گام‌های کوچک و commit آنها در **mainline**.
2. **Componentization**: تقسیم برنامه به مجموعه‌ای از **loosely coupled**, **well-encapsulated** کامپوننت‌ها.

تا زمانی که اندازه تیم یا برنامه کوچک است (تیم تا ۲۰ نفر و حداکثر دو سال توسعه)، کافی است یک **pipeline** واحد برای ساخت کامل برنامه داشته باشید. با buildهای سریع، unit test کارآمد، و build grid برای acceptance testing می‌توانید مقیاس را افزایش دهید fileciteturn49file0. پس از این حد، استفاده از کامپوننت‌ها، pipeline‌های مبتنی بر وابستگی، و مدیریت اثربخش **artifacts** کلید افزایش سرعت **delivery** و **feedback** است. این روش از پیچیدگی **branching strategies** جلوگیری می‌کند و یکپارچه‌سازی نرم‌افزار را تسهیل می‌نماید fileciteturn49file0.
