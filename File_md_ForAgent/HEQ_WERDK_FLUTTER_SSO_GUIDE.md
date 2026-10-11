# 📱 دليل تكامل المصادقة الموحدة لتطبيق فلاتر HEQ Werdk
## (Flutter Client Web SSO & Deep Link Integration Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **إعداد الروابط العميقة (Deep Links Setup):** تكوين ملفات AndroidManifest و iOS URL Schemes لاستقبال الرابط `your_scheme://auth_success`.
> * **دورة المصادقة عبر المتصفح الخارجي:** فتح رابط المصادقة عبر `url_launcher` والتقاط رمز المصادقة المرتجع (`code`).
> * **استماع الروابط العميقة ومعالجة التوكن:** كود فلاتر للالتقاط التلقائي عبر `app_links` واستدعاء سيرفر التطبيق لإنهاء تسجيل الدخول.
> * **الفئة المستهدفة:** مطورو تطبيقات الموبايل (Flutter Engineers)، ومطورو واجهات المستخدم.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس تطبيقات Flutter وخبير أمان الروابط العميقة (Mobile Security & Deep Links Engineer):
> مهمتك هي برمجة وإعداد دورة المصادقة الموحدة (SSO Flow) عبر المتصفح الخارجي واستقبال كود التفويض عبر Deep Links في تطبيق Flutter.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. إعدادات الروابط العميقة: استخدم البروتوكول العام `your_scheme://auth_success`.
> 2. استدعاءات الخوادم: اضبط رابط المصادقة على `https://your-auth-sso.com/api/sso/authorize` بمعرف `client_id=your_client_id` وتوجيه كود التحقق لسيرفرك على `https://your-api-domain.com/auth/sso-verify`.
> 3. التزم بتكوين حزمتي `url_launcher` و `app_links` وإجراءات الأمان المشروحة في هذا الدليل.
> ```

---

## 🔄 كيف تعمل دورة المصادقة (Flow)؟

1. المستخدم يضغط على زر "المتابعة بواسطة SSO" في التطبيق.
2. يقوم التطبيق بفتح المتصفح (Web Browser) على رابط المصادقة المخصص.
3. يقوم المستخدم بتسجيل الدخول (إن لزم الأمر) ويضغط "تأكيد ومتابعة".
4. سيرفر الـ SSO يقوم بإغلاق العملية وإعادة توجيه المتصفح إلى رابط عميق (Deep Link) مخصص لتطبيقك حاملاً معه كود المصادقة (`code`).
5. تطبيقك يستقبل الرابط، يقرأ الكود، ويرسله إلى سيرفر الباك إند الخاص بك للتحقق منه وإنهاء تسجيل الدخول.

---

## 🛠️ الخطوات المطلوبة برمجياً (في تطبيق الموبايل)

### 1. إعداد الروابط العميقة (Deep Links)
يجب إعداد الروابط العميقة في تطبيقك لكي يتمكن من استقبال الرابط: `your_scheme://auth_success`

**مثال لنظام Android (داخل `AndroidManifest.xml`):**
```xml
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <!-- استقبال الرابط العميق your_scheme://auth_success -->
    <data android:scheme="your_scheme" android:host="auth_success" />
</intent-filter>
```

### 2. فتح صفحة المصادقة في المتصفح
عندما يضغط المستخدم على زر تسجيل الدخول، استخدم حزمة مثل `url_launcher` لفتح الرابط التالي:

```dart
import 'package:url_launcher/url_launcher.dart';

Future<void> loginWithSso() async {
  // الرابط الرسمي للمصادقة في سيرفر SSO
  final Uri authUrl = Uri.parse(
    'https://your-auth-sso.com/api/sso/authorize'
    '?client_id=your_client_id'
    '&redirect_uri=your_scheme://auth_success'
  );

  // نستخدم mode: LaunchMode.externalApplication لفتح المتصفح الخارجي
  if (await canLaunchUrl(authUrl)) {
    await launchUrl(authUrl, mode: LaunchMode.externalApplication);
  } else {
    print('لا يمكن فتح رابط المصادقة');
  }
}
```

### 3. الاستماع لعودة المستخدم والتقاط الكود
استخدم حزمة مثل `app_links` أو `uni_links` لالتقاط الرابط عند عودة النظام من المتصفح إلى تطبيق Werdk:

```dart
import 'package:app_links/app_links.dart';

class SsoHandler {
  final _appLinks = AppLinks();

  void initDeepLinks() {
    _appLinks.uriLinkStream.listen((Uri? uri) {
      if (uri != null) {
        // التحقق مما إذا كان الرابط هو رابط العودة من مصادقة SSO
        if (uri.scheme == 'your_scheme' && uri.host == 'auth_success') {
          
          final String? code = uri.queryParameters['code'];
          final String? error = uri.queryParameters['error'];

          if (error != null) {
            // المستخدم قام بالضغط على "إلغاء والعودة" في صفحة الويب
            print('تم إلغاء عملية المصادقة بواسطة المستخدم');
            return;
          }

          if (code != null) {
            // ✅ نجاح! استلمنا الكود
            print('SSO Code Received: $code');
            
            // 🚀 الخطوة الأخيرة: 
            // أرسل هذا الكود إلى السيرفر الخاص بكم (Backend)
            sendCodeToBackend(code);
          }
        }
      }
    });
  }

  Future<void> sendCodeToBackend(String code) async {
    // 💡 يقوم مهندس الباك إند باستلام هذا الكود 
    // ثم يتواصل برمجياً مع سيرفر SSO للتحقق واستلام بيانات المستخدم (Server-to-Server).
    
    /* مثال توضيحي:
    final response = await http.post(
      Uri.parse('https://your-api-domain.com/auth/sso-verify'), 
      body: {'code': code}
    );
    if(response.statusCode == 200) { 
       // الدخول بنجاح وتوجيه المستخدم للرئيسية
    }
    */
  }
}
```

---

## 🔒 ملاحظات أمنية هامة للمهندس:
* **مدة صلاحية الكود:** الكود (`code`) المرفق في الرابط صالح لمدة **دقيقتين فقط (120 ثانية)** ويستخدم لمرة واحدة. يجب تمريره بسرعة للباك إند الخاص بكم.
* **الـ Client Secret:** يُمنع منعاً باتاً وضع المفتاح السري (`client_secret`) داخل تطبيق الفلاتر. عملية التحقق من الكود (استدعاء مسار `verify-code`) يجب أن تتم **حصراً في سيرفر Werdk** (Server-to-Server) للحفاظ على سرية النظام.
