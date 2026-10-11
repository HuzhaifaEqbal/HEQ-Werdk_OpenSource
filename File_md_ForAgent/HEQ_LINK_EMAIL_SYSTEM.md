# ✉️ منظومة وقوالب البريد الإلكتروني التفاعلي HEQ Link
## (Transactional Email System & Brevo HTML Templates Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **توثيق القالب الأساسي الفاخر (Master HTML Template):** تصميم متجاوب داكن باللون الأسود العميق متوافق مع كافة برامج البريد.
> * **قوالب رسائل التحقق (OTP & 2FA Templates):** تصميم كروت كود التحقق السداسي ونصوص الأمان التحذيرية.
> * **قوالب تنبيهات الأمان (Security Alerts):** إشعارات تسجيل الدخول من أجهزة جديدة، وتغيير كلمات المرور.
> * **تكامل خدمة Brevo (Sendinblue API):** استدعاء دالة `sendEmailBrevo` وتمرير المتغيرات النصية.
> * **الفئة المستهدفة:** مهندسو الواجهة الخلفية، مطورو قوالب البريد (Email Devs)، ومصممو واجهات المستخدم.

---

## 1. قالب البريد الأساسي (The Master Template)

نظام HEQ Link يستخدم دالة `sendEmailBrevo` لإرسال الرسائل عبر خدمة **Brevo (Sendinblue سابقاً)**.
النظام يغلف أي محتوى نصي (HTML) داخل قالب (Template) موحد يحمل هوية المنصة (اللون الأسود العميق والخطوط البيضاء) لضمان الفخامة والاحترافية.

هذا هو كود القالب الأساسي الذي يحيط بأي رسالة يتم إرسالها:

```html
<!-- القالب الأساسي (Master Wrapper) -->
<div dir="rtl" style="font-family: 'Segoe UI', Tahoma, sans-serif; background-color: #000000; padding: 20px; text-align: right; color: #ffffff;">
  <div style="max-width: 600px; margin: auto; background: #0a0a0a; border: 1px solid #222222; border-radius: 12px; padding: 25px;">
    
    <!-- Logo Header (الترويسة) -->
    <div style="padding-bottom: 15px; text-align: right; border-bottom: 1px solid #222222;">
      <h1 style="color: #ffffff; margin: 0; font-size: 22px; font-weight: 900; letter-spacing: 1px;">HEQ - Hajen</h1>
    </div>

    <!-- Main Content Area (محتوى الرسالة المتغير) -->
    <div style="padding: 25px 0; color: #cccccc; line-height: 1.8; font-size: 14px;">
      <!-- هنا يتم وضع محتوى الرسالة (HTML) -->
      ${html}
    </div>

    <!-- Footer Statement Area (التذييل) -->
    <div style="padding-top: 20px; font-size: 12px; color: #777777; border-top: 1px solid #222222; line-height: 1.5;">
      هذه الرسالة الإلكترونية مرسلة تلقائيا من النظام إلى "@username"<br><br>
      HEQ - Hajen<br>
      اللغة المدعومة الأساسية | العربية
    </div>
  </div>
</div>
```

---

## 2. أنواع رسائل البريد (Email Types)

بناءً على هذا القالب، يتم توليد عدة أنواع من الرسائل الديناميكية في النظام، وهذه هي الكتل البرمجية (HTML) الخاصة بكل نوع والتي يتم حقنها في مكان `${html}`:

### أ. رسائل التحقق (OTP & Verification)
تُستخدم عند إنشاء حساب جديد أو تفعيل ميزات الأمان (2FA).

```html
<h2 style="color: #00D2FF; margin-top: 0;">رمز التوثيق الخاص بك</h2>
<p>لقد طلبنا هذا الرمز للتحقق من هويتك، يرجى إدخال الرمز التالي في التطبيق:</p>
<div style="background: #111111; padding: 15px; border-radius: 8px; text-align: center; margin: 20px 0; border: 1px solid #333333;">
  <span style="font-size: 28px; font-weight: bold; letter-spacing: 4px; color: #ffffff;">123456</span>
</div>
<p style="color: #ff4444; font-size: 12px;">⚠️ تحذير: لا تشارك هذا الرمز مع أي شخص، فريقنا لن يطلب منك هذا الرمز أبداً.</p>
```

### ب. تنبيهات الأمان (Security Alerts)
تُرسل عند اكتشاف تسجيل دخول جديد أو من جهاز غير معروف (مثل تطبيق HEQ Werdk).

```html
<h2 style="color: #FFD700; margin-top: 0;">تنبيه أمني: تسجيل دخول جديد</h2>
<p>تم تسجيل دخول إلى حسابك من جهاز جديد، إليك التفاصيل:</p>
<ul style="list-style: none; padding: 0; margin: 15px 0; background: #111111; padding: 15px; border-radius: 8px; border: 1px dashed #444444;">
  <li style="margin-bottom: 8px;">📱 <strong>الجهاز:</strong> iPhone 14 Pro</li>
  <li style="margin-bottom: 8px;">📍 <strong>الموقع:</strong> دمشق، سوريا</li>
  <li style="margin-bottom: 0;">⏰ <strong>الوقت:</strong> 2026-09-25 19:30</li>
</ul>
<p>إذا لم تكن أنت من قام بتسجيل الدخول، يرجى تغيير كلمة المرور الخاصة بك فوراً.</p>
```

### ج. رسائل استعادة كلمة المرور (Password Recovery)
مهمة جداً للخطوة القادمة في Werdk.

```html
<h2 style="color: #00D2FF; margin-top: 0;">طلب إعادة تعيين كلمة المرور</h2>
<p>لقد تلقينا طلباً لإعادة تعيين كلمة المرور لحسابك. استخدم الرمز التالي للمتابعة:</p>
<div style="background: #111111; padding: 15px; border-radius: 8px; text-align: center; margin: 20px 0; border: 1px solid #333333;">
  <span style="font-size: 28px; font-weight: bold; letter-spacing: 4px; color: #ffffff;">987654</span>
</div>
<p>إذا لم تقم بهذا الطلب، يمكنك تجاهل هذه الرسالة بأمان.</p>
```

### د. الرسائل الإدارية (Admin Notifications)
تُرسل عند تفعيل الحسابات، التوثيق، أو التحذيرات.

```html
<h2 style="color: #00E676; margin-top: 0;">مبروك التوثيق! 🎉</h2>
<p>يسعدنا إخبارك بأنه تمت الموافقة على طلبك للحصول على شارة التوثيق في هَجين.</p>
<p>يمكنك الآن الاستمتاع بميزات الحسابات الموثقة والمصداقية العالية في المجتمع.</p>
```

---

## 3. كيفية الاستدعاء برمجياً (The API)

لإرسال أي من هذه الرسائل من الكود (سواء من HEQ Link أو إذا أردت استخدام نفس السيرفر لـ Werdk)، يتم استدعاء الدالة كالتالي:

```javascript
const { sendEmailBrevo } = require("../utils/helpers");

const email = "user@example.com";
const subject = "رمز استعادة كلمة المرور - HEQ Werdk";
const mailHtml = \`
  <h2 style="color: #FFD700; margin-top: 0;">استعادة الحساب</h2>
  <p>رمزك هو: <strong>123456</strong></p>
\`;

// سيقوم السيرفر تلقائياً بتغليف \`mailHtml\` داخل القالب الأسود الفخم وإرسالها
await sendEmailBrevo(email, subject, mailHtml);
```

## توصيات لمرحلة (حسابي - Werdk):
1. **استعادة كلمة المرور (Forgot Password):** يجب تصميم واجهة في فلاتر (Werdk) تطلب الإيميل، ثم تتصل بالباك إند لإرسال كود OTP عبر `sendEmailBrevo`.
2. **تغيير كلمة المرور (Change Password):** واجهة تطلب كلمة المرور القديمة والجديدة، وتتصل بمسار (Route) يقوم بتحديث الباسوورد المشفرة في قاعدة بيانات `users`.
3. **تحديث البيانات:** تحديث الاسم، رقم الهاتف، أو حذف الحساب. يجب إرسال إيميل "تنبيه أمان" عند تغيير أي بيانات حساسة.
