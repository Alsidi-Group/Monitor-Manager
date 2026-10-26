# مدير المراقبة — Monitor Manager

<div dir="rtl">

**تطبيق أندرويد عربي لمراقبة الهاتف الحقيقية: البطارية، الحرارة، الشحن، الاستهلاك، وحماية الطاقة — بدون روت.**

- **الإصدار الحالي:** v2.12.0 (versionCode 14)
- **المطور:** مروان السيدي — Marwan Alsidi
- **الدولة:** دولـة لـيـبـيـا 🇱🇾
- **حزمة التطبيق:** `com.alsidi.monitormanager`
- **الحماية:** موقّع بمفتاح ثابت لا يتغير أبداً — SHA-1 `2F66C14A FF6E61D5 E15EA3A9 48ACE2D7 BE04ECC4`

---

## ⬇️ التحميل المباشر

| الملف | الحجم | الرابط |
|---|---|---|
| التطبيق (APK) | ~5.4 MB | [/MonitorManager-v2.12.0.apk](/MonitorManager-v2.12.0.apk) |
| ملف التحديثات | ~1.5 KB | [/update.json](/update.json) |
| مشروع apktool (ZIP) | ~11 MB | [/MonitorManager-v2.12.0-apktool-project.zip](/MonitorManager-v2.12.0-apktool-project.zip) |
| ملف README | نصي | [/README.md](/README.md) |
| مفتاح التوقيع الثابت | ~2 KB | [/monitormanager.keystore](/monitormanager.keystore) |

**قائمة تحميل مستمرة:** كل الروابط القديمة تعمل للأبد — أي رابط بإصدار قديم (`v2.8.0` / `v2.9.0` / `v2.10.0` / `v2.11.0`…) أو `MonitorManager-latest.apk` يخدم تلقائياً **أحدث إصدار** موجود في المجلد، مع رأس `Content-Disposition: attachment` لتنزيل إجباري، و`CORS: *` ليعمل الفاحص داخل التطبيق.

**صفحة التحميل الكاملة:** [/download.html](/download.html) — بطاقات بأحجام وبصمات MD5 حية + خطوات التثبيت + خطوات الرفع على GitHub.

---

## 📲 التثبيت

1. حمّل ملف `MonitorManager-v2.12.0.apk` من الرابط أعلاه.
2. اسمح بـ «التثبيت من مصادر غير معروفة» لمتصفحك.
3. ثبّت مباشرة **فوق النسخة القديمة** — التوقيع ثابت من v2.8.0 حتى اليوم، فالترقية تتم بلا حذف ولا فقدان بيانات.
4. إن كان جهازك يحمل نسخة أقدم من v2.8.0 (موقعة بمفتاح أول) احذفها مرة واحدة فقط — وبعدها كل الترقيات المستقبلية تُثبَّت مباشرة للأبد.

---

## 🔐 صلاحية قطع WiFi والبيانات (بدون روت)

ميزة «توفير الطاقة» تحتاج صلاحية النظام `WRITE_SECURE_SETTINGS` ليعمل القطع والاستعادة التلقائي الكامل. يوفر التطبيق **ثلاث طرق بلا روت**:

### الطريقة 1 — Shizuku (الأفضل: بلا حاسوب) ✨
من شاشة توفير الطاقة داخل التطبيق:
1. اضغط «تثبيت تطبيق Shizuku» (مجاني من Play Store).
2. شغّل Shizuku عبر **التصحيح اللاسلكي** (أندرويد 11+ — مرة واحدة).
3. ارجع للتطبيق واضغط **«تنفيذ أمر المنح تلقائياً الآن»** — التطبيق ينفّذ الأمر بنفسه ويتحقق منه.
4. انتهى — القطع التلقائي الكامل يعمل دائماً.

### الطريقة 2 — adb من حاسوب
```bash
adb shell pm grant com.alsidi.monitormanager android.permission.WRITE_SECURE_SETTINGS
```
(زر «نسخ أمر adb» موجود داخل التطبيق)

### الطريقة 3 — بلا أي صلاحية (النقرة الواحدة)
على أندرويد 10+: زر «قطع الآن» يفتح فوراً **لوحة الإنترنت** في النظام — أوقف WiFi والبيانات بمفتاح واحد. وعلى أندرويد 9 وأقدم يعمل القطع البرمجي التلقائي مباشرة بلا أي صلاحيات.

---

## ✍️ التوقيع الثابت (مثل النسخ القديمة)

من الإصدار v2.12.0 أصبح التوقيع **مثبّتاً رسمياً داخل المشروع** ولا يمكن أن يتغير مستقبلاً:

```json
// android/app/build.gradle — signingConfigs.projectKey
{
  "storeFile": "../../keystore/monitormanager.keystore",
  "storePassword": "android",
  "keyAlias": "androiddebugkey",
  "keyPassword": "android"
}
```

- **SHA-1:** `2F:66:C1:4A:FF:6E:61:D5:E1:5E:A3:A9:48:AC:E2:D7:BE:04:EC:C4`
- نفس المفتاح وقّع v2.8.0 → v2.12.0 كلها — أي ترقية تُثبَّت فوق القديمة مباشرة.
- ملف المفتاح متوفر للتحميل: [/monitormanager.keystore](/monitormanager.keystore) (كلمة السر: `android`، الاسم: `androiddebugkey`).
- **لإعادة توقيع أي بناء محلي من مشروع apktool:**
  ```bash
  zipalign -f 4 project/dist/app-debug-unsigned.apk aligned.apk
  apksigner sign --ks monitormanager.keystore --ks-key-alias androiddebugkey \
    --ks-pass pass:android --key-pass pass:android --out final.apk aligned.apk
  ```
- **للتحقق من توقيع أي نسخة:**
  ```bash
  apksigner verify --print-certs MonitorManager-v2.12.0.apk
  ```
- بطاقة «خدمات Google و Play Protect» داخل التطبيق تعرض بصمة التوقيع الحية من النظام — اضغطها للنسخ وقارنها بالأعلى.

---

## 🛡️ خدمات Google و Play Protect (جديد v2.12)

بطاقة جديدة في شاشة «حول التطبيق» تعرض مباشرة من النظام:
- **خدمات Google Play (GMS):** مثبتة؟ + الإصدار الحي.
- **متجر Google Play:** مثبت؟
- **Play Protect:** حالة فحص التطبيقات الضارة من إعدادات النظام (بصدق: مفعّل / غير مفعّل / غير معروف).
- **سلامة النظام:** نظام رسمي (release-keys) + إقلاع موثّق (Verified Boot).
- **معايير Google Play:** التوافق (توقيع ثابت + targetSdk حديث) + بصمة SHA-1 للتطبيق.

---

## 🚀 بناء المشروع

### من مصدر Gradle الكامل
```bash
cd android
JAVA_HOME=<jdk-21> ./gradlew assembleDebug
# المخرج موقّع تلقائياً بالمفتاح الثابت من signingConfigs.projectKey
```

### من مشروع apktool (ZIP التحميل)
```bash
java -jar apktool.jar d MonitorManager-v2.12.0.apk -o project   # فك
java -jar apktool.jar b project -o rebuilt.apk                   # إعادة تجميع (مثبتة: versionCode 14)
zipalign -f 4 rebuilt.apk aligned.apk
apksigner sign --ks monitormanager.keystore --ks-key-alias androiddebugkey \
  --ks-pass pass:android --key-pass pass:android --out final.apk aligned.apk
```

### بناء واجهة الويب (Next.js)
```bash
bun install
EXPORT_MODE=1 bunx next build   # تصدير ثابت إلى .next-export/ (webDir الخاص بـ Capacitor)
bunx cap sync android           # مزامنة الأصول
rm -f android/app/src/main/assets/public/MonitorManager-*   # منع تضخم APK
cd android && JAVA_HOME=<jdk-21> ./gradlew assembleDebug
```

---

## 🔄 روتين كل إصدار مستقبلي (القائمة المستمرة)

1. عدّل `src/lib/device-sim.ts` (APP_VERSION / APP_VERSION_CODE) و`android/app/build.gradle` (versionCode/versionName).
2. `EXPORT_MODE=1 bunx next build` ثم `bunx cap sync android` ثم `gradlew assembleDebug`.
3. `zipalign` + `apksigner sign --ks keystore/monitormanager.keystore ...` (المفتاح الثابت — لا تتغير أبداً).
4. انسخ APK إلى `public/` و`download/` باسم الإصدار الجديد واحذف النسخة السابقة.
5. حدّث `update.json` (versionCode / apkUrl / md5 / size / changelog) في `public/` + `download/` + `.next-export/`.
6. `bash scripts/sync-aliases.sh` — ينسخ الأسماء القديمة كمرادفات لأحدث إصدار.
7. `bash scripts/verify-links.sh` — تحقق 200 + MD5 + CORS + رؤوس التنزيل.
8. حدّث صفحة `download.html` (أو اتركها — تجلب الإصدار والأحجام من update.json حياً).

---

## 📄 بنية update.json

```json
{
  "appName": "مدير المراقبة",
  "versionName": "2.12.0",
  "versionCode": 14,
  "apkUrl": "https://<host>/MonitorManager-v2.12.0.apk",
  "md5": "<بصمة APK>",
  "size": <حجم APK بالبايت>,
  "updatedAt": "2026-10-26",
  "changelog": "• …"
}
```
- التطبيق يقارن `versionCode` المحلي مع الملف — إن كان الأحدث يعرض «ما الجديد» ويفتح التحميل.
- `apkUrl` يقبل رابط GitHub العادي أو Raw ويصلحه تلقائياً — يمكنك تغيير المصدر من داخل الخانة.

---

## 🗂️ سجل الإصدارات

| الإصدار | أبرز المحتوى |
|---|---|
| **v2.12.0** (14) | خدمات Google و Play Protect + تثبيت التوقيع القديم نهائياً (signingConfig داخلي) |
| v2.11.0 (13) | إصلاح جذري لموفر الطاقة: لوحة الإنترنت الفورية + منح Shizuku التلقائي بلا روت/حاسوب |
| v2.10.0 (12) | خانة «البحث عن تحديثات» + تحميل مباشر |
| v2.9.0 (11) | إشعارات الشحن الحية + تفريغ البطارية + وقت الشحن/التفريغ المتبقي |
| v2.8.0 (10) | مسار WRITE_SECURE_SETTINGS بلا روت + 3 ثيمات + أحداث الشحن + دعم ليبيا |
| v2.5.0 | روابط تحميل مجددة + أصول القياسات الحقيقية |

**ميزات أساسية ثابتة:** قراءات حقيقية 100% (BatteryManager + مستشعرات العتاد)، خدمة أمامية دائمة بإشعار حي، 6 ويدجت، 6 ثيمات، 10 لغات، تتبع تطبيقات الخلفية، صحة البطارية والدورات، واط/أمبير حقيقيان.

---

## 💳 دعم التطبيق

بمبلغ رمزي تريده كهدية — تحويل مصرفي / وان باي **OnePay** — مصرف الجمهورية:
**140201000078964** (اضغط الرقم داخل التطبيق لنسخه تلقائياً)

</div>

---

*Monitor Manager v2.12.0 — Built with Next.js 16 + Capacitor — مروان السيدي · Marwan Alsidi · دولـة لـيـبـيـا 🇱🇾*
