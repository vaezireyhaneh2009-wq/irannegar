# ساخت APK ایران‌نگار (قدم به قدم)

## پیش‌نیازها (یک بار نصب کنید)
1. Node.js (نسخه LTS) از nodejs.org
2. Android Studio از developer.android.com/studio
   (هنگام نصب، گزینه‌های Android SDK و Android SDK Platform را نگه دارید)
3. اتصال اینترنت برای دانلود پکیج‌ها

## مراحل
داخل پوشه‌ی پروژه (همین پوشه) ترمینال را باز کنید:

```
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap add android
npm install -D @capacitor/assets
npx capacitor-assets generate --android
npx cap sync android
```

### روش الف: ساخت APK با ترمینال
```
cd android
./gradlew assembleDebug        (ویندوز: gradlew.bat assembleDebug)
```
فایل خروجی:
`android/app/build/outputs/apk/debug/app-debug.apk`
این فایل را می‌توانید مستقیم روی گوشی نصب کنید یا برای داور بفرستید.

### روش ب: با Android Studio
```
npx cap open android
```
صبر کنید Gradle Sync تمام شود، سپس
Build ← Build Bundle(s) / APK(s) ← Build APK(s)

## تست روی گوشی
گوشی را با USB وصل کنید (Developer options و USB debugging روشن باشد) و در Android Studio دکمه‌ی Run را بزنید.
یا فایل APK را به گوشی منتقل کنید و نصب کنید (اجازه‌ی «نصب از منابع ناشناس» لازم است).

## نسخه‌ی نهایی برای انتشار در بازار/مایکت
APK بالا «debug» است. برای انتشار: Build ← Generate Signed Bundle / APK ← APK ← ساخت Keystore جدید.
**فایل keystore و رمزش را حتماً جای امن نگه دارید**؛ بدون آن نمی‌توانید برنامه را آپدیت کنید.

## اگر بعداً HTML را عوض کردید
فایل `www/index.html` را جایگزین کنید و دوباره:
```
npx cap sync android
```
و APK را از نو بسازید.

## نکته‌ها
- فونت وزیرمتن الان از Google Fonts لود می‌شود؛ بدون اینترنت فونت پیش‌فرض (Tahoma) نمایش داده می‌شود. برای آفلاین‌شدن کامل، فایل فونت را در `www/fonts/` بگذارید و با @font-face در index.html معرفی کنید.
- صدای فارسی دستیار صوتی به موتور TTS گوشی بستگی دارد (Google Text-to-Speech با بسته‌ی فارسی).
- نام بسته (`ir.irannegar.app`) در `capacitor.config.json` است؛ اگر خواستید عوضش کنید، قبل از `npx cap add android` تغییر بدهید.
