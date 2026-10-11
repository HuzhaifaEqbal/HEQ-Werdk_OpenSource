# 👤 دليل تصميم وبرمجة مراحل إنشاء الحساب
## (HEQ Account Creation Flow, Design Tokens & UI Architecture Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **فلسفة مسار إنشاء الحساب الثلاثي (3-Step Flow):** شاشة التسجيل الأولى، شاشة كود الـ OTP السداسية، ومعالج إكمال الحساب وإعداد البروفايل.
> * **مصفوفة الألوان الذهبية الملكية (Gold Theme Tokens):** قيم التدرجات الذهبية الفاخرة للأزرار والبطاقات.
> * **المكونات القابلة لإعادة الاستخدام في فلاتر (Reusable Widgets):** الأزرار الكبسولية (`StadiumBorder`)، مربعات الـ OTP المخصصة، ومؤشرات قوة كلمة المرور.
> * **الفئة المستهدفة:** مهندسو واجهات المستخدم في فلاتر، ومصممو تجربة المستخدم (UI/UX Designers).

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس واجهات مستخدم وتطبيقات Flutter محترف (Senior Flutter UI/UX Architect):
> مهمتك هي بناء وبرمجة تدفق إنشاء الحساب ثلاثي المراحل (3-Step Account Creation & Onboarding Flow) بتصميم فاخر (Luxury Gold & Dark Theme) متضمن شاشة التسجيل، التحقق بكود الـ OTP المكون من 6 خانات، ومعالج إعداد البروفايل والصور الرمزية.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. مسار المشروع: هيكل الواجهات والكود داخل `your_project/lib/features/auth/presentation/screens/` والمكونات في `your_project/lib/features/auth/presentation/widgets/`.
> 2. استدعاءات الـ API: وجه نداءات التسجيل والتحقق إلى `https://your-api-domain.com/api/v1/auth` عبر طبقة الـ Repository المعتمدة.
> 3. استخدم توكنات الألوان الذهبية والخطوط والأزرار الكبسولية المحددة في هذا المستند بدقة.
> ```

---

## 1. فلسفة التصميم ومصفوفة الألوان (Design Tokens)

### المفهوم الأساسي
* **النمط البصري:** مقتبس من تجربة **Twitter / X** العصرية (Minimalist & Direct).
* **الحقول المفتوحة (Open Flat Fields):** بدون حواف أو مربعات رمادية ثقيلة حول الحقول، بل كتابة مباشرة على الشاشة مع خط سفلي رفيع (`Divider`) يتأثر بلون النص مع شفافية خفيفة.
* **الخطوط:** 
  * للنصوص العربية والعناوين والأزرار: `GoogleFonts.cairo()`.
  * للأرقام والإيميلات وخانات الـ OTP: `GoogleFonts.inter()` أو `FontFamily: 'Inter'`.
* **الأزرار:** بيضاوية الشكل كبسولية (`shape: const StadiumBorder()`) بارتفاع ثابت `52px`.

### لوحة الألوان الذهبية المخصصة لتطبيق Werdk (Gold Theme Palette)

```dart
class HeqColors {
  // الألوان الأساسية الأصلية
  static const Color darkBg = Color(0xFF000000);
  static const Color lightBg = Color(0xFFFFFFFF);
  static const Color originalCyan = Color(0xFF00D2FF);

  // درجات اللون الذهبي الفاخر لتطبيق Werdk
  static const Color goldPrimary = Color(0xFFD4AF37);     // ذهبي كلاسيكي ناصع
  static const Color goldSecondary = Color(0xFFFFDF73);   // ذهبي فاتح للتدرجات والحدود
  static const Color goldDark = Color(0xFF996515);        // ذهبي داكن للظلال والتباين
  static const Color goldSurface = Color(0xFF1C1914);     // خلفية بطاقات داكنة بلمسة ذهبية

  // تدرج لوني ذهبي فاخر للأزرار والبطاقات
  static const LinearGradient goldGradient = LinearGradient(
    colors: [Color(0xFFFFDF73), Color(0xFFD4AF37), Color(0xFF996515)],
    begin: Alignment.topLeft,
    end: Alignment.bottomRight,
  );
}
```

---

## 2. خريطة مراحل إنشاء الحساب الثلاث (The 3-Step Flow)

```
[ شاشة التسجيل الأولى ]   --->   [ شاشة كود الـ OTP ]   --->   [ معالج إكمال الحساب ]
  1. Signup Screen               2. VerifyScreen (6-PIN)       3. ProfileSetupScreen
  - الاسم الكامل                   - 6 مربعات منفصلة              - خطوة 1: الصورة الرمزية
  - البريد الإلكتروني              - لصق الرمز التلقائي           - خطوة 2: الاسم والنبذة والهدف
  - كلمة المرور ومؤشر قوتها       - عداد 60 ثانية لإعادة الإرسال   - خطوة 3: الدولة والميلاد والخصوصية
  - زر المتابعة الكبسولي          - زر فتح تطبيق الإيميل         - زر الانطلاق للرئيسية
```

---

## 3. الكتل البرمجية الأساسية القابلة لإعادة الاستخدام (Ready-to-use Reusable Widgets)

### أ. زر الإجراء الرئيسي القابل للتخصيص (الأصلي + الذهبي)
هذا المكون يدعم النمط الأصلي (أبيض وأسود) أو النمط الذهبي الفاخر:

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

enum ButtonThemeStyle {
  monochrome, // النمط الأصلي لتطبيق HEQ Link (أبيض في الداكن / أسود في الفاتح)
  solidGold,  // ذهبي مصمت للأزرار البارزة
  gradientGold // تدرج ذهبي ملكي فاخر
}

class HeqPrimaryButton extends StatelessWidget {
  final String text;
  final VoidCallback? onPressed;
  final bool isLoading;
  final ButtonThemeStyle style;

  const HeqPrimaryButton({
    super.key,
    required this.text,
    required this.onPressed,
    this.isLoading = false,
    this.style = ButtonThemeStyle.solidGold, // القيمة الافتراضية
  });

  @override
  Widget build(BuildContext context) {
    final isLight = Theme.of(context).brightness == Brightness.light;

    // 1. تحديد الألوان حسب الستايل
    Color btnBgColor;
    Color btnTextColor;

    switch (style) {
      case ButtonThemeStyle.monochrome:
        btnBgColor = isLight ? const Color(0xFF000000) : const Color(0xFFFFFFFF);
        btnTextColor = isLight ? const Color(0xFFFFFFFF) : const Color(0xFF000000);
        break;
      case ButtonThemeStyle.solidGold:
        btnBgColor = const Color(0xFFD4AF37);
        btnTextColor = const Color(0xFF000000);
        break;
      case ButtonThemeStyle.gradientGold:
        btnBgColor = Colors.transparent;
        btnTextColor = const Color(0xFF000000);
        break;
    }

    Widget content = isLoading
        ? SizedBox(
            width: 22,
            height: 22,
            child: CircularProgressIndicator(
              strokeWidth: 2.2,
              color: btnTextColor,
            ),
          )
        : Text(
            text,
            style: GoogleFonts.cairo(
              fontSize: 16,
              fontWeight: FontWeight.w700,
              color: btnTextColor,
            ),
          );

    return SizedBox(
      width: double.infinity,
      height: 52,
      child: style == ButtonThemeStyle.gradientGold
          ? Container(
              decoration: BoxDecoration(
                gradient: const LinearGradient(
                  colors: [Color(0xFFFFDF73), Color(0xFFD4AF37), Color(0xFFA67C1E)],
                  begin: Alignment.topLeft,
                  end: Alignment.bottomRight,
                ),
                borderRadius: BorderRadius.circular(100),
              ),
              child: ElevatedButton(
                onPressed: isLoading ? null : onPressed,
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.transparent,
                  shadowColor: Colors.transparent,
                  shape: const StadiumBorder(),
                ),
                child: content,
              ),
            )
          : ElevatedButton(
              onPressed: isLoading ? null : onPressed,
              style: ElevatedButton.styleFrom(
                backgroundColor: btnBgColor,
                foregroundColor: btnTextColor,
                elevation: 0,
                shape: const StadiumBorder(),
                disabledBackgroundColor: isLight ? Colors.black26 : Colors.white24,
              ),
              child: content,
            ),
    );
  }
}
```

---

### ب. رسائل التوست العائمة المخصصة (Golden & Status SnackBar)
طريقة إظهار التوست العائم مع دعم الحالة الذهبية وحالات الخطأ والنجاح:

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

enum ToastState { success, error, goldNotice }

void showHeqToast(BuildContext context, String message, {ToastState state = ToastState.goldNotice}) {
  Color bgColor;
  Color textColor = Colors.white;

  switch (state) {
    case ToastState.error:
      bgColor = const Color(0xFFFF4D4D); // أحمر للأخطاء
      break;
    case ToastState.success:
      bgColor = const Color(0xFF00E676); // أخضر للنجاح
      break;
    case ToastState.goldNotice:
      bgColor = const Color(0xFFD4AF37); // ذهبي للتنبيهات والترحيب
      textColor = Colors.black; // نص أسود فوق الخلفية الذهبية لضمان التباين
      break;
  }

  ScaffoldMessenger.of(context).hideCurrentSnackBar();
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(
      content: Text(
        message,
        textAlign: TextAlign.center,
        style: GoogleFonts.cairo(
          fontWeight: FontWeight.w700,
          fontSize: 13.5,
          color: textColor,
        ),
      ),
      backgroundColor: bgColor,
      behavior: SnackBarBehavior.floating,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(14)),
      margin: const EdgeInsets.symmetric(horizontal: 24, vertical: 16),
      duration: const Duration(seconds: 3),
    ),
  );
}
```

---

### ج. مكون حقل الإدخال بنمط الشاشة المباشرة (Minimalist Text Field)

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

class MinimalistInputField extends StatelessWidget {
  final String label;
  final String hint;
  final TextEditingController controller;
  final TextInputType keyboardType;
  final TextInputAction textInputAction;
  final bool obscureText;
  final Widget? suffixIcon;
  final ValueChanged<String>? onChanged;
  final ValueChanged<String>? onSubmitted;
  final bool isInterFont;

  const MinimalistInputField({
    super.key,
    required this.label,
    required this.hint,
    required this.controller,
    this.keyboardType = TextInputType.text,
    this.textInputAction = TextInputAction.next,
    this.obscureText = false,
    this.suffixIcon,
    this.onChanged,
    this.onSubmitted,
    this.isInterFont = false,
  });

  @override
  Widget build(BuildContext context) {
    final isLight = Theme.of(context).brightness == Brightness.light;
    final textColor = isLight ? Colors.black87 : Colors.white;

    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text(
          label,
          style: TextStyle(
            fontSize: 13,
            fontWeight: FontWeight.w600,
            color: textColor.withOpacity(0.5),
          ),
        ),
        const SizedBox(height: 4),
        TextField(
          controller: controller,
          keyboardType: keyboardType,
          textInputAction: textInputAction,
          obscureText: obscureText,
          onChanged: onChanged,
          onSubmitted: onSubmitted,
          style: isInterFont
              ? TextStyle(
                  fontSize: 19,
                  fontWeight: FontWeight.w600,
                  color: textColor,
                  fontFamily: 'Inter',
                )
              : GoogleFonts.cairo(
                  fontSize: 19,
                  fontWeight: FontWeight.w600,
                  color: textColor,
                ),
          decoration: InputDecoration(
            hintText: hint,
            hintStyle: TextStyle(
              color: textColor.withOpacity(0.25),
              fontSize: 18,
            ),
            border: InputBorder.none,
            isDense: true,
            contentPadding: const EdgeInsets.symmetric(vertical: 8),
            suffixIcon: suffixIcon,
            suffixIconConstraints: const BoxConstraints(minWidth: 24, minHeight: 24),
          ),
        ),
        Divider(
          color: textColor.withOpacity(0.15),
          thickness: 1,
          height: 2,
        ),
      ],
    );
  }
}
```

---

### د. مؤشر قوة كلمة المرور المباشر (Password Strength Meter)

```dart
class PasswordStrengthWidget extends StatelessWidget {
  final int strengthLevel; // 0=none, 1=weak, 2=fair, 3=good, 4=strong
  final Color strengthColor;
  final double strengthPercent;

  const PasswordStrengthWidget({
    super.key,
    required this.strengthLevel,
    required this.strengthColor,
    required this.strengthPercent,
  });

  @override
  Widget build(BuildContext context) {
    if (strengthLevel == 0) return const SizedBox.shrink();

    final isLight = Theme.of(context).brightness == Brightness.light;
    final labels = ['', 'ضعيفة', 'مقبولة', 'جيدة', 'قوية جداً'];

    return Column(
      children: [
        const SizedBox(height: 12),
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceBetween,
          children: [
            Text(
              labels[strengthLevel],
              style: TextStyle(color: strengthColor, fontSize: 12, fontWeight: FontWeight.bold),
            ),
            Text(
              "أمان كلمة المرور",
              style: TextStyle(
                color: (isLight ? Colors.black : Colors.white).withOpacity(0.35),
                fontSize: 12,
              ),
            ),
          ],
        ),
        const SizedBox(height: 6),
        ClipRRect(
          borderRadius: BorderRadius.circular(8),
          child: LinearProgressIndicator(
            value: strengthPercent,
            backgroundColor: isLight ? Colors.black.withOpacity(0.06) : Colors.white.withOpacity(0.1),
            color: strengthColor,
            minHeight: 4,
          ),
        ),
      ],
    );
  }
}
```

---

### هـ. مربعات إدخال كود التحقق السداسي (6-PIN OTP Input)

هذا الكود يدعم:
1. التنقل التلقائي للخانة التالية عند الكتابة.
2. دعم الرجوع عند الحذف (`Backspace`).
3. إمكانية لصق الرمز كاملاً دفعة واحدة (`Paste full 6 digits`).
4. التمييز بالحد الذهبي عند التركيز (`Focus`).

```dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:google_fonts/google_fonts.dart';

class SixDigitOtpField extends StatefulWidget {
  final ValueChanged<String> onCompleted;
  final Color activeBorderColor;

  const SixDigitOtpField({
    super.key,
    required this.onCompleted,
    this.activeBorderColor = const Color(0xFFD4AF37), // ذهبي عند التركيز
  });

  @override
  State<SixDigitOtpField> createState() => _SixDigitOtpFieldState();
}

class _SixDigitOtpFieldState extends State<SixDigitOtpField> {
  final List<TextEditingController> _controllers = List.generate(6, (_) => TextEditingController());
  final List<FocusNode> _focusNodes = List.generate(6, (_) => FocusNode());

  @override
  void dispose() {
    for (var c in _controllers) {
      c.dispose();
    }
    for (var f in _focusNodes) {
      f.dispose();
    }
    super.dispose();
  }

  void _onDigitChanged(int index, String value) {
    if (value.length > 1) {
      // التعامل مع اللصق المباشر (Paste)
      final digits = value.replaceAll(RegExp(r'\D'), '');
      for (int i = 0; i < 6 && i < digits.length; i++) {
        _controllers[i].text = digits[i];
      }
      if (digits.length >= 6) {
        _focusNodes[5].unfocus();
        widget.onCompleted(_controllers.map((c) => c.text).join());
      } else {
        _focusNodes[digits.length].requestFocus();
      }
      return;
    }

    if (value.isNotEmpty) {
      if (index < 5) {
        _focusNodes[index + 1].requestFocus();
      } else {
        _focusNodes[index].unfocus();
        final fullCode = _controllers.map((c) => c.text).join();
        if (fullCode.length == 6) {
          widget.onCompleted(fullCode);
        }
      }
    }
  }

  @override
  Widget build(BuildContext context) {
    final isLight = Theme.of(context).brightness == Brightness.light;
    final textColor = isLight ? Colors.black87 : Colors.white;

    return Directionality(
      textDirection: TextDirection.ltr, // لضمان تدفق الأرقام من اليسار لليمين
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: List.generate(6, (index) {
          return Container(
            width: 48,
            height: 56,
            alignment: Alignment.center,
            decoration: BoxDecoration(
              color: isLight ? Colors.black.withOpacity(0.02) : Colors.white.withOpacity(0.04),
              borderRadius: BorderRadius.circular(14),
              border: Border.all(
                color: _focusNodes[index].hasFocus
                    ? widget.activeBorderColor
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
        }),
      ),
    );
  }
}
```

---

### و. شريط مؤشر الخطوات الثلاث لمعالج الملف الشخصي (Profile Step Indicator)

```dart
Widget buildHeqStepIndicator(int currentStep, {Color activeColor = const Color(0xFFD4AF37)}) {
  return Builder(builder: (context) {
    final isLight = Theme.of(context).brightness == Brightness.light;
    return Row(
      mainAxisSize: MainAxisSize.min,
      children: List.generate(3, (index) {
        final step = index + 1;
        final isActive = step <= currentStep;
        final isCurrent = step == currentStep;
        return Row(
          children: [
            AnimatedContainer(
              duration: const Duration(milliseconds: 250),
              width: isCurrent ? 28 : 22,
              height: 6,
              decoration: BoxDecoration(
                color: isActive
                    ? activeColor
                    : (isLight ? Colors.black.withOpacity(0.1) : Colors.white.withOpacity(0.15)),
                borderRadius: BorderRadius.circular(10),
              ),
            ),
            if (index < 2) const SizedBox(width: 6),
          ],
        );
      }),
    );
  });
}
```

---

### ز. مكون اختيار وقص الصورة الرمزية (Circular Avatar Picker)

```dart
Widget buildAvatarPicker({
  required File? imageFile,
  required VoidCallback onTap,
  Color accentColor = const Color(0xFFD4AF37),
  required BuildContext context,
}) {
  final isLight = Theme.of(context).brightness == Brightness.light;

  return Center(
    child: GestureDetector(
      onTap: onTap,
      child: Stack(
        children: [
          Container(
            width: 140,
            height: 140,
            decoration: BoxDecoration(
              color: isLight ? Colors.black.withOpacity(0.04) : Colors.white.withOpacity(0.06),
              shape: BoxShape.circle,
              border: Border.all(
                color: imageFile != null
                    ? accentColor
                    : (isLight ? Colors.black.withOpacity(0.12) : Colors.white.withOpacity(0.18)),
                width: 2,
              ),
              image: imageFile != null
                  ? DecorationImage(image: FileImage(imageFile), fit: BoxFit.cover)
                  : null,
            ),
            child: imageFile == null
                ? Center(
                    child: Icon(
                      Icons.add_a_photo_outlined,
                      size: 40,
                      color: accentColor,
                    ),
                  )
                : null,
          ),
          if (imageFile != null)
            Positioned(
              bottom: 0,
              right: 0,
              child: Container(
                padding: const EdgeInsets.all(8),
                decoration: BoxDecoration(
                  color: accentColor,
                  shape: BoxShape.circle,
                ),
                child: const Icon(Icons.edit_rounded, size: 16, color: Colors.black),
              ),
            ),
        ],
      ),
    ),
  );
}
```

---

## 4. ملخص إرشادات التطبيق في HEQ Werdk

1. **الخلفية العامة:** استخدم دائماً خلفية نقية تماماً `Color(0xFF000000)` للوضع الليلي و `Color(0xFFFFFFFF)` للوضع النهاري.
2. **شريط الإجراءات السفلي (Sticky Bottom Actions):**
   * اجعل الزر الرئيسي `HeqPrimaryButton` مثبتاً في أسفل الشاشة داخل `SafeArea` و `Padding(horizontal: 26, vertical: 16)`.
3. **الحواف والكبسولات:**
   * الحقول ذات خط سفلي بدون برواز (`border: InputBorder.none`).
   * الأزرار كبسولية دائرية بالكامل (`StadiumBorder`).
   * المربعات وخانات الـ OTP بزوايا ناعمة دائرية بمقدار `14px`.
4. **اللمسة الذهبية:**
   * اجعل الأزرار التفاعلية الرئيسية بلون ذهبي `Color(0xFFD4AF37)` مع نص أسود.
   * إشعار التوست للترحيب أو النجاح باللون الذهبي (`ToastState.goldNotice`).
   * مؤشر التركيز للـ PIN ومؤشر الخطوات باللون الذهبي.
