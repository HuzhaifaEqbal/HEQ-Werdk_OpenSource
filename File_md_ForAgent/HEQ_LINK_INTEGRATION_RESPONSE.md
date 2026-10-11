# 🔗 الدليل التقني للتكامل المشترك بين HEQ Link و HEQ Werdk
## (Cross-App Integration, User Schema & Architecture Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **توثيق نموذج المستخدم الموحد (PostgreSQL Schema):** حقول المعرف الموحد `heq_id` والرتب الإيمانية وإعدادات الخصوصية.
> * **معايير أمان وتوليد رموز JWT:** خوارزمية التشفير، مدة الصلاحية، واستخراج بيانات المستخدم.
> * **بروتوكول الربط المتبادل والروابط العميقة:** دورة الـ Deep Links وسياسات CORS وأمان الشبكة.
> * **الفئة المستهدفة:** مهندسو الواجهة الخلفية لكلا النظامين، ومهندسو أمان الخدمات السحابية.

---

## 1. بنية المستخدم وقاعدة البيانات (User Schema & Database)

### نوع قاعدة البيانات
* **قاعدة البيانات الأساسية:** **PostgreSQL** (تعمل عبر `pg` Connection Pool مع تفعيل SSL).

### نموذج المستخدم (User Model & Schema)
جدول المستخدمين في قاعدة البيانات هو `users`، وهذه أبرز الحقول المعرّفة فيه:

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,              -- المعرف الرقمي الأساسي (Auto-increment)
    heq_id TEXT DEFAULT '',             -- المعرف الفريد الموحد داخل المنظومة (مثل: HEQ00042)
    email TEXT UNIQUE NOT NULL,         -- البريد الإلكتروني للمستخدم
    name TEXT NOT NULL,                 -- الاسم الظاهر للمستخدم
    avatar TEXT DEFAULT '',             -- رابط الصورة الرمزية المباشر (Full CDN URL)
    cover_image TEXT DEFAULT '',        -- صورة الغلاف
    bio TEXT DEFAULT '',                -- النبذة التعريفية
    country TEXT DEFAULT '',            -- الدولة
    residence TEXT DEFAULT '',          -- مكان الإقامة
    age INTEGER,                        -- العمر
    gender TEXT DEFAULT '',             -- الجنس
    flames INTEGER DEFAULT 0,           -- نقاط التفاعل (Flames)
    rank_tier TEXT DEFAULT 'rank_1',    -- رتبة المستوى
    faith_rank TEXT DEFAULT '✨ مبادر', -- الرتبة الإيمانية
    verification_type TEXT DEFAULT 'none', -- حالة ونوع التوثيق (none, blue, gold...)
    badge_style JSONB DEFAULT '{}'::jsonb, -- إعدادات الشارة المخصصة
    privacy_settings JSONB,             -- إعدادات الخصوصية
    two_fa_enabled INTEGER DEFAULT 0,   -- تفعيل 2FA
    hajen_auth_enabled BOOLEAN DEFAULT FALSE, -- نظام أمان هجين للأجهزة الموثوقة
    disabled INTEGER DEFAULT 0,         -- هل الحساب معطل (1 = نعم, 0 = نشط)
    joined_at BIGINT NOT NULL           -- توقيت التسجيل (Unix Timestamp بالمللي ثانية)
);
```

### حقل الربط الموحد (Unified Identifier)
* **المعرف الأساسي الموصى به للربط:** **`heq_id`** (سلسلة نصية تبدأ بـ `HEQ` متبوعة برقم المستخدم بخمس خانات، مثال: `HEQ00001` أو `HEQ00156`). يتم توليده تلقائياً عند تفعيل الحساب عبر:
  `const heqId = 'HEQ' + String(userId).padStart(5, '0');`
* **المعرف الرقمي الثابت:** **`id`** (Integer) وهو الـ Primary Key الداخلي المعتمد في كل العلاقات والجلسات.
* **الخلاصة:** يمكنكم تخزين `heq_id` و `heq_link_user_id` في جدول المستخدمين الخاص بتطبيق Werdk كـ Unique Foreign Identifier.

---

## 2. نظام المصادقة والـ JWT (Authentication & JWT)

### آلية توليد الـ Token
نستخدم معيار **JWT (JSON Web Token)** عبر مكتبة `jsonwebtoken`:

1. **Access Token (توكن الوصول):**
   * الدالة: `signAccessToken(payload)`
   * المفتاح السري في السيرفر: `process.env.SECRET_KEY`
   * مدة الصلاحية: **ساعتان (`2h`)**.
2. **Refresh Token (توكن التجديد):**
   * الدالة: `signRefreshToken(payload)`
   * المفتاح السري في السيرفر: `process.env.REFRESH_SECRET`
   * مدة الصلاحية: **60 يوماً (`60d`)**.

### حمولة البيانات (Token Payload)
البيانات المشفرة داخل الـ Access Token هي:

```json
{
  "id": 15,
  "email": "user@heqlink.com",
  "v": 0,
  "iat": 1727180000,
  "exp": 1727187200
}
```
* `id`: رقم المستخدم الأساسي (`users.id`).
* `email`: البريد الإلكتروني.
* `v`: رقم إصدار الجلسة (`jwt_version`) المستخدم للإلغاء الفوري للجلسات عند تغيير كلمة المرور أو تسجيل الخروج.

### التوصية المعمارية للربط بين السيرفرين (Shared vs API Verification)
نوصي بالخيار **(ب) - مسار المصادقة المنفصل الموثوق (OAuth2-Style Code Exchange)** لضمان أمان النظام واستقلالية الخدمات:

1. **سيرفر مستقل لكل تطبيق مع API للتحقق المتبادل (موصى به جداً أمنياً):**
   * بدلاً من مشاركة قاعدة البيانات أو `JWT_SECRET`، يرسل تطبيق HEQ Link رمز دخول مؤقت (One-Time Auth Code) صالح لدقيقتين فقط إلى Werdk.
   * يقوم سيرفر Werdk باستدعاء سيرفر HEQ Link:
     `POST /api/sso/verify-code` مع `client_id` و `client_secret` الخاص بـ Werdk.
   * يرد سيرفر HEQ Link ببيانات المستخدم (`id`, `heq_id`, `email`, `name`, `avatar`).
   * ينشئ سيرفر Werdk جلسته الخاصة المستقلة.
   * **الميزة:** حماية سرية السيرفرين وعدم تأثر أحد التطبيقين في حال حدوث أي مشكلة أو تغيير في بنية الآخر.

2. **الخيار المشترك (إذا رغبت الإدارة بسيرفر واحد أو مفتاح موحد):**
   * استخدام نفس قيمة `process.env.SECRET_KEY`، وبالتالي يستطيع سيرفر Werdk فك تشفير التوكن مباشرة وقراءة `id` و `email`.

---

## 3. الربط العميق (Deep Linking & App-to-App Auth)

### الوضع الحالي في تطبيق HEQ Link (Flutter)
* التطبيق يعتمد بالفعل على حزمة **`app_links: ^7.0.0`** في `pubspec.yaml`.
* الاستماع مهيأ ومُفعل في `lib/main.dart` عبر `_appLinks.uriLinkStream` و `_appLinks.getInitialLink()`.

### الإعدادات المطلوبة لتفعيل Scheme المخصص (`heqlink://`)

#### في Android (`android/app/src/main/AndroidManifest.xml`):
داخل وسم `<activity android:name=".MainActivity">`:
```xml
<!-- دمج معيار heqlink Scheme للربط بين التطبيقات -->
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="heqlink" />
</intent-filter>
```

#### في iOS (`ios/Runner/Info.plist`):
```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>heqlink</string>
        </array>
    </dict>
</array>
```

### تصور المنطق البرمجي في فلاتر (Code Implementation in HEQ Link)

في دالة `_handleDeepLink(Uri uri)` داخل `lib/main.dart`:

```dart
void _handleDeepLink(Uri uri) async {
  debugPrint("Received deep link: $uri");

  // معالجة طلب المصادقة من التطبيقات الشقيقة (HEQ Ecosystem Auth)
  if (uri.scheme == 'heqlink' && uri.host == 'auth') {
    final String? callbackUrl = uri.queryParameters['callback'];
    final String? state = uri.queryParameters['state'];

    if (callbackUrl == null) return;

    // 1. التحقق من وجود جلسة دخول نشطة للمستخدم في HEQ Link
    final prefs = await SharedPreferences.getInstance();
    final String? token = prefs.getString('token');
    final String? userName = prefs.getString('userName');

    if (token == null) {
      // المستخدم غير مسجل دخول في HEQ Link، توجيهه لشاشة تسجيل الدخول أولاً
      navigatorKey.currentState?.push(MaterialPageRoute(
        builder: (_) => LoginScreen(pendingAuthRedirect: uri),
      ));
      return;
    }

    // 2. إظهار BottomSheet لتأكيد منح الصلاحية لتطبيق Werdk
    final context = navigatorKey.currentContext;
    if (context == null) return;

    final bool? approved = await showModalBottomSheet<bool>(
      context: context,
      isDismissible: false,
      shape: const RoundedRectangleBorder(
        borderRadius: BorderRadius.vertical(top: Radius.circular(20)),
      ),
      builder: (ctx) => AppAuthConfirmationSheet(
        appName: 'HEQ Werdk',
        userName: userName ?? '',
      ),
    );

    if (approved == true) {
      // 3. توليد كود مصادقة مؤقت Auth Code من السيرفر
      final String authCode = await AuthService.generateSsoAuthCode(targetApp: 'werdk');

      // 4. إعادة التوجيه إلى تطبيق Werdk عبر الـ Callback
      final Uri returnUri = Uri.parse(callbackUrl).replace(
        queryParameters: {
          'code': authCode,
          if (state != null) 'state': state,
        },
      );

      await launchUrl(returnUri, mode: LaunchMode.externalApplication);
    }
  }
}
```

---

## 4. خدمة رفع الملفات (Bunny.net Media)

### آلية تخزين الصور الرمزية (Avatars)
* تتم إدارة التخزين عبر **Bunny.net Storage Zone** و **CDN Pull Zone**.
* مسار مجلد صور المستخدمين في Bunny.net هو: **`users/avatars/`**.
* تتم عملية الرفع بتشفير Base64 عبر دالة الباك إند `uploadBase64ToBunny` في `Myserver/utils/bunnyUploader.js` بواسطة `PUT` إلى:
  `https://storage.bunnycdn.com/${BUNNY_STORAGE_ZONE}/users/avatars/${timestamp}_${randomId}.jpg`

### طبيعة الرابط المخزن في قاعدة البيانات
* **يتم تخزين الرابط كاملاً كـ Full CDN URL** وليس مساراً نسبياً.
* مثال على الرابط الفعلي في حقل `avatar` بجدول `users`:
  `https://heqlinkmedia1.b-cdn.net/users/avatars/1727180000_a8f9z2.jpg`
* **الفائدة لتطبيق Werdk:** 
  لا يحتاج تطبيق Werdk أو خادمه لأي إعدادات خاصة أو مفاتيح وصول لـ Bunny.net لقراءة وعرض صور المستخدمين؛ يكفي استخدام قيمة حقل `avatar` مباشرة داخل `CachedNetworkImage` أو أي مكون عرض صور.

---

## 5. ملخص جهوزية التكامل (Action Plan)

| البند | الحالة لدى HEQ Link | الخطوة القادمة |
| :--- | :---: | :--- |
| **قاعدة البيانات** | PostgreSQL جاهزة تماماً وتتضمن `heq_id` و `avatar` كـ Full URL. | اعتماد `heq_id` كحقل ربط حسابات المستخدمين. |
| **المصادقة (JWT)** | جاهزة ومفعلة بـ `SECRET_KEY` وتدعم حمولة `id` و `email`. | الاتفاق الإداري على: (تبادل كود SSO عبر API أم مشاركة `SECRET_KEY`). |
| **الربط العميق** | حزمة `app_links` موجودة ومنطق الاستماع يعمل. | إضافة الـ Intent Filter لـ `heqlink://` وشاشة تأكيد الربط. |
| **خدمة الوسائط** | روابط الصور كاملة ومتاحة علناً عبر CDN Bunny.net. | تطبيق Werdk يقرأ رابط `avatar` مباشرة دون أي معالجة إضافية. |

نحن على أتم الاستعداد لتقديم أي استفسارات أو دعم إضافي يضمن نجاح الربط بسلاسة!
