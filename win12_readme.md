# Windows 12 Mobile Launcher 🪟📱

Launcher متطور لنظام Android يحاكي تجربة Windows 12 Mobile الكاملة

## ✨ المميزات

### الواجهة الرئيسية
- 🎨 تصميم Windows 12 الحديث مع تأثيرات شفافة
- 📱 شريط المهام (Taskbar) السفلي
- 🔵 زر Start المميز بشعار Windows
- ⏰ شريط الحالة العلوي مع الساعة والتاريخ
- 🔍 بحث متقدم عن التطبيقات

### قائمة Start
- 📊 عرض جميع التطبيقات بشكل مرتب
- 🎯 تنظيم التطبيقات في شبكة 4 أعمدة
- 🖼️ أيقونات التطبيقات بدقة عالية
- ⚡ فتح التطبيقات بلمسة واحدة
- 🎭 تأثيرات حركية عند الفتح والإغلاق

### الإعدادات السريعة
- 📡 WiFi
- 🔵 Bluetooth
- 🔋 البطارية
- ⚙️ إعدادات النظام

### صفحة الإعدادات
- 🖥️ إعدادات النظام
- 🌐 الشبكة والاتصال
- 📱 التطبيقات والتخزين
- 🔒 الأمان والخصوصية
- 🏠 إعدادات Launcher
- ℹ️ معلومات الجهاز

## 📋 المتطلبات

- **نظام التشغيل**: Android 7.0 (API 24) أو أحدث
- **ذاكرة RAM**: 2 GB على الأقل (يُفضل 4 GB)
- **مساحة التخزين**: 50 MB

## 🚀 التثبيت

### الطريقة 1: Android Studio

1. **استنساخ المشروع**
```bash
git clone https://github.com/yourusername/windows12-launcher.git
cd windows12-launcher
```

2. **فتح المشروع في Android Studio**
   - File → Open
   - اختر مجلد المشروع

3. **مزامنة Gradle**
   - انتظر حتى يتم تحميل كل المكتبات

4. **توصيل الجهاز**
   - قم بتفعيل وضع المطور على هاتفك
   - فعّل USB Debugging
   - وصّل الهاتف بالكمبيوتر

5. **تشغيل التطبيق**
   - اضغط على زر Run (▶️) في Android Studio

### الطريقة 2: تثبيت APK مباشرة

1. قم ببناء APK من Android Studio:
   - Build → Build Bundle(s) / APK(s) → Build APK(s)

2. انقل ملف APK إلى هاتفك

3. افتح الملف وقم بالتثبيت

## 🎯 كيفية الاستخدام

### تعيين كـ Launcher افتراضي

1. بعد تثبيت التطبيق، اضغط زر Home
2. ستظهر قائمة باللانشرات المتاحة
3. اختر "Windows 12 Launcher"
4. اضغط "Always" لجعله افتراضياً

### التنقل في الواجهة

#### زر Start
- **اضغط**: فتح/إغلاق قائمة Start
- **قائمة Start**: عرض جميع التطبيقات المثبتة

#### فتح التطبيقات
1. اضغط على زر Start
2. اختر التطبيق المطلوب
3. التطبيق سيفتح مباشرة

#### الإعدادات السريعة
- **WiFi**: إدارة الاتصال اللاسلكي
- **Bluetooth**: تفعيل/إلغاء البلوتوث
- **Battery**: عرض حالة البطارية
- **Settings**: الإعدادات الكاملة

#### زر الإعدادات الرئيسي
- موجود في قائمة Start (أسفل)
- يفتح صفحة إعدادات Windows 12

### خيارات التطبيقات

- **ضغطة عادية**: فتح التطبيق
- **ضغطة طويلة**: قائمة خيارات (قريباً)

## 🛠️ هيكل المشروع

```
windows12-launcher/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/windows12/launcher/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── SettingsActivity.kt
│   │   │   │   └── (ملفات أخرى)
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   ├── activity_main.xml
│   │   │   │   │   ├── activity_settings.xml
│   │   │   │   │   └── settings_item.xml
│   │   │   │   ├── drawable/
│   │   │   │   │   ├── (أيقونات وخلفيات)
│   │   │   │   ├── values/
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   └── mipmap/
│   │   │   └── AndroidManifest.xml
│   └── build.gradle
└── build.gradle
```

## 🎨 التخصيص

### تغيير الألوان

عدّل ملف `res/values/colors.xml`:

```xml
<color name="windows_blue">#0078D4</color>
<color name="windows_dark_blue">#005A9E</color>
```

### تعديل عدد الأعمدة

في `MainActivity.kt`:

```kotlin
appsGrid.columnCount = 4 // غيّر العدد حسب الرغبة
```

### تخصيص الخلفية

في `res/drawable/windows_background.xml`:

```xml
<gradient
    android:startColor="#50B4FF"
    android:centerColor="#0078D4"
    android:endColor="#005A9E"
/>
```

## 🔧 المشاكل المعروفة وحلولها

### المشكلة: التطبيق لا يظهر كخيار Launcher
**الحل**: تأكد من إضافة intent-filter الصحيح في AndroidManifest.xml

### المشكلة: الأيقونات لا تظهر
**الحل**: تأكد من وجود صلاحية QUERY_ALL_PACKAGES

### المشكلة: التطبيق يتوقف عند الفتح
**الحل**: تحقق من Logcat في Android Studio

## 📱 المتطلبات التقنية

### الصلاحيات المطلوبة

- `QUERY_ALL_PACKAGES`: لعرض جميع التطبيقات
- `SET_WALLPAPER`: لتغيير الخلفية
- `INTERNET`: للميزات المستقبلية
- `ACCESS_WIFI_STATE`: لعرض حالة WiFi
- `BLUETOOTH`: لإدارة البلوتوث

### المكتبات المستخدمة

```gradle
- AndroidX Core KTX
- Material Design Components
- ConstraintLayout
- RecyclerView
- Lifecycle Components
- Kotlin Coroutines
```

## 🚧 الميزات القادمة

- [ ] ويدجتات على الشاشة الرئيسية
- [ ] تخصيص البلاط (Tiles)
- [ ] دعم الثيمات
- [ ] مدير الملفات مدمج
- [ ] تأثيرات Fluent Design
- [ ] دعم اللغة العربية الكامل
- [ ] مركز الإشعارات
- [ ] خلفيات متحركة
- [ ] تطبيق الإعدادات مخصص بالكامل

## 📄 الترخيص

هذا المشروع مفتوح المصدر تحت رخصة MIT

## 👨‍💻 المطور

تم تطويره بواسطة Claude مع التركيز على محاكاة تجربة Windows 12 الأصلية

## 🤝 المساهمة

المساهمات مرحب بها! يرجى:

1. Fork المشروع
2. إنشاء فرع للميزة الجديدة
3. Commit التغييرات
4. Push إلى الفرع
5. فتح Pull Request

## 📧 الدعم

لأي استفسارات أو مشاكل:
- افتح Issue على GitHub
- راسلنا على البريد الإلكتروني

## 🌟 شكر خاص

شكراً لكل من ساهم في تطوير هذا المشروع!

---

**ملاحظة**: هذا مشروع تجريبي لأغراض تعليمية. Windows هي علامة تجارية مسجلة لشركة Microsoft.
