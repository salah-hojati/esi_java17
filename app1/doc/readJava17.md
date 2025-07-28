<div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">


جاوا ۱۷ (Java 17) که در سپتامبر ۲۰۲۱ منتشر شد، یک نسخه **LTS** (پشتیبانی بلندمدت) است و نسبت به جاوا ۱۱ بهبودهای قابل توجهی دارد. در ادامه مهم‌ترین ویژگی‌های جدید و تغییرات Java 17 نسبت به Java 11 را بررسی می‌کنیم:

---

### **۱. ویژگی‌های اصلی جدید در جاوا ۱۷**
#### **۱.۱. سیلد کلاس‌ها (Sealed Classes) - [JEP 409]**
- امکان محدود کردن ارث‌بری از کلاس‌ها یا پیاده‌سازی اینترفیس‌ها را فراهم می‌کند.
- مثال:

</div>

  ```java
  public abstract sealed class Shape permits Circle, Square, Rectangle { }
  public final class Circle extends Shape { } // فقط کلاس‌های مجاز می‌توانند ارث‌بری کنند
  ```
<div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">

#### **۱.۲. کلاس‌های رکورد (Records) - [JEP 395]**
- سینتکس ساده‌تری برای کلاس‌های **غیرقابل تغییر (Immutable)** ایجاد می‌کند.
- مثال (مقایسه با جاوا ۱۱):
</div>

  ```java
  // جاوا ۱۷ (رکورد)
  public record Person(String name, int age) { }

  // معادل در جاوا ۱۱
  public class Person {
      private final String name;
      private final int age;
      // + constructor + getters + equals + hashCode + toString
  }
  ```
<div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">

#### **۱.۳. سوئیچ پیشرفته (Pattern Matching for switch) - [JEP 406]**
- امکان استفاده از **الگوها (Patterns)** در سوئیچ:

</div>

  ```java
  String message = switch (obj) {
      case Integer i -> "عدد: " + i;
      case String s -> "رشته: " + s;
      default -> "ناشناخته";
  };
  ```
<div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">

#### **۱.۴. متن چندخطی (Text Blocks) - [JEP 378]**
- بهبود یافته نسبت به جاوا ۱۵ (اولین نسخه پایدار در جاوا ۱۷).
- مثال:

</div>

  ```java
  String json = """
      {
          "name": "Java",
          "version": 17
      }
      """;
  ```

 <div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">


---

### **۲. بهبودهای API**
#### **۲.۱. متدهای جدید در `String`**
- `formatted()`: جایگزین `String.format()` برای متن‌های چندخطی.

</div>

  ```java
  String message = "Hello %s".formatted("Java 17");
  ```
<div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">

#### **۲.۲. `Stream.toList()`**
- تبدیل `Stream` به لیست به سادگی:
</div>

  ```java
  List<String> list = Stream.of("a", "b").toList(); // جاوا ۱۷
  // معادل جاوا ۱۱: .collect(Collectors.toList())
  ```
<div dir="rtl" style="text-align: right; font-family: 'B Nazanin', Tahoma, sans-serif;">
 
---

### **۳. تغییرات در JVM و عملکرد**
#### **۳.۱. ماشین مجازی جدید (ZGC & Shenandoah)**
- **ZGC** و **Shenandoah** به عنوان **GCهای پیش‌فرض** برای کاهش تاخیر (Latency) بهینه‌سازی شدند.

#### **۳.۲. بهبود عملکرد با Vector API (Incubator)**
- امکان اجرای عملیات **موازی سخت‌افزاری** (SIMD) برای محاسبات عددی.

---

### **۴. حذف و منسوخ‌شدن‌ها**
- **حذف Applet API**: کاملاً از جاوا حذف شد.
- **منسوخ شدن Security Manager**: برای حذف در آینده آماده می‌شود.

---

### **۵. ویژگی‌های داخلی (برای توسعه‌دهندگان حرفه‌ای)**
- **Foreign Function & Memory API (Incubator)**: تعامل ایمن با کد نیتیو (جایگزین JNI).
- **Strongly Encapsulate JDK Internals**: افزایش امنیت با محدود کردن دسترسی به APIهای داخلی.

---

### **مقایسه کلیدی Java 17 vs Java 11**
| ویژگی | Java 11 | Java 17 |
|--------|---------|---------|
| **سیلد کلاس‌ها** | ❌ | ✅ |
| **رکوردها** | ❌ | ✅ |
| **سوئیچ پیشرفته** | ❌ | ✅ |
| **متن چندخطی** | ❌ | ✅ (پایدار) |
| **ZGC/Shenandoah** | ❌ (پیلوت) | ✅ (پیش‌فرض) |
| **Stream.toList()** | ❌ | ✅ |
| **HttpClient** | ✅ (جاوا ۱۱) | ✅ (بهبود یافته) |

---

### **نتیجه‌گیری: آیا به جاوا ۱۷ ارتقا دهیم؟**
- **بله** اگر:
    - نیاز به **پشتیبانی بلندمدت (LTS)** دارید.
    - از **رکوردها**، **سیلد کلاس‌ها** یا **سوئیچ پیشرفته** استفاده می‌کنید.
    - به **بهبودهای عملکردی** (مثل ZGC) نیاز دارید.
- **جاوا ۱۱** هنوز برای پروژه‌های قدیمی قابل استفاده است، اما جاوا ۱۷ **امن‌تر** و **کارآمدتر** است.

جاوا ۱۷ یک **پرش بزرگ** از جاوا ۱۱ محسوب می‌شود و استفاده از آن برای پروژه‌های جدید **توصیه می‌شود**. 🚀
</div>
 