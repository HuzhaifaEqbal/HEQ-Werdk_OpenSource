# 🦉 الدليل الشامل لتميمة التطبيق وحالات الحركة
## (3D Hoopoe Mascot Character Identity & Animation States Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **هوية تميمة الهدهد (Character Identity):** الأبعاد الثلاثية، الإضاءة الناعمة، لوحة الألوان الرسمية، ومراجع التوليد المتسق.
> * **سجل حالات الحركة الكامل (Complete Animation Matrix):** الحركات الأساسية (Idle, Fly, Landing)، حركات الدرس (Thinking, Reading, Explaining)، وحركات التقييم (Correct, Wrong, Celebrate, Boss).
> * **المعايير التقنية للتصدير:** صيغ Animated WebP الشفافة، دقة 512x512، معدل الإطارات، والتكامل في فلاتر عبر `MascotWidget`.
> * **الفئة المستهدفة:** مصممو الرسوم المتحركة (3D Animators)، مهندسو التوجيه (Prompt Engineers)، ومطورو Flutter.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Midjourney / Runway / Kling / Flux / GPT):**
> ```text
> بصفتك خبير تصميم شخصيات ثلاثية الأبعاد وتحريك متقدم (3D Pixar-Style Character Animator):
> مهمتك هي تصميم وتوليد الحركات التفاعلية لتميمة الهدهد التعليمية (Hoopoe Mascot) بدقة متسقة ونمط بيكسار، مع خلفية شفافة وصيغة Animated WebP.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. روابط التخزين والأصول: اضبط روابط الأصول على `https://your-cdn-assets.com/mascot/your_file.webp`.
> 2. كود الاستدعاء في Flutter: ضع المكون داخل `your_project/lib/features/tutor/widgets/mascot_widget.dart`.
> 3. التزم بمصفوفة الحركات (Idle, Thinking, Correct, Wrong, Combo, Boss) والبرومبتات المحددة تفصيلياً في هذا الدليل.
> ```

---

## 🦉 هوية الشخصية (Mascot Identity)

### الشخصية المختارة: الهدهد (Hoopoe)

| العنصر | التفاصيل |
|--------|---------|
| **الاسم** | الهدهد — Hoopoe |
| **المرجع القرآني** | قصة نبي الله سليمان عليه السلام (سورة النمل) |
| **سبب الاختيار** | تاجه الريشي المعبّر، ارتباطه القرآني، شكله محبوب ومميز |
| **الأسلوب** | Cute 3D — يشبه أسلوب بيكسار |
| **الإضاءة** | Soft Lighting — ناعمة ودافئة |
| **زاوية الكاميرا** | 3/4 View (مائلة قليلاً للأمام) |
| **الخلفية** | شفافة (Transparent PNG / WebP) |

### لوحة الألوان:

| اللون | الكود | الاستخدام |
|-------|-------|-----------|
| ذهبي عميق | `#C9A227` | التاج الريشي والتفاصيل |
| سيان | `#00BCD4` | الجناحين والجسم |
| أخضر إسلامي | `#2E7D32` | الزخارف والتفاصيل |
| كريمي فاتح | `#FFF8E1` | الصدر والبطن |
| بني دافئ | `#795548` | المنقار والأرجل |

---

## 🎨 ضبط ثبات الشخصية (Consistency Settings)

> ⚠️ **مهم جداً:** قبل كل توليد، تأكد من هذه الإعدادات:

```
✅ استخدم نفس الـ Seed في كل مرة
✅ الخلفية: Transparent أو Green Screen (#00FF00)
✅ الزاوية: 3/4 View أو Front View فقط
✅ الصيغة: Animated WebP شفافة
✅ المدة: 3 إلى 5 ثوانٍ لكل حركة
✅ الحجم: 512x512 px كحد أدنى
```

**الـ Seed المعتمد والمرجع:**
```
Seed: 20260920134231
Character Reference URL: https://your-cdn-assets.com/mascot/A_cute_3D_Hoopoe_bird.jpeg
```

---

## ✅ قائمة الحركات الكاملة

---

### 🟢 الحركات الأساسية (للشاشات العامة)

---

#### [ ] 1. Idle — حركة الانتظار

**متى تُستخدم:** شاشة الخريطة، شاشة الاختيار، أي وقت انتظار  
**المدة:** 4 ثوانٍ (Loop لا نهائي)

**وصف الحركة:**
- تنفس بطيء وهادئ (الجسم يرتفع وينخفض قليلاً)
- رمشة بالعين كل ثانيتين
- ابتسامة خفيفة ثابتة
- التاج يتمايل برفق كأنه في نسيم خفيف

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, soft warm lighting.
The bird has a golden crown of feathers on its head, cyan-blue wings, cream-colored chest, and a brown beak.
Animation: gentle breathing idle loop — chest slowly rises and falls, eyes blink softly every 2 seconds,
a subtle warm smile, the crown feathers sway gently like in a soft breeze.
Background: transparent.
Camera: 3/4 front view, slightly low angle.
Style: Disney Pixar, cute 3D, soft shadows, subsurface scattering on feathers.
Duration: 4 seconds seamless loop.
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/loop.webp`

---

#### [ ] 2. Loading — حركة التحميل (اختيارية)

**متى تُستخدم:** أثناء تحميل الدرس، انتظار البيانات  
**المدة:** 3 ثوانٍ (Loop)

**وصف الحركة:**
- الهدهد يمسك كتاباً صغيراً مفتوحاً
- عيناه تتحركان على الصفحة يميناً ويساراً بسرعة
- يومض بين الحين والآخر كأنه يتعلم

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, holding a tiny open golden book.
Animation: the bird's eyes scan the book left and right quickly, occasionally looking up with curiosity,
blinking with wonder. The book glows slightly with a warm golden light.
Background: transparent.
Camera: 3/4 front view.
Style: Disney Pixar, cute 3D, warm soft lighting.
Duration: 3 seconds seamless loop.
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/Hoopoe_bird_reading_book.webp`

---

### 🔵 حركات جلسة الدرس (Lesson Session)

---

#### [ ] 3. Thinking — حركة التفكير

**متى تُستخدم:** أثناء قراءة المستخدم للسؤال، قبل اختيار الإجابة  
**المدة:** 3-4 ثوانٍ (Loop)

**وصف الحركة:**
- يضع جناحه على منقاره
- ينظر للأعلى اليسار بعيون مفكرة
- التاج يرتفع قليلاً (إشارة تركيز)
- يومض ببطء

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, in a thinking pose.
Animation: the bird places the tip of its wing gently under its beak/chin, looks upward-left with thoughtful eyes,
the crown feathers raise slightly indicating concentration, slow blinking, subtle swaying motion.
Background: transparent.
Camera: 3/4 front view.
Style: Disney Pixar, cute 3D, soft warm lighting, expressive eyes.
Duration: 3 seconds seamless loop.
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/thinking.webp`

---

#### [ ] 4. Correct Answer — إجابة صحيحة

**متى تُستخدم:** بعد إجابة صحيحة أو إتمام العقدة بنجاح  
**المدة:** 3 ثوانٍ (يُشغَّل مرة واحدة — no loop)

> 💡 **ملاحظة توجيهية لفريق العمل:** يُفضل عرض هذه التوليدات بعد اجتياز العقدة/الجزء كاملاً لتقليل الحشو البصري، ونكتفي برسائل التفاعل الفوري الخفيفة في الشاشة أثناء الأسئلة الفردية.

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, celebrating a correct answer.
Animation: the bird does a happy little jump, its crown feathers fan out with excitement,
wings open slightly, gives a thumbs-up gesture with one wing, wide joyful smile,
golden sparkles and small stars burst around it.
Background: transparent.
Camera: 3/4 front view, slightly dynamic angle.
Style: Disney Pixar, cute 3D, celebratory, bright warm lighting, golden particle effects.
Duration: 3 seconds, play once (no loop).
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/ThumbsUp.webp`

---

#### [ ] 5. Incorrect Answer — إجابة خاطئة

**متى تُستخدم:** عند التعثر أو الحاجة لإعادة المحاولة  
**المدة:** 4 ثوانٍ (يُشغَّل مرة واحدة)

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, reacting to a wrong answer gently.
Animation sequence:
1. Eyes close softly, head shakes gently side to side (not aggressively)
2. One wing raises to touch the top of its head with a mild surprised expression
3. Crown feathers lower slightly
4. Then immediately: head lifts back up, warm encouraging smile appears, gives a gentle nod
Background: transparent.
Camera: 3/4 front view.
Style: Disney Pixar, cute 3D, soft sympathetic lighting, gentle and encouraging mood.
Duration: 4 seconds, play once (no loop).
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/IncorrectAnswer.webp`

---

### 🔥 حركات الحماس والتحديات (Gamification & Boss Levels)

---

#### [ ] 6. Combo — متتالية صحيحة

**متى تُستخدم:** عند الإجابة الصحيحة على 3 أسئلة متتالية  
**المدة:** 3 ثوانٍ (يُشغَّل مرة واحدة)

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, in an excited combo reaction.
Animation: the bird vibrates with energy, a golden aura or gentle fire halo surrounds it,
crown feathers glow and stand tall, eyes shimmer with excitement, wings flutter rapidly,
the bird bounces with electric enthusiasm.
Background: transparent.
Camera: 3/4 front view, slightly dynamic.
Style: Disney Pixar, cute 3D, high energy, golden glowing lighting effects, electric excitement.
Duration: 3 seconds, play once (no loop).
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/Combo.webp`

---

#### [ ] 7. Boss Excellent — نجاح ساحق في التحدي

**متى تُستخدم:** عند اجتياز اختبار Boss Level بنتيجة ممتازة  
**المدة:** 5 ثوانٍ (يُشغَّل مرة واحدة — احتفالي فاخر)

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, celebrating a boss level victory.
Animation: the bird triumphantly raises a small golden trophy cup above its head with both wings,
colorful confetti rains down from above, crown feathers shimmer and sparkle gold,
the biggest and most joyful smile possible, golden stars and fireworks burst around it.
Background: transparent.
Camera: 3/4 front view, slightly low angle looking up at the trophy.
Style: Disney Pixar, cute 3D, grand celebration, bright golden lighting, festive particle effects.
Duration: 5 seconds, play once (no loop).
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/BossExcellent.webp`

---

#### [ ] 8. Boss Fail — رسوب في التحدي

**متى تُستخدم:** عند عدم اجتياز اختبار Boss Level  
**المدة:** 4 ثوانٍ (يُشغَّل مرة واحدة)

**برومبت التوليد:**
```text
A cute 3D Hoopoe bird character in Pixar animation style, reacting to a boss level failure with resilience.
Animation:
1. The bird wipes sweat from its forehead with one wing (tired but not defeated expression)
2. Crown feathers tilt slightly to one side
3. The bird holds up a small wooden sign that reads "Try Again!" with a small star on it
4. Ends with an encouraging nod and a tired-but-hopeful smile
Background: transparent.
Camera: 3/4 front view.
Style: Disney Pixar, cute 3D, warm sympathetic lighting, encouraging and resilient mood.
Duration: 4 seconds, play once (no loop).
Output: animated WebP with transparent background.
```
url: `https://your-cdn-assets.com/mascot/BossFail.webp`

---

## 🔗 روابط الاستدعاء (CDN Links)

```yaml
mascot_animations:
  idle:            "https://your-cdn-assets.com/mascot/idle.webp"
  loading:         "https://your-cdn-assets.com/mascot/loading.webp"
  thinking:        "https://your-cdn-assets.com/mascot/thinking.webp"
  correct_answer:  "https://your-cdn-assets.com/mascot/correct_answer.webp"
  incorrect_answer: "https://your-cdn-assets.com/mascot/incorrect_answer.webp"
  combo:           "https://your-cdn-assets.com/mascot/combo.webp"
  boss_excellent:  "https://your-cdn-assets.com/mascot/boss_excellent.webp"
  boss_fail:       "https://your-cdn-assets.com/mascot/boss_fail.webp"
```

---

## 📱 تكامل Flutter — كيفية الاستخدام

### إعداد الـ Package:
```yaml
# pubspec.yaml
dependencies:
  flutter:
    sdk: flutter
  extended_image: ^8.1.1   # دعم WebP متحرك
```

### المتغيرات الثابتة:
```dart
// your_project/lib/constants/mascot_urls.dart
class MascotAnimations {
  static const String baseUrl = 'https://your-cdn-assets.com/mascot/';

  static const String idle           = '${baseUrl}idle.webp';
  static const String loading        = '${baseUrl}loading.webp';
  static const String thinking       = '${baseUrl}thinking.webp';
  static const String correctAnswer  = '${baseUrl}correct_answer.webp';
  static const String incorrectAnswer = '${baseUrl}incorrect_answer.webp';
  static const String combo          = '${baseUrl}combo.webp';
  static const String bossExcellent  = '${baseUrl}boss_excellent.webp';
  static const String bossFail       = '${baseUrl}boss_fail.webp';
}
```

### Widget جاهز:
```dart
// your_project/lib/widgets/mascot_widget.dart
import 'package:flutter/material.dart';
import 'package:extended_image/extended_image.dart';
import '../constants/mascot_urls.dart';

class MascotWidget extends StatelessWidget {
  final String animationUrl;
  final double size;

  const MascotWidget({
    Key? key,
    required this.animationUrl,
    this.size = 150,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return ExtendedImage.network(
      animationUrl,
      width: size,
      height: size,
      fit: BoxFit.contain,
      isAntiAlias: true,
    );
  }
}
```

### منطق التبديل بين الحركات:
```dart
String getMascotAnimation(QuizState state) {
  switch (state) {
    case QuizState.idle:       return MascotAnimations.idle;
    case QuizState.thinking:   return MascotAnimations.thinking;
    case QuizState.correct:    return MascotAnimations.correctAnswer;
    case QuizState.incorrect:  return MascotAnimations.incorrectAnswer;
    case QuizState.combo:      return MascotAnimations.combo;
    case QuizState.bossWin:    return MascotAnimations.bossExcellent;
    case QuizState.bossFail:   return MascotAnimations.bossFail;
    default:                   return MascotAnimations.idle;
  }
}
```

---

## 🗺️ أصول خريطة المسار (Map Decorations - Static PNG)

> **استراتيجية التحميل:** يتم تصدير هذه الأصول كصور ثابتة مفرغة الشفافية (Transparent PNG). ترفع على السيرفر ويقوم التطبيق بتحميلها مسبقاً (Preloading) لضمان خريطة فائقة السلاسة.

#### 1. البداية والتجهيز (Start / Packing)
url: `https://your-cdn-assets.com/mascot/Start.png`

#### 2. الاستكشاف (Exploration)
url: `https://your-cdn-assets.com/mascot/Exploration.png`

#### 3. استراحة الطريق (Camp / Rest)
url: `https://your-cdn-assets.com/mascot/Camp.png`

#### 4. الإرشاد والتوجيه (Signpost)
url: `https://your-cdn-assets.com/mascot/Signpost.png`

#### 5. التفكير والتأمل (Pondering / Confusion)
url: `https://your-cdn-assets.com/mascot/Confusion.png`

#### 6. القوة والثقل (Tafkheem / Heavy)
url: `https://your-cdn-assets.com/mascot/Tafkheem.png`

#### 7. الرقة والخفة (Tarqeeq / Light)
url: `https://your-cdn-assets.com/mascot/Light.png`

#### 8. اكتشاف كنز (Discovery)
url: `https://your-cdn-assets.com/mascot/Discovery.png`

#### 9. جسر العبور (Connection)
url: `https://your-cdn-assets.com/mascot/Connection.png`

#### 10. القمة والختام (The Peak / Mastery)
url: `https://your-cdn-assets.com/mascot/Mastery.png`

---

*آخر تحديث: سبتمبر 2026 — Open Islamic App Design Team*
