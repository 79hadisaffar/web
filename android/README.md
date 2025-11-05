# Finance App - Android Project

این پروژه یک اپلیکیشن Android ساده است که با GitHub Actions بیلد می‌شود.

## ساختار پروژه

```
android/
├── app/
│   ├── build.gradle
│   ├── proguard-rules.pro
│   └── src/
│       └── main/
│           ├── AndroidManifest.xml
│           └── java/com/financeapp/MainActivity.java
├── gradle/
│   └── wrapper/
│       └── gradle-wrapper.properties
├── build.gradle
├── settings.gradle
├── gradle.properties
└── gradlew
```

## بیلد محلی

برای بیلد کردن APK به صورت محلی:

```bash
cd android
./gradlew assembleDebug
```

خروجی در مسیر زیر قرار می‌گیرد:
```
android/app/build/outputs/apk/debug/app-debug.apk
```

## GitHub Actions

این پروژه دارای یک workflow به نام `Android Debug APK` است که به صورت خودکار:

1. بر روی هر push به برنچ‌های `main` و `copilot/add-network-error-handling` اجرا می‌شود
2. APK دیباگ را بیلد می‌کند
3. فایل `app-debug.apk` را به عنوان Artifact آپلود می‌کند

### دانلود APK از GitHub Actions

1. به صفحه Actions مراجعه کنید: https://github.com/79hadisaffar/web/actions
2. آخرین workflow run با نام "Android Debug APK" را انتخاب کنید
3. در قسمت Artifacts، فایل `app-debug` را دانلود کنید

## مشخصات فنی

- **Android Gradle Plugin**: 8.5.0
- **Gradle**: 8.7
- **Compile SDK**: 34
- **Min SDK**: 21
- **Target SDK**: 34
- **Java**: 17

## نکات مهم

- این workflow از JDK 17 استفاده می‌کند
- Gradle cache فعال است برای سرعت بخشیدن به بیلد
- Artifact به مدت 30 روز نگهداری می‌شود

## لینک ریپوزیتوری

https://github.com/79hadisaffar/web
