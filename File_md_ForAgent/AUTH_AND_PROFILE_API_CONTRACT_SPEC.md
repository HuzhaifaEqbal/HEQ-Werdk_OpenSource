# 🔐 مواصفة تكامل الـ API للمصادقة والملف الشخصي والمعلم الذكي
## (Auth, User Profile & Smart Tutor API Contract Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **توثيق نقاط اتصال المصادقة المتقدمة:** تسجيل الدخول بكلمة المرور، طلب رمز استعادة كلمة المرور عبر OTP، وإعادة تعيين كلمة المرور.
> * **إدارة الملف الشخصي وخطة التعلم:** جلب بيانات المستخدم وتحديث مسار التعلم وحساب الوقت التقديري لختم المنهج.
> * **محرك المعلم الذكي (`ask-tutor`):** استدعاء نموذج الذكاء الاصطناعي للإجابة عن أسئلة الطالب السياقية مع مؤشرات التحميل.
> * **معايير تجربة المستخدم والتعامل مع الأخطاء:** حظر استثناءات الكود الإنجليزية وعرض رسائل عربية تفاعلية.
> * **الفئة المستهدفة:** مهندسو الواجهة الأمامية (Flutter)، مهندسو الواجهة الخلفية (Node.js/Prisma)، ومطورو تكامل الـ REST APIs.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس أنظمة خلفية وتكامل واجهات برمجية (Senior Backend & API Integration Engineer):
> مهمتك هي بناء وتطبيق مواصفات الـ REST API للمصادقة وإدارة الملف الشخصي والمعلم الذكي (Smart Tutor) وفق المعايير المحددة في هذا المستند.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. عنوان الخادم الأساسي (Base URL): اضبط المتغير الأساسي على `https://your-api-domain.com/api/v1` واجعل الـ Host قابلاً للتكوين عبر متغيرات البيئة `your_api_env`.
> 2. مسارات تطبيق العميل (Flutter Client): ضع خدمات الاتصال والمستودعات في `your_project/lib/core/network/` و `your_project/lib/features/auth/`.
> 3. التزم بتنسيق طلبات واستجابات JSON، والتعامل الآمن مع التوكنات، ورسائل الخطأ العربية للمستخدم الموضحة في العقد الفني أدناه.
> ```

---

## 🔗 الرابط الأساسي للسيرفر (Base URL):
جميع المسارات تبدأ بـ:
```http
https://your-api-domain.com/api/v1
```

---

## 🔐 1. مسارات المصادقة المتقدمة (Authentication Endpoints)

### أ. تسجيل الدخول بكلمة المرور
- **المسار:** `POST /auth/login`
- **Request Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "SecretPassword123"
  }
  ```
- **Response Body:**
  ```json
  {
    "success": true,
    "token": "JWT_ACCESS_TOKEN_HERE",
    "user": {
      "id": 1,
      "email": "user@example.com",
      "name": "عبد الله"
    }
  }
  ```

### ب. طلب كود استعادة كلمة المرور (Forgot Password)
- **المسار:** `POST /auth/forgot-password`
- **Request Body:**
  ```json
  {
    "email": "user@example.com"
  }
  ```

### ج. التحقق وإعادة تعيين كلمة المرور (Reset Password)
- **المسار:** `POST /auth/reset-password`
- **Request Body:**
  ```json
  {
    "email": "user@example.com",
    "otp": "123456",
    "newPassword": "NewStrongPassword456"
  }
  ```

---

## 👤 2. مسارات الملف الشخصي وخطة التعلم (Profile & Onboarding)

### أ. جلب بيانات المستخدم الحالي
- **المسار:** `GET /user/me`
- **Headers:** `Authorization: Bearer <TOKEN>`
- **الوظيفة:** استرجاع بيانات الملف الشخصي، نقاط الخبرة (XP)، أيام الشعلة، والواحات المكتملة.

### ب. تحديث بيانات المستخدم وتحديد مسار التعلم
- **المسار:** `PUT /user/me`
- **Headers:** `Authorization: Bearer <TOKEN>`
- **Request Body:**
  ```json
  {
    "learningPath": "tajweed_scratch",
    "learningGoalMins": 15
  }
  ```
  *(الخيارات المتاحة لـ `learningPath`: `tajweed_scratch` أو `taharah_experienced`).*
- **Response Body:**
  ```json
  {
    "success": true,
    "estimation": "إذا التزمت بخطة 15 دقيقة ستختم التجويد خلال 80 يوماً!"
  }
  ```

---

## 🤖 3. محرك المعلم الذكي (Smart Tutor AI Assistant)

- **المسار:** `POST /user/ask-tutor`
- **Headers:** `Authorization: Bearer <TOKEN>`
- **Request Body:**
  ```json
  {
    "lessonContext": "نص الدرس الحالي وموضوع المسألة الفقهية أو الآية",
    "userQuestion": "ما الفرق بين الإظهار الحلقي والإظهار الشفوي؟"
  }
  ```
- **Response Body:**
  ```json
  {
    "success": true,
    "answer": "الإظهار الحلقي يتعلق بأحكام النون الساكنة والتنوين عند حروف الحلق الستة، بينما الإظهار الشفوي يتعلق بالميم الساكنة عند باقي الحروف ما عدا الميم والباء."
  }
  ```

---

## 🛡️ 4. قواعد الاستجابة والتعامل مع الأخطاء (Error Handling Standards)
1. **الرسائل الصديقة للمستخدم:** يتم اعتراض كافة الأخطاء (`catch (e)`) وعرض رسائل باللغة العربية واضحة دون أي مصطلحات تقنية أو استثناءات برمجية إنجليزية.
2. **إدارة جلسة المستخدم:** حفظ رمز الـ JWT بأمان في `flutter_secure_storage` وتجديده عند انتهاء الصلاحية.
