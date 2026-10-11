# 💎 دليل الهوية البصرية ونظام التصميم الموحد (Hajen Design System)
## (Hajen Unified Visual Identity, Design Tokens & UI Guidelines)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **لوحة الألوان الرقمية وتوكينات التصميم (Design Tokens):** قيم HEX والتباين المطلق في الوضع الليلي والنهاري، والأزرق السماوي النيوني (`#00D2FF`) والذهب الملكي (`#D4AF37`).
> * **مبدأ الكتابة المباشرة على الشاشة (Direct Screen Typography):** التخلي عن الحشو الرمادي الصندوقي واعتماد الحقول المفتوحة مع الخطوط الرفيعة.
> * **أكواد النماذج المعيارية في فلاتر:** مكونات حقول الإدخال، الأزرار الكبسولية، الفواصل، والأيقونات.
> * **الفئة المستهدفة:** مصممو واجهات وتجربة المستخدم (UI/UX)، ومطورو الواجهات الأمامية (Flutter / Web).

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس تصميم واجهات ونظم تصميم متقدمة (Design System Lead & Flutter UI Engineer):
> مهمتك هي تطبيق وإنشاء مكتبة عناصر ونظام التصميم الموحد (Unified Minimalist Design System) في Flutter، والتي تدعم النمط الداكن الخالص (#000000) والأزرار الكبسولية والحقول المفتوحة والأسطح الزجاجية (Glassmorphism).
> 
> إرشادات التطبيق وبيئة العمل:
> 1. مسار المشروع: هيكل توكنات التصميم والمكونات داخل `your_project/lib/core/theme/` و `your_project/lib/core/widgets/`.
> 2. مكتبة الأيقونات والخطوط: اعتمد مسارات الأصول العامة مثل `your_project/assets/icons/` وخطوط جوجل (Cairo, Inter, Amiri).
> 3. التزم بنسب التباين، والألوان النيونية والذهبية، والأكواد المعيارية الموضحة في هذا الدليل الفني.
> ```

---

## 🎨 1. لوحة الألوان الأساسية ونسب التباين (Color Palette)

تم التخلي عن الخلفيات الرمادية الباهتة والحشو اللوني، واعتماد التباين المطلق مع لمسات الإضاءة النيونية:

| الاستخدام | الوضع الداكن (Dark Mode) | الوضع الفاتح (Light Mode) | الرمز البرمجي / Hex |
| :--- | :--- | :--- | :--- |
| **خلفية الشاشة الأساسية** | أسود نقي وخالص | أبيض نقي وخالص | Dark: `#000000` / Light: `#FFFFFF` |
| **النصوص والعناوين الرئيسية** | أبيض نقي | أسود داكن | Dark: `Colors.white` / Light: `Colors.black87` |
| **النصوص الثانوية والإرشادات** | شفافية بيضاء | شفافية سوداء | `textColor.withOpacity(0.65)` |
| **لون الهوية التفاعلي (Accent)** | أزرق سماوي نيون | أزرق سماوي نيون | `#00D2FF` |
| **اللمسات الجانبية: الأخضر الإسلامي (Secondary Accent)** | أخضر زمردي متوازن | أخضر زمردي متوازن | `#10B981` (`islamicGreen`) |
| **اللمسات الجانبية: الذهبي الملكي (Secondary Accent)** | ذهبي ملكي متوازن | ذهبي ملكي متوازن | `#D4AF37` (`royalGold`) |
| **الحدود والخطوط الفاصلة** | خط شعري خافت | خط شعري خافت | `textColor.withOpacity(0.12 - 0.15)` |
| **أزرار الأكشن التدميرية (Danger)** | أحمر ناري | أحمر ناري | `#FFFF4D4D` |
| **النجاح والتأكيد (Success)** | أخضر نيون | أخضر نيون | `#00E676` |

---

## ✍️ 2. مبدأ الكتابة المباشرة على الشاشة (Direct Screen Typography)

### ❌ كيف كان النظام القديم (Before):
- حقول إدخال محاطة بحاويات رمادية ثقيلة أو مربعات داخل مربعات (Boxes inside Cards).
- حشو بصري يجعل الشاشة مزدحمة وضيقة.

### ✅ كيف أصبح النظام الجديد (After):
- كتابة مباشرة على خلفية الشاشة (Directly on Canvas) بأحجام خطوط كبيرة ومريحة (`fontSize: 18-28`).
- خط سفلي رفيع جداً (Hairline Underline) يفصل بين الحقول.
- أيقونات SVG ناعمة مدمجة في يمين أو يسار الحقل (`suffixIcon` / `prefixIcon`).

```dart
// 📌 كود النموذج المعياري لحقول الإدخال المباشرة:
Column(
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    // 1. عنوان الحقل المصغر
    Text(
      t.email,
      style: TextStyle(
        fontSize: 13,
        fontWeight: FontWeight.w600,
        color: textColor.withOpacity(0.5),
      ),
    ),
    const SizedBox(height: 4),

    // 2. حقل الكتابة المباشر
    TextField(
      controller: _emailController,
      style: TextStyle(
        fontSize: 19,
        fontWeight: FontWeight.w600,
        color: textColor,
        fontFamily: 'Inter',
      ),
      decoration: InputDecoration(
        hintText: "heq@official.com",
        hintStyle: TextStyle(
          color: textColor.withOpacity(0.25),
          fontSize: 18,
        ),
        border: InputBorder.none,
        isDense: true,
        contentPadding: const EdgeInsets.symmetric(vertical: 8),
        suffixIcon: SvgPicture.asset(
          'assets/icons/email_outlined.svg',
          width: 20,
          height: 20,
          colorFilter: ColorFilter.mode(
            textColor.withOpacity(0.35),
            BlendMode.srcIn,
          ),
        ),
        suffixIconConstraints: const BoxConstraints(minWidth: 24, minHeight: 24),
      ),
    ),

    // 3. الخط الفاصل الرفيع (Hairline Divider)
    Divider(
      color: textColor.withOpacity(0.15),
      thickness: 1,
      height: 2,
    ),
  ],
)
```

---

## 💊 3. نظام الأزرار البيضاوية (Stadium Pill Buttons)

### المعايير البرمجية للأزرار:
- شكل كبسولة بيضاوية كاملة (`shape: const StadiumBorder()`).
- تباين لوني ذكي معكوس (High Inverted Contrast):
  - في الوضع الداكن: خلفية الزر بيضاء ناصعة (`#FFFFFF`) والكتابة سوداء (`#000000`).
  - في الوضع الفاتح: خلفية الزر سوداء فاحمة (`#000000`) والكتابة بيضاء (`#FFFFFF`).
- ثبات الارتفاع على `height: 52` مع مؤشر تحميل مدمج لمنع اهتزاز الشاشة.

```dart
// 📌 كود الزر البيضاوي الموحد (Stadium Pill Button):
SizedBox(
  width: double.infinity,
  height: 52,
  child: ElevatedButton(
    onPressed: _isLoading ? null : _handleAction,
    style: ElevatedButton.styleFrom(
      backgroundColor: isLight ? const Color(0xFF000000) : const Color(0xFFFFFFFF),
      foregroundColor: isLight ? const Color(0xFFFFFFFF) : const Color(0xFF000000),
      elevation: 0,
      shape: const StadiumBorder(),
      disabledBackgroundColor: isLight ? Colors.black26 : Colors.white24,
    ),
    child: _isLoading
        ? SizedBox(
            width: 22,
            height: 22,
            child: CircularProgressIndicator(
              strokeWidth: 2.2,
              color: isLight ? Colors.white : Colors.black,
            ),
          )
        : Text(
            t.continueButton,
            style: GoogleFonts.cairo(
              fontSize: 16,
              fontWeight: FontWeight.w700,
            ),
          ),
  ),
)
```

---

## 🔢 4. نظام مربعات الرموز الذكية (6-PIN Smart OTP Boxes)

تستخدم في كافة عمليات التحقق (Verify OTP, 2FA Login, 2FA Setup, Password Reset, Delete Account):

### الميزات البرمجية:
1. **اتجاه إجباري (LTR)**: لمنع انقلاب ترتيب الأرقام في الواجهة العربية.
2. **انتقال تلقائي للمربع التالي** فور إدخال أي رقم.
3. **رجوع وحذف تلقائي** عند الضغط على زر `Backspace` عبر `RawKeyboardListener`.
4. **دعم النسخ واللصق (Clipboard Paste Parsing)**: عند لصق 6 أرقام يتم ملء كافة المربعات فوراً.
5. **تنفيذ الإجراء تلقائياً (Auto-Submit)** عند اكتمال الرقم السادس دون الحاجة للنقر على زر.

```dart
// 📌 بناء المربع الفردي في الـ 6-PIN:
Widget _buildPinBox(int index, bool isLight, Color textColor) {
  return Container(
    width: 48,
    height: 56,
    alignment: Alignment.center,
    decoration: BoxDecoration(
      color: isLight ? Colors.black.withOpacity(0.02) : Colors.white.withOpacity(0.04),
      borderRadius: BorderRadius.circular(14),
      border: Border.all(
        color: _focusNodes[index].hasFocus
            ? const Color(0xFF00D2FF)
            : (isLight ? Colors.black.withOpacity(0.12) : Colors.white.withOpacity(0.16)),
        width: _focusNodes[index].hasFocus ? 2 : 1.2,
      ),
    ),
    child: RawKeyboardListener(
      focusNode: FocusNode(),
      onKey: (event) {
        if (event is RawKeyDownEvent &&
            event.logicalKey == LogicalKeyboardKey.backspace &&
            _controllers[index].text.isEmpty &&
            index > 0) {
          _focusNodes[index - 1].requestFocus();
          _controllers[index - 1].clear();
        }
      },
      child: TextField(
        controller: _controllers[index],
        focusNode: _focusNodes[index],
        keyboardType: TextInputType.number,
        textAlign: TextAlign.center,
        maxLength: 1,
        showCursor: false,
        style: GoogleFonts.inter(
          fontSize: 22,
          fontWeight: FontWeight.bold,
          color: textColor,
        ),
        decoration: const InputDecoration(
          counterText: '',
          border: InputBorder.none,
          contentPadding: EdgeInsets.zero,
        ),
        inputFormatters: [FilteringTextInputFormatter.digitsOnly],
        onChanged: (val) => _onDigitChanged(index, val),
      ),
    ),
  );
}
```

---

## 🔔 5. نظام التنبيهات العائمة (Floating Custom SnackBar)

بدلاً من الـ SnackBar الكلاسيكي الملتصق بأسفل الشاشة، تم اعتماد التوست العائم الأنيق:

```dart
// 📌 دالة إظهار التنبيهات الموحدة:
void _showSnackBar(String message, {bool isError = true}) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(
      content: Text(
        message,
        textAlign: TextAlign.center,
        style: GoogleFonts.cairo(
          fontWeight: FontWeight.w600,
          fontSize: 13.5,
          color: Colors.white,
        ),
      ),
      backgroundColor: isError ? const Color(0xFFFF4D4D) : const Color(0xFF00D2FF),
      behavior: SnackBarBehavior.floating,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
      margin: const EdgeInsets.symmetric(horizontal: 24, vertical: 16),
      duration: const Duration(seconds: 3),
    ),
  );
}
```

---

## 🧊 6. متى وكيف نحافظ على الزجاج المصنفر (Frosted Glassmorphism)؟

نظام التصميم الجديد لا يلغي الزجاج المصنفر، بل يضعه في **مكانه الصحيح والفاخر**:

1. **أين يُلغى الزجاج؟**
   - حقول الإدخال والنماذج المباشرة (استبدل بالكتابة المباشرة على الشاشة).
2. **أين يُحافظ على الزجاج المصنفر ويُعزز؟**
   - أشرطة التنقل العلوية والسفلية (`AppBar`, `BottomNavigationBar`).
   - القوائم السفلية المنبثقة (`ModalBottomSheet`).
   - بطاقات التراكب والحوارات المنبثقة (`Dialogs`).
   - مشغلات الميديا والكاميرا والوسائط الشفافة (`Media Overlay Sheets`).

```dart
// 📌 كود الزجاج المصنفر المعتمد بالمشروع الأساسي (GlassContainer):
import 'dart:ui';
import 'package:flutter/material.dart';

class GlassContainer extends StatelessWidget {
  final Widget child;
  final double? width;
  final double? height;
  final EdgeInsetsGeometry? padding;
  final EdgeInsetsGeometry? margin;
  final double borderRadius;
  final bool isLight;
  final BoxBorder? border;
  final Color? color;
  final VoidCallback? onTap;

  const GlassContainer({
    Key? key,
    required this.child,
    this.width,
    this.height,
    this.padding,
    this.margin,
    this.borderRadius = 16.0,
    this.isLight = false,
    this.border,
    this.color,
    this.onTap,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    final Color backgroundColor = isLight 
        ? Colors.white.withOpacity(0.5) 
        : Colors.white.withOpacity(0.08);
        
    final Color borderColor = isLight 
        ? Colors.black.withOpacity(0.1) 
        : Colors.white.withOpacity(0.2);

    Widget widget = Container(
      margin: margin,
      width: width,
      height: height == double.infinity ? null : height,
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(borderRadius),
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(isLight ? 0.05 : 0.2),
            blurRadius: 15,
            spreadRadius: 0,
          )
        ],
      ),
      child: ClipRRect(
        borderRadius: BorderRadius.circular(borderRadius),
        child: BackdropFilter(
          filter: ImageFilter.blur(sigmaX: 25.0, sigmaY: 25.0),
          child: Container(
            padding: padding,
            decoration: BoxDecoration(
              color: color ?? backgroundColor,
              borderRadius: BorderRadius.circular(borderRadius),
              border: border ?? Border.all(color: borderColor, width: 1.0),
            ),
            child: child,
          ),
        ),
      ),
    );

    if (onTap != null) {
      return GestureDetector(onTap: onTap, child: widget);
    }
    return widget;
  }
}
```

---

## 🌓 7. متطلبات الثيمات المزدوجة ودعم اللغات الثلاث (Dual Themes & Multi-Language)

> [!IMPORTANT]
> **قاعدة صارمة للتطوير:** عدم كتابة أي ألوان أو نصوص ثابتة ومباشرة في واجهات الشاشات.

### 1. الثيمات (Dark & Light Canvas):
- **الألوان الأساسية محصورة في "الأسود والأبيض"**:
  - في الوضع الداكن: الخلفية أسود نقي `#000000` والنصوص بيضاء `#FFFFFF`.
  - في الوضع الفاتح: الخلفية أبيض نقي `#FFFFFF` والنصوص سوداء `#000000`.
  - الألوان الثانوية (الأزرق النيوني، الأخضر، الأحمر) لا تُستخدم إلا عند الضرورة القصوى للدلالات الوظيفية فقط (حالة النجاح، الخطأ، التركيز).
- **المنع التام للحشو اللوني والبطاقات الملونة المتعددة**: الحفاظ على البساطة والمينيماليزم المطلق.

### 2. دعم اللغات الثلاث (Multi-Language Readiness):
- تجهيز كافة النصوص والمكونات لدعم **3 لغات**:
  1. **العربية (Arabic - ar)**: الخط الأساسي `GoogleFonts.notoSansArabic` (أو `amiri` للآيات القرآنية حصراً).
  2. **الإنجليزية (English - en)**: الخط الأساسي `GoogleFonts.inter`.
  3. **اللغة الإضافية (مثل الفرنسية fr أو الأردية ur)**.
- استخدام مفاتيح الترجمة المعيارية والابتعاد عن أي نصوص hardcoded في الشاشات.

---

## 🧭 8. خطة العمل لتوحيد باقي شاشات وميزات التطبيق (Roadmap)

1. **الخطوة الأولى (Clean Canvas)**: ضبط لون خلفية الشاشة إلى الأسود النقي `#000000` أو الأبيض النقي `#FFFFFF`.
2. **الخطوة الثانية (Typography)**: استخدام `GoogleFonts.notoSansArabic` للعربية و`GoogleFonts.inter` للأرقام والنصوص اللاتينية، و `GoogleFonts.amiri` للرسم القرآني فقط.
3. **الخطوة الثالثة (Inputs & Buttons)**: تحويل حقول الإدخال إلى النمط المباشر ذو الخط السفلي، وتحويل الأزرار إلى `Stadium Pill` بتباين معكوس.
4. **الخطوة الرابعة (Assets & Icons)**: استخدام أيقونات الـ SVG المعتمدة من مسار `assets/icons/`.
5. **الخطوة الخامسة (Localization & Theming)**: التحقق من التوافق الفوري مع الوضعين (Dark / Light) واللغات الثلاث.

