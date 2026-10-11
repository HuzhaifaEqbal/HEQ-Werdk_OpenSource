# 📖 مواصفات محرك قارئ القرآن الكريم المتقدم (QCF V2)
## (Advanced Quran Reader Architecture, QCF V2 Font Glyphs & Word-Timing Sync Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **معمارية عرض المصحف المطابق للطباعة (Pixel-Perfect 604 Pages):** استخدام خطوط QCF V2 الرسمية من Quran Foundation برسم الآيات كلمة بكلمة وسطر بسطر.
> * **محرك التظليل المتزامن للكلمات (Word-Level Karaoke Audio Sync):** ربط أوقات تلاوة القراء بمواقع الكلمات على صفحة المصحف وتظليلها لحظياً.
> * **إدارة تعدد الروايات:** دعم رواية حفص عن عاصم مع المحافظة على هيكل رواية ورش واستقلالية النماذج.
> * **الفئة المستهدفة:** مهندسو Flutter المتخصصون، ومطورو محركات عرض المصحف الشريف والأنظمة الصوتية المتزامنة.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس برمجيات وتطبيقات خبير في Flutter والمعماريات الصوتية المتقدمة:
> مهمتك هي بناء محرك متكامل لقارئ القرآن الكريم (رواية حفص عن عاصم) بدقة مطابقة لصفحات المصحف الشريف (604 صفحات) باستخدام خطوط QCF V2 الرسمية وتزامن تظليل الكلمات لحظياً أثناء الاستماع (Word-level Audio Karaoke Highlight).
> 
> إرشادات التطبيق وبيئة العمل:
> 1. مسار المشروع: هيكل الكود داخل `your_project/lib/features/quran_reader/` و `your_project/lib/core/audio/`.
> 2. مصادر البيانات والروابط: استعمل خوادم وواجهات برمجية بصيغة `your_api` و `https://your-api-domain.com/quran` وروابط الخطوط بصيغة `your_urls/fonts/p{PAGE}.woff2`.
> 3. بنية التخزين والكاش: صمم الكاش للتخزين المحلي داخل `your_project/storage/` مع دعم التشغيل دون إنترنت (Offline Mode).
> 4. التزم بجميع المواصفات المعمارية وخطوات التنفيذ الـ 9 المشروحة تفصيلياً في المستند أدناه دون أي تغيير في قواعد المصحف الرسمية.
> ```

---

## 🎯 الهدف النهائي (System Goal)

أريد بناء نظام قارئ قرآن حديث ودقيق جدًا لرواية **حفص عن عاصم** باستخدام **QCF V2** من Quran Foundation، مع:

1. عرض صفحات المصحف بشكل قريب جدًا من المصحف الحقيقي.
2. استخدام بيانات الكلمات الرسمية بدل كتابة النص يدويًا.
3. استخدام QCF V2 glyphs وpage-specific fonts.
4. دعم 604 صفحات.
5. معرفة الصفحة والسطر وترتيب كل كلمة.
6. ربط كل كلمة بالـverse_key والـword index.
7. جلب صوتيات القرّاء من Quran Foundation.
8. دعم عدة قرّاء.
9. الحصول على word timings عندما تكون متوفرة.
10. أثناء تشغيل الصوت، تحديد الكلمة الحالية وتظليلها على نفس مكانها في الصفحة.
11. الحفاظ على نظام ورش الموجود حاليًا وعدم تغييره.
12. بناء النظام بطريقة تسمح لاحقًا بإضافة ورش الحديثة دون إعادة بناء قارئ القرآن بالكامل.

---

# أول قاعدة مهمة جدًا

**لا تفترض أي بيانات. لا تخترع إحداثيات. لا تخترع word timings. لا تنشئ 604 ملفات JSON يدويًا. لا تعيد كتابة القرآن يدويًا.**

قبل كتابة الكود، افحص المشروع الحالي وافهم:

- أين يوجد قارئ القرآن الحالي؟
- كيف يتم اختيار الرواية؟
- كيف يتم تحميل نص حفص وورش حاليًا؟
- أين توجد ملفات الصوت؟
- كيف يتم تشغيل الصوت؟
- هل يوجد model أو repository للقرآن أصلًا؟
- ما هي بنية Flutter الحالية؟
- ما هي packages المستخدمة للصوت والكاش والتخزين؟

**لا تحذف أو تكسر أي شيء خاص بورش.**

النظام الجديد يخص **حفص فقط في هذه المرحلة**.

---

# 1. مصدر بيانات القرآن

استخدم Quran Foundation Content API كمصدر رسمي لبيانات حفص.

نريد QCF V2:

- Mushaf ID = 1
- `code_v2`
- `page_number`
- `line_number`
- `position`
- `verse_key`
- `text_qpc_hafs` كـfallback/validation عند الحاجة.

توثيق QCF الرسمي يوضح أن QCF V2 هو خيار Pixel-perfect Mushaf، وأن `code_v2 + page_number` هما الأساس للرسم. كما أن بيانات الكلمات تتضمن `page_number` و`line_number` و`position`.

لا تستخدم Unicode Arabic text وحده لرسم الصفحة النهائية إذا كان الهدف هو الشكل الدقيق للمصحف.

المصدر الرسمي:
https://api-docs.quran.com/docs/tutorials/fonts/font-rendering/

Page Layout:
https://api-docs.quran.com/docs/tutorials/fonts/page-layout/

---

# 2. جلب بيانات الكلمات

استخدم Content API مع:

```text
words=true
word_fields=code_v2,text_qpc_hafs,page_number,line_number,position
mushaf=1
```

ويجب أن يكون الناتج قادرًا على إعطائنا لكل كلمة على الأقل:

```text
id
verse_key
position
page_number
line_number
code_v2
text_qpc_hafs
char_type_name
```

لا تفترض أن كل line هو verse.

**مهم جدًا:**

السطر الواحد في المصحف قد يحتوي كلمات من أكثر من آية.

لذلك لا ترسم كل آية كفقرة مستقلة.

بدل ذلك:

```text
API verses
    ↓
extract all words
    ↓
group by page_number
    ↓
group by line_number
    ↓
render physical Mushaf lines
```

هذا ضروري للحصول على layout صحيح.

---

# 3. لا نريد 604 JSON يدويًا

لا تنشئ:

```text
page1.json
page2.json
page3.json
...
page604.json
```

يدويًا.

إذا كان من الضروري تخزين البيانات محليًا، أنشئ **نظام بيانات واحد قابل للفهرسة**، مثل:

```text
quran_words
quran_pages
quran_lines
```

أو JSON/database واحد منظم.

المفتاح الأساسي يجب أن يسمح بالوصول السريع إلى:

```text
page_number
line_number
verse_key
word_index
```

ويجب أن يكون بالإمكان الحصول على جميع كلمات صفحة معينة بسرعة.

---

# 4. QCF V2 fonts

QCF V2 يعتمد على font خاص بكل صفحة.

النمط الرسمي:

```text
https://verses.quran.foundation/fonts/quran/hafs/v2/woff2/p{PAGE}.woff2
```

حيث:

```text
PAGE = 1 ... 604
```

مثال:

```text
p1.woff2
p2.woff2
...
p604.woff2
```

لا تفترض أن هذه fonts يجب تحميلها كلها عند تشغيل التطبيق.

نفّذ caching ذكيًا:

### الوضع الطبيعي

عندما يفتح المستخدم صفحة:

```text
load page data
load required page font
cache them
render
```

### الوضع offline

أضف بنية تسمح لاحقًا بخيار:

```text
تنزيل المصحف للاستخدام دون إنترنت
```

وعند تفعيل التنزيل:

```text
download Quran data
download required 604 QCF V2 fonts
store locally
mark Quran package as available offline
```

لكن لا تنفذ تنزيل 604 fonts دفعة واحدة بدون التحقق أولًا من حجم البيانات الإجمالي وتجربة الأداء.

---

# 5. Rendering

الهدف هو:

```text
QuranPage(pageNumber)
```

وتكون الصفحة مبنية من:

```text
page
 ├── line 1
 │    ├── word 1
 │    ├── word 2
 │    └── ...
 ├── line 2
 ├── line 3
 └── ...
```

كل كلمة يجب أن تعرف:

```text
verseKey
wordIndex
pageNumber
lineNumber
position
codeV2
```

استخدم QCF font الخاص بالصفحة نفسها.

لا تستخدم font مختلف لكل كلمة.

---

# 6. إحداثيات الكلمات

هذه نقطة حساسة جدًا.

**لا تفترض أن Quran Foundation API يعطي x/y/width/height جاهزة لكل كلمة إذا لم تكن موجودة فعلًا في الاستجابة.**

الـAPI يعطي layout metadata مثل:

```text
page_number
line_number
position
```

وQCF V2 يعطي glyph rendering.

إذا كنا نحتاج bounding boxes حقيقية للكلمات من أجل الـhighlight:

يجب حسابها من layout/rendering الفعلي في Flutter أو استخدام مصدر موثوق يوفر هذه الإحداثيات.

لا تخترع:

```text
x = 100
y = 200
width = ...
```

ولا تعمل إحداثيات ثابتة مرتبطة بدقة شاشة واحدة.

---

# 7. أهم شيء: نظام هوية الكلمة

نحتاج إلى مفتاح ثابت يربط:

```text
Quran word
Audio timing
Highlight
User interaction
```

استخدم:

```text
verse_key + word_index
```

مثال:

```text
24:35 + word 3
```

يمثل الكلمة الثالثة في الآية 35 من سورة النور.

إذا كانت بيانات Quran Foundation تستخدم `position` بدل `word_index` في مكان معين، أنشئ mapping واضح ولا تفترض أن الرقم نفسه دائمًا يمثل الشيء نفسه.

---

# 8. الصوتيات

استخدم Quran Foundation كمصدر الصوتيات الجديد.

لدينا **Ayah-by-Ayah Recitations**.

قائمة القراء الرسمية:

```text
GET /resources/recitations
```

وتعيد:

```text
id
reciter_name
style
translated_name
```

توثيق:
https://api-docs.quran.com/docs/content_apis_versioned/4.0.0/recitations/

**مهم جدًا:**

هناك نوعان من IDs في Quran Foundation:

1. `recitation_id`
   - خاص بـ ayah-by-ayah recitations.

2. `chapter_reciter_id`
   - خاص بـ chapter recitations.

لا تخلط بينهما.

التوثيق الرسمي يحذر من أن هذه IDs غير قابلة للاستبدال.

---

# 9. جلب صوت آية

الصوت الأساسي يمكن أن يكون:

```text
verse_key = 24:35
```

والـAPI يعيد:

```json
{
  "verse_key": "24:35",
  "url": "..."
}
```

استخدم endpoint الخاص بـ ayah-by-ayah recitation.

توثيق:
https://api-docs.quran.com/docs/content_apis_versioned/4.0.0/recitation-audio-files/

---

# 10. Word Timings

هذه أهم نقطة في المشروع.

نريد أثناء تشغيل الصوت معرفة:

```text
أي كلمة تُقرأ الآن؟
```

Quran Foundation يوفر chapter recitation مع:

```text
segments=true
```

وعند توفر timing data، الـsegment يكون:

```text
[word_index, start_ms, end_ms]
```

مثال:

```json
[
  [1, 0, 630],
  [2, 650, 1570],
  [3, 1570, 3110]
]
```

أي:

```text
word 1 → 0ms - 630ms
word 2 → 650ms - 1570ms
word 3 → 1570ms - 3110ms
```

التوثيق الرسمي:
https://api-docs.quran.com/docs/content_apis_versioned/4.0.0/chapter-reciter-audio-file/

---

# 11. لا تفترض أن كل قارئ لديه timings

هذه قاعدة إلزامية.

إذا أعاد الـAPI:

```text
segments
```

استخدمها.

إذا لم يعطِ timings لقارئ معين:

```text
لا تخترع timings
```

ولا تحاول تخمينها من طول الصوت.

بدل ذلك:

```text
audio works
word highlighting disabled for that recitation
```

أو استخدم fallback واضح إذا وجد مصدر timing موثوق.

---

# 12. مهم: الصوت والتوقيت ليسا إحداثيات

لا تربط:

```text
audio timing → x/y
```

مباشرة.

الربط الصحيح:

```text
Audio
  ↓
verse_key
  ↓
word_index
  ↓
Quran word
  ↓
current rendered widget
  ↓
actual screen position
  ↓
highlight
```

وبالتالي لو تغير:

- حجم الشاشة
- zoom
- orientation
- font scale
- device

يبقى الصوت صحيحًا، وموقع الـhighlight يعاد حسابه من layout الحالي.

---

# 13. نموذج البيانات المقترح

أنشئ models واضحة.

مثال:

```dart
class QuranWord {
  final int id;
  final String verseKey;
  final int wordIndex;
  final int pageNumber;
  final int lineNumber;
  final int position;
  final String codeV2;
  final String fallbackText;
}
```

ثم:

```dart
class WordTiming {
  final String verseKey;
  final int wordIndex;
  final int startMs;
  final int endMs;
}
```

ثم:

```dart
class Reciter {
  final int id;
  final String name;
  final String? style;
}
```

ثم:

```dart
class VerseAudio {
  final String verseKey;
  final String url;
  final int recitationId;
}
```

لا تجعل `QuranWord` يعرف شيئًا عن audio URL.

ولا تجعل `WordTiming` يعرف x/y.

ولا تجعل `VerseAudio` يعرف UI.

افصل الـdata عن الـpresentation.

---

# 14. Architecture

أريد architecture نظيفة تقريبًا بهذا الشكل:

```text
QuranReader
│
├── data
│   ├── quran_api
│   ├── audio_api
│   ├── local_cache
│   └── repositories
│
├── domain
│   ├── QuranWord
│   ├── QuranPage
│   ├── QuranLine
│   ├── WordTiming
│   ├── Reciter
│   └── VerseAudio
│
└── presentation
    ├── QuranPageView
    ├── QuranLineView
    ├── QuranWordView
    ├── AudioPlayer
    └── WordHighlightController
```

أو استخدم architecture الموجودة أصلًا في المشروع إذا كانت جيدة.

**لا تعيد هيكلة المشروع كله بدون سبب.**

ادمج النظام الجديد مع architecture الحالية.

---

# 15. Audio synchronization

أثناء تشغيل الصوت:

```text
audio.position
```

يتم تحديثه بشكل مستمر.

ثم:

```text
currentTimeMs
```

نبحث عن:

```text
timing.startMs <= currentTimeMs < timing.endMs
```

فنحصل على:

```text
currentWordIndex
```

ثم:

```text
currentWordIndex
        ↓
QuranWord
        ↓
find rendered word
        ↓
highlight
```

عند انتهاء timing:

```text
remove highlight
```

وعند الانتقال إلى الآية التالية:

```text
load next verse audio
load next timings
highlight first word
```

إذا كان النظام يستخدم chapter audio بدل ملفات الآيات، انتبه أن timestamps قد تكون offsets بالنسبة إلى بداية ملف السورة، وليس بداية الآية. يجب التعامل معها كما يحدد الـAPI.

---

# 16. Highlight

الـhighlight يجب أن يكون overlay فوق الكلمة، وليس تعديلًا دائمًا على QCF glyph.

مثلًا:

```text
QCF word
     ↓
Render
     ↓
Measure actual bounds
     ↓
Overlay highlight
```

الـhighlight يجب أن يتبع الكلمة حتى لو تغير layout.

لا تستخدم:

```text
Positioned(left: 100, top: 200)
```

كحل ثابت.

استخدم القياسات الفعلية للـrendered widget.

---

# 17. User interaction

عند الضغط على كلمة:

```text
tap word
```

يجب معرفة:

```text
verseKey
wordIndex
```

وبناءً عليه يمكن لاحقًا:

- تشغيل الآية
- تكرار الكلمة
- إظهار معنى الكلمة
- نسخ الآية
- إظهار التفسير
- إضافة bookmark

لكن في هذه المرحلة ركز على:

```text
tap → identify word
```

ولا تضف ميزات غير مطلوبة.

---

# 18. Multiple Reciters

الـUI يجب أن يسمح للمستخدم باختيار قارئ.

مثال:

```text
القارئ:
[ عبد الباسط عبد الصمد ▼ ]
```

عند تغيير القارئ:

```text
selectedReciterId changes
        ↓
audio source changes
        ↓
timings change
        ↓
Quran page DOES NOT change
```

لأن:

```text
Quran layout = independent
Audio = independent
Timing = independent
```

---

# 19. Caching

لا تجلب نفس البيانات كل مرة.

نفذ cache على الأقل لـ:

```text
Quran page data
QCF page font
reciter list
audio URL metadata
word timings
```

لكن لا تخزن ملفات الصوت كاملة محليًا إلا إذا كان هناك سبب واضح أو ميزة offline مطلوبة.

يمكن لاحقًا إضافة:

```text
Download Recitation
```

لكن لا تجعل ذلك جزءًا إجباريًا من النسخة الأولى.

---

# 20. Offline Quran

أريد أن تكون architecture قابلة لدعم:

```text
Download Quran
```

بحيث:

```text
Quran text/data
+
604 QCF V2 fonts
```

يمكن تخزينها محليًا.

أما الصوتيات، فاجعلها نظامًا منفصلًا:

```text
Download recitation
```

ولا تربط تنزيل القرآن بتنزيل الصوتيات.

---

# 21. Authentication

Quran Foundation APIs تحتاج:

```text
x-auth-token
x-client-id
```

**لا تضع client secret أو أي secret داخل Flutter app.**

استخدم backend موجود في المشروع أو أنشئ service backend صغيرة إذا كانت architecture الحالية تسمح.

Flutter:

```text
Flutter
   ↓
Your backend
   ↓
Quran Foundation
```

ولا:

```text
Flutter
   ↓
secret
   ↓
Quran Foundation
```

الـAPI documentation نفسها تنص على إبقاء credentials الحساسة على server.

---

# 22. Security

لا تضع:

```text
CLIENT_SECRET
ACCESS_SECRET
PRIVATE_KEY
```

داخل:

```text
.dart
.env المضمّن داخل التطبيق
APK
```

أي secret يجب أن يبقى server-side.

إذا كانت البيئة الحالية تحتوي بالفعل على backend، استخدمه بدل إنشاء backend جديد بدون داعٍ.

---

# 23. ورش

**ممنوع تعديل نظام ورش الحالي.**

حاليًا:

```text
Hafs → NEW QCF V2 system
Warsh → EXISTING SYSTEM
```

لاحقًا فقط عندما نوفر:

```text
Warsh modern Quran data
Warsh layout
Warsh coordinates
Warsh fonts
```

نضيف:

```text
WarshDataProvider
```

بدون إعادة كتابة قارئ القرآن.

لذلك من البداية افصل:

```dart
QuranEdition / QuranRiwayah
```

عن:

```dart
QuranDataProvider
```

حتى يكون ممكنًا:

```text
Hafs → QCFV2Provider
Warsh → ExistingWarshProvider
```

---

# 24. لا تستخدم مشروع GitHub كـsource نهائي بدون تحقق

إذا وجدت project مثل:

```text
quran-page-viewer
```

يمكن استخدامه لفهم data structures أو للاستفادة من generated data إذا كانت مطابقة للمصدر الرسمي.

لكن **المصدر المرجعي النهائي يجب أن يكون Quran Foundation الرسمي**.

لا تنسخ data عمياء من repository غير رسمي.

تحقق من:

```text
verse count
page count
word ordering
page numbers
line numbers
code_v2
```

قبل اعتماد أي generated dataset.

---

# 25. Validation

بعد التنفيذ لا تقل:

```text
Done
```

إلا بعد اختبار فعلي.

اختبر على الأقل:

### Page 1

```text
Surah Al-Fatihah
```

### صفحة وسطية

مثلاً:

```text
Page 300
```

### صفحة قرب نهاية المصحف

```text
Page 604
```

تحقق من:

```text
correct page
correct lines
correct words
correct Arabic rendering
correct verse boundaries
correct QCF font
```

ثم اختبر الصوت:

```text
24:35
```

مثلًا:

```text
play
→ word 1 highlight
→ word 2 highlight
→ word 3 highlight
...
```

ثم غيّر القارئ:

```text
Reciter A
→ Reciter B
```

وتأكد أن:

```text
page unchanged
words unchanged
layout unchanged
timings/audio changed correctly
```

---

# 26. اختبارات مهمة جدًا

لا تعتبر النظام ناجحًا إذا نجحت صفحة واحدة فقط.

اختبر:

```text
verse starts in middle of line
verse ends in middle of line
multiple verses on same line
page boundary between verses
surah boundary
basmala
verse end markers
```

خصوصًا لأن السطر الواحد قد يحتوي كلمات من عدة آيات.

---

# 27. Error handling

إذا فشل:

### Quran API

اعرض fallback/cache.

### Font

استخدم fallback text مؤقتًا ولا تظهر صفحة فارغة.

### Audio

أظهر خطأ قابل للفهم.

### Timing

شغل الصوت بدون word highlight بدل إيقاف التلاوة.

### Network

إذا كانت الصفحة مخزنة محليًا:

```text
use cache
```

---

# 28. الأداء

لا تحمل كل صفحات المصحف في الذاكرة.

استخدم lazy loading:

```text
current page
previous page
next page
```

ويمكن prefetch للصفحة التالية.

الهدف:

```text
smooth page scrolling
smooth audio
no frame drops
no unnecessary API calls
```

ولا تعيد بناء كامل الصفحة عند تغير currentWordIndex.

يجب أن يتغير فقط الـhighlight المطلوب.

---

# 29. المطلوب منك قبل التنفيذ

قبل أن تعدل الملفات:

1. افحص المشروع.
2. حدد الملفات المسؤولة عن Quran Reader.
3. حدد نظام ورش الحالي.
4. حدد نظام الصوت الحالي.
5. حدد state management المستخدم.
6. حدد packages الحالية.
7. حدد أين يمكن وضع Quran Foundation integration.
8. اقترح أقل عدد ممكن من الملفات التي تحتاج تعديل.
9. لا تبدأ بإعادة بناء التطبيق كله.

بعد ذلك اعرض لي:

```text
CURRENT ARCHITECTURE
```

ثم:

```text
FILES TO CREATE
FILES TO MODIFY
FILES NOT TO TOUCH
```

ثم نفذ التغيير تدريجيًا.

---

# 30. قاعدة التنفيذ النهائية

**لا تختصر.**

إذا كان هناك شيء غير واضح في API:

ابحث في documentation الرسمية أولًا.

إذا كانت البيانات غير موجودة:

لا تخترعها.

إذا كانت coordinates غير متوفرة:

لا تدّعي أنها موجودة.

إذا كانت word timings غير متوفرة لقارئ:

لا تخمنها.

إذا كان هناك اختلاف بين API versions:

استخدم أحدث documentation الرسمية وتحقق من response schema.

إذا وجدت implementation رسمي من Quran Foundation:

فضّله على implementation عشوائي من GitHub.

---

# النتيجة التي أريد الوصول إليها

أريد في النهاية قارئ قرآن حفص بالشكل التالي:

```text
┌─────────────────────────────┐
│          سورة النور          │
│                             │
│      [صفحة المصحف الحقيقية] │
│                             │
│  الكلمات مرسومة بـ QCF V2  │
│                             │
│       كلمة ← Highlight      │
│                             │
│                             │
├─────────────────────────────┤
│ ▶ 00:12                     │
│                             │
│ القارئ: عبد الباسط ▼       │
│                             │
│  🔊 الصوت يعمل              │
└─────────────────────────────┘
```

وأثناء التلاوة:

```text
Audio position
      ↓
Word timing
      ↓
verse_key + word_index
      ↓
QuranWord
      ↓
Rendered word
      ↓
Actual bounds
      ↓
Highlight
```

هذا هو الـpipeline الأساسي للمشروع.

**لا تغير نظام ورش الحالي.**
**لا تعيد كتابة القرآن.**
**لا تنشئ 604 JSON يدويًا.**
**لا تخترع coordinates.**
**لا تخترع timings.**
**لا تضع secrets في Flutter.**
**استخدم المصادر الرسمية قدر الإمكان.**
**ونفذ حفص أولًا بشكل كامل وقابل للتوسع.**

## IMPORTANT — Migration Strategy

لا تحذف أو تستبدل نظام حفص القديم في البداية.

أريد تنفيذ النظام الجديد بشكل **Parallel / Safe Migration**.

### المرحلة 1 — لا نلمس أي شيء

حاليًا يجب أن يبقى:

```text
Hafs → النظام القديم
Warsh → النظام القديم
```

اعمل النظام الجديد لحفص بشكل منفصل:

```text
Hafs Legacy
Hafs QCF V2
Warsh Legacy
```

ولا تجعل QCF V2 هو النظام الافتراضي بعد.

---

# المرحلة 2 — Proof of Concept على سورة الفاتحة

قبل نقل كامل القرآن، طبّق النظام الجديد على **سورة الفاتحة فقط**.

المطلوب أن تعمل الفاتحة بالكامل باستخدام:

```text
QCF V2
+
Quran Foundation Quran data
+
QCF page font
+
word mapping
+
audio
+
word timings
+
word highlighting
```

اختبر جميع آيات الفاتحة، وليس آية واحدة فقط.

يجب أن أتأكد أن:

1. النص صحيح.
2. شكل المصحف صحيح.
3. الكلمات في أماكنها الصحيحة.
4. تقسيم الأسطر صحيح.
5. `verse_key` صحيح.
6. `word_index` صحيح.
7. الضغط على الكلمة يعيد الكلمة الصحيحة.
8. الصوت الصحيح يعمل.
9. الـword timings مرتبطة بالكلمات الصحيحة.
10. الهايلايت ينتقل من كلمة إلى كلمة أثناء التلاوة.
11. تغيير القارئ يغير الصوت والتوقيتات فقط ولا يكسر الصفحة.
12. لا يوجد تأثير على ورش.
13. النظام القديم لحفص ما زال موجودًا كـfallback.

---

# المرحلة 3 — صفحة الاختبار

لا تفترض أن سورة الفاتحة = صفحة واحدة فقط بطريقة rendering بسيطة.

استخدم بيانات QCF الرسمية لتحديد:

```text
page_number
line_number
position
```

والـfont الخاص بالصفحة.

إذا كانت الفاتحة موجودة ضمن الصفحة الأولى، اختبر الصفحة الأولى كصفحة مصحف كاملة، وليس فقط آيات الفاتحة.

يجب أن يظهر محتوى الصفحة بالطريقة التي يحددها QCF V2.

---

# المرحلة 4 — اختبار الصوت

اختبر آيات الفاتحة مع قارئ واحد أولًا.

مثال:

```text
1:1
1:2
1:3
...
1:7
```

لكل آية:

```text
verse_key
    ↓
audio
    ↓
timings
    ↓
word_index
    ↓
QuranWord
    ↓
rendered word
    ↓
highlight
```

ثم اختبر قارئًا ثانيًا.

المطلوب:

```text
نفس الصفحة
نفس الكلمات
نفس الإحداثيات/layout
صوت مختلف
timings مختلفة حسب القارئ إذا كانت متوفرة
```

---

# المرحلة 5 — لا تعتبر النظام ناجحًا بمجرد ظهور النص

ظهور النص وحده لا يعني أن الـPOC نجح.

يجب أن ينجح:

```text
Visual rendering
+
Word identity
+
Word interaction
+
Audio
+
Timing synchronization
+
Highlight positioning
```

كلها معًا.

---

# المرحلة 6 — تقرير اختبار إلزامي

بعد تنفيذ الفاتحة، لا تبدأ مباشرة بنقل بقية القرآن.

اعمل تقريرًا داخليًا واضحًا يبين:

```text
QCF API ............... PASS / FAIL
QCF V2 font ........... PASS / FAIL
Page rendering ........ PASS / FAIL
Line grouping ......... PASS / FAIL
Word mapping .......... PASS / FAIL
Verse mapping ......... PASS / FAIL
Word interaction ...... PASS / FAIL
Audio ................ PASS / FAIL
Word timings .......... PASS / FAIL
Highlight ............. PASS / FAIL
Multiple reciters .... PASS / FAIL
Warsh unchanged ...... PASS / FAIL
Legacy Hafs fallback . PASS / FAIL
```

إذا كان أي جزء أساسي FAIL، لا تبدأ migration الكامل.

---

# المرحلة 7 — Migration Flag

إذا نجحت الفاتحة بالكامل، أضف feature flag واضح مثل:

```dart
useNewHafsReader
```

بحيث يمكن التحكم:

```text
false → Hafs Legacy
true  → Hafs QCF V2
```

ولا تغير النظام القديم.

بهذا أستطيع اختبار النظام الجديد بسهولة.

---

# المرحلة 8 — الترحيل التدريجي

بعد نجاح الفاتحة، لا تحذف النظام القديم فورًا.

ابدأ بالتوسع:

```text
Phase A:
Al-Fatihah

Phase B:
A few additional pages

Phase C:
A few complete surahs

Phase D:
Full 604-page Mushaf

Phase E:
Production migration
```

في كل مرحلة حافظ على fallback للنظام القديم.

---

# المرحلة 9 — حذف حفص القديم

**ممنوع حذف Hafs Legacy إلا بعد اكتمال النظام الجديد بالكامل.**

بعد أن نتأكد من:

```text
all 604 pages
all Quran words
all verse mappings
audio
reciters
timings where available
highlight
offline/cache
performance
```

وتم اختبار النظام على أجهزة فعلية، عندها فقط يمكن إزالة النظام القديم.

لكن حتى ذلك الوقت:

```text
Hafs Legacy → موجود
Hafs QCF V2 → موجود
Warsh Legacy → موجود
```

---

# النتيجة المطلوبة

أريد أن أقدر أشغل التطبيق الآن وأجد:

```text
Warsh
→ يعمل كما كان تمامًا.

Hafs
→ يعمل كما كان تمامًا.

New Hafs QCF V2
→ موجود بشكل منفصل للاختبار.
```

وبعد نجاح سورة الفاتحة، نقرر تفعيل QCF V2 لحفص.

**لا تقم بأي destructive migration.**

لا تحذف ملفات حفص القديمة.

لا تستبدل الـmodels القديمة.

لا تغير Warsh.

لا تغير audio system الموجود إلا إذا كان ضروريًا لتكامل النظام الجديد.

ابنِ الجديد أولًا، اختبره، ثم ننقل المستخدمين إليه.

# ملاحظة مهمة بخصوص الاختبارا ت المذكورة بالاعلى كلها انا بعملها لما تخلص شغل انت  ع سورة الفاتحة 