# راهنمای کامل بیلد Android APK با GitHub Actions

## 📱 اطلاعات پروژه

**لینک ریپوزیتوری GitHub:**
```
https://github.com/79hadisaffar/web
```

**لینک صفحه Actions:**
```
https://github.com/79hadisaffar/web/actions
```

## ✅ چه کارهایی انجام شده است؟

### 1. ساختار پروژه Android
یک پروژه Android کامل در مسیر `android/` ساخته شده است که شامل:
- **Android Gradle Plugin**: نسخه 8.5.0
- **Gradle**: نسخه 8.7
- **Compile SDK**: 34 (Android 14)
- **Min SDK**: 21 (Android 5.0)
- **Target SDK**: 34
- **Java**: نسخه 17

### 2. GitHub Actions Workflow
یک workflow با نام **"Android Debug APK"** ساخته شده است که:
- بر روی هر push به برنچ `main` و `copilot/add-network-error-handling` اجرا می‌شود
- بر روی pull request ها اجرا می‌شود
- قابلیت اجرای دستی (manual dispatch) دارد
- APK دیباگ را بیلد و آپلود می‌کند

## 🚀 چگونه APK را دریافت کنیم؟

### روش 1: از طریق صفحه Actions (توصیه می‌شود)

1. به صفحه Actions مراجعه کنید:
   ```
   https://github.com/79hadisaffar/web/actions
   ```

2. در لیست workflows، روی **"Android Debug APK"** کلیک کنید

3. آخرین workflow run را انتخاب کنید

4. اگر وضعیت workflow "Action required" است:
   - دکمه **"Approve and run"** را بزنید
   - منتظر بمانید تا بیلد تکمیل شود (معمولاً 3-5 دقیقه)

5. بعد از اتمام موفق بیلد:
   - به پایین صفحه بروید
   - در بخش **"Artifacts"** فایل `app-debug` را پیدا کنید
   - روی آن کلیک کنید تا دانلود شود (یک فایل ZIP)

6. فایل ZIP را استخراج کنید:
   - داخل آن فایل `app-debug.apk` را خواهید یافت
   - این APK را روی دستگاه Android خود نصب کنید

### روش 2: اجرای دستی Workflow

1. به صفحه Actions بروید

2. در سمت چپ، workflow **"Android Debug APK"** را انتخاب کنید

3. روی دکمه **"Run workflow"** کلیک کنید

4. برنچ مورد نظر را انتخاب کنید (مثلاً `copilot/add-network-error-handling`)

5. دکمه **"Run workflow"** سبز رنگ را بزنید

6. منتظر بمانید تا workflow اجرا و تکمیل شود

7. APK را از بخش Artifacts دانلود کنید

### روش 3: با Push جدید

هر push جدید به برنچ فعلی، workflow را به صورت خودکار اجرا می‌کند:
```bash
git commit --allow-empty -m "Trigger Android build"
git push
```

## 📋 جزئیات فنی

### ساختار پروژه
```
android/
├── app/
│   ├── build.gradle           # تنظیمات Gradle ماژول app
│   ├── proguard-rules.pro     # قوانین ProGuard
│   └── src/
│       └── main/
│           ├── AndroidManifest.xml
│           ├── java/com/financeapp/MainActivity.java
│           └── res/
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── build.gradle               # تنظیمات Gradle پروژه
├── settings.gradle            # تنظیمات ماژول‌ها
├── gradle.properties          # خصوصیات Gradle
├── gradlew                    # اسکریپت Gradle Wrapper (Unix)
└── README.md                  # راهنمای پروژه Android
```

### Workflow Steps

1. **Checkout code**: کد از ریپوزیتوری دریافت می‌شود
2. **Set up JDK 17**: Java 17 با توزیع Temurin نصب می‌شود
3. **Grant execute permission**: دسترسی اجرا به gradlew داده می‌شود
4. **Build Debug APK**: APK دیباگ با دستور `./gradlew assembleDebug` بیلد می‌شود
5. **Upload Debug APK**: APK به عنوان artifact آپلود می‌شود (30 روز نگهداری)
6. **Display APK info**: اطلاعات APK نمایش داده می‌شود

### Cache و Optimization

- Gradle cache فعال است برای سرعت بخشیدن به بیلدهای بعدی
- Dependencies به صورت خودکار cache می‌شوند
- JVM options: `-Xmx2048m` برای استفاده بهینه از حافظه

## ⚠️ نکات مهم

1. **دسترسی به Artifacts:**
   - اگر ریپوزیتوری Public باشد، همه می‌توانند artifact را ببینند
   - اگر Private باشد، فقط کاربران با دسترسی می‌توانند دانلود کنند

2. **مدت نگهداری:**
   - Artifacts به مدت 30 روز نگهداری می‌شوند
   - بعد از آن به صورت خودکار حذف می‌شوند

3. **محدودیت‌های GitHub Actions:**
   - اکانت‌های رایگان: 2000 دقیقه در ماه
   - هر بیلد معمولاً 3-5 دقیقه طول می‌کشد

## 🔧 بیلد محلی (اختیاری)

اگر می‌خواهید APK را به صورت محلی بیلد کنید:

```bash
cd android
./gradlew assembleDebug
```

خروجی در این مسیر قرار می‌گیرد:
```
android/app/build/outputs/apk/debug/app-debug.apk
```

## 🆘 عیب‌یابی

### Workflow اجرا نمی‌شود
- بررسی کنید که workflow file در مسیر `.github/workflows/android-debug-apk.yml` وجود دارد
- اطمینان حاصل کنید که push به برنچ درست انجام شده است
- Actions ممکن است نیاز به تأیید داشته باشد (اگر "Action required" نمایش داده می‌شود)

### بیلد با خطا مواجه شد
- لاگ‌های بیلد را در صفحه workflow run بررسی کنید
- اطمینان حاصل کنید که همه فایل‌های لازم commit شده‌اند

### Artifact پیدا نمی‌شود
- فقط workflow run های موفق artifact دارند
- اطمینان حاصل کنید که workflow به طور کامل اجرا شده است
- Artifact بعد از 30 روز منقضی می‌شود

## 📞 پشتیبانی

برای هرگونه سوال یا مشکل:
- Issue در GitHub ایجاد کنید
- لاگ‌های workflow را چک کنید
- مستندات GitHub Actions را مطالعه کنید: https://docs.github.com/en/actions

---

**تاریخ ایجاد**: نوامبر 2025
**آخرین بروزرسانی**: نوامبر 2025
**وضعیت**: ✅ آماده برای استفاده
