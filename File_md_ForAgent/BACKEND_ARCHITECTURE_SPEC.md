# 📋 سجل وثائق ومواصفات الباك إند وقاعدة البيانات
## (Backend & Database Architecture Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **توثيق البنية التحتية الخلفية:** مرجع شامل لمهندسي الباك إند ونماذج الذكاء الاصطناعي لتصميم خدمات وخوادم التطبيق.
> * **مخططات قواعد البيانات (Database Schemas):** جداول ومجموعات الواحات (`oases`)، العقد التعليمية (`learning_nodes`)، تقدم المستخدم، وخوارزميات التكرار المتباعد (FSRS).
> * **معمارية نقاط الاتصال (API Architecture):** مواصفات المسارات البرمجية لجلب المناهج، حفظ التقدم، ونظام نقاط الخبرة والمكافآت.
> * **الفئة المستهدفة:** مهندسو الواجهة الخلفية (Backend Engineers)، مهندسو قواعد البيانات، ومطورو الـ Full-Stack.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس أنظمة خلفية وقواعد بيانات رئيسي (Lead Backend & Database Architect):
> مهمتك هي بناء وتصميم البنية التحتية الخلفية، ونماذج قواعد البيانات (MongoDB / PostgreSQL Collections)، ومسارات REST APIs لمنظومة التعلم التفاعلي والواحات، وتتبع التكرار المتباعد (FSRS)، وإحصائيات تلاوة المصحف.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. مسار المشروع: هيكل نماذج البيانات والخدمات في `your_project/backend/src/models/` و `your_project/backend/src/controllers/`.
> 2. استدعاءات الخادم والـ API: وجه نقاط النهاية إلى `https://your-api-domain.com/api/v1/` مع دعم التخزين بدون إنترنت.
> 3. التزم بمخططات JSON المحددة للواحات والعقد ونظام المكافآت والشعلة وقواعد التصميم الموضحة في هذه المواصفة.
> ```

---

## 🌴 القسم الأول: مسار التعلم التفاعلي ونظام الواحات (Learn Journey & Oases System)
- **مسار الواجهة الأمامية (Flutter)**: `your_project/lib/features/learn/`
- **المفهوم**: رحلة تفاعلية بأسلوب دوولينجو (Duolingo Gamified Path) مقسمة لواحات (Oases)، كل واحة تمثل محطة تعليمية (تجويد، قرآن، سنة، فقه). تحتوي كل واحة على مستويات ودروس وأسئلة تفاعلية (MASAQ AI Distractors) وحسابات التكرار المتباعد (FSRS Algorithm).

### 1. مخططات قاعدة البيانات المطلوبة (MongoDB / PostgreSQL Collections)

#### أ. جدول/مجموعة الواحات (`oases`)
```json
{
  "_id": "ObjectId",
  "orderIndex": 1,
  "slug": "tajweed-basics",
  "title": {
    "ar": "واحة مبادئ التجويد",
    "en": "Basics of Tajweed Oasis"
  },
  "description": {
    "ar": "تعلم أحكام النون الساكنة والتنوين والميم الساكنة",
    "en": "Learn rules of Nun Sakinah, Tanween, and Meem Sakinah"
  },
  "category": "tajweed", // tajweed | quran | sunnah | fiqh
  "totalNodes": 5,
  "requiredGems": 0,
  "oasisAsset": "oasis_desert_bloom", // Rive animation identifier
  "createdAt": "ISODate",
  "updatedAt": "ISODate"
}
```

#### ب. جدول/مجموعة عقد ومحطات التعلم (`learning_nodes`)
```json
{
  "_id": "ObjectId",
  "oasisId": "ObjectId",
  "nodeIndex": 1,
  "title": {
    "ar": "الإظهار الحلقي",
    "en": "Al-Izhar Al-Halqi"
  },
  "type": "lesson", // lesson | review | checkpoint | boss_challenge
  "xpReward": 25,
  "gemsReward": 5,
  "exercises": [
    {
      "exerciseId": "ex_01",
      "type": "multiple_choice", // multiple_choice | verse_reorder | audio_listen | fill_blank
      "question": {
        "ar": "ما هو حرف الإظهار في قوله تعالى: (مِنْ خَوْفٍ)؟",
        "en": "What is the Izhar letter in: (مِنْ خَوْفٍ)?"
      },
      "verseUthmani": "الَّذِي أَطْعَمَهُم مِّن جُوعٍ وَآمَنَهُم مِّنْ خَوْفٍ",
      "correctOption": "الخاء",
      "options": ["الخاء", "الميم", "الواو", "الفاء"], // MASAQ AI generated distractors
      "explanation": {
        "ar": "جاء حرف الخاء (أحد حروف الحلق الستة) بعد النون الساكنة، فيكون الحكم إظهاراً حلقياً.",
        "en": "The letter Kha follows Nun Sakinah, making it Izhar Halqi."
      },
      "audioUrl": "https://cdn.heqlink.com/audio/tajweed/ex_01.mp3"
    }
  ]
}
```

#### ج. جدول/مجموعة تقدم المستخدم والذاكرة المعرفية (`user_learning_progress` & `fsrs_memory`)
```json
{
  "_id": "ObjectId",
  "userId": "ObjectId",
  "currentNodeId": "ObjectId",
  "completedNodeIds": ["ObjectId"],
  "streakDays": 7,
  "totalXp": 450,
  "totalGems": 60,
  "lives": 5, // Hearts system
  "lastCompletedAt": "ISODate",
  "fsrsCards": [
    {
      "exerciseId": "ex_01",
      "stability": 2.4, // FSRS Stability
      "difficulty": 4.1, // FSRS Difficulty
      "reps": 3,
      "lapses": 0,
      "state": "review", // new | learning | review | relearning
      "due": "ISODate"
    }
  ]
}
```

### 2. واجهات برمجة التطبيقات المطلوبة (APIs & Endpoints)
- `GET /api/v1/learn/oases`: جلب خريطة الواحات الكاملة مع حالة تقدم المستخدم.
- `GET /api/v1/learn/nodes/:nodeId`: جلب تفاصيل وتمارين محطة معينة.
- `POST /api/v1/learn/nodes/:nodeId/submit`: إرسال إجابات المستخدم، احتساب النقاط (XP)، تحديث سلسلة الأيام (Streak)، وتحديث بارامترات FSRS.
- `POST /api/v1/learn/lives/recover`: استعادة القلوب المفقودة عبر مراجعة سريعة أو نقاط حسنات.

---

## 📖 القسم الثاني: واحة القرآن الكريم التفاعلية (The Holy Quran Mastery Oasis)
- **مسار الواجهة الأمامية**: `lib/features/learn/quran/`
- **المفهوم**: مسار متخصص لإتقان حفظ وتثبيت وتدبر القرآن الكريم وفق مستويات تدريجية (قصار السور -> جزء عم -> الأجزاء الطوال)، مع مراعاة الحرمة والقدسية التامة للنص القرآني الشريف.

> [!NOTE]
> **نقطة للمراجعة والتحقق الشرعي (قيد السؤال الفقهي):**
> آلية تمرين "ترتيب كلمات/آيات القرآن ككبسولات مبعثرة (Ayah Reorder)":
> هل يجوز شرعاً عرض كلمات الآية مبعثرة بقصد التعليم واختبار الحفظ حتى يرتبها المستخدم في سياقها الصحيح؟
> يتم تعليق اعتماد آلية التبعثر لحين استيفاء الفتوى والتوجيه الشرعي المعتمد، والاعتماد حالياً على إكمال الفراغ بالرسم العثماني والربط السمعي.

### 1. آليات وتمارين واحة القرآن (Quran Learning Mechanics)
1. **تمرين إكمال المقطع القرآني (Ayah Word Gap)**: عرض الآية كاملة بالرسم العثماني مع فراغ لكلمة واحدة لاختبار ضبط الحفظ والحركات.
2. **تمرين الربط السمعي (Audio Ear Training)**: استماع لمقطع تلاوة ينتهي عند رأس آية، وعلى المستخدم اختيار بداية الآية التالية.
3. **تمرين المتشابهات اللفظية (Mutashabihat Distractor Challenge)**: تدريب الذاكرة على الآيات المتشابهة في نهاياتها أو بداياتها.
4. **ميزة الترتيل الذكي والتحقق الصوتي (AI Recitation & Voice Evaluation - المرحلة المتقدمة الأخيرة)**: قيام المستخدم بالترتيل عبر الميكروفون والتعرف الآلي على الأخطاء التجويدية واللفظية فورياً.

### 2. مخططات قاعدة بيانات واحة القرآن (`quran_mastery_nodes`)
```json
{
  "_id": "ObjectId",
  "surahNumber": 113,
  "surahName": "سورة الفلق",
  "ayahRange": "1-5",
  "totalAyahs": 5,
  "level": "beginner", // beginner | intermediate | advanced
  "audioReciter": "al-husary",
  "exercises": [
    {
      "exerciseId": "q_ex_01",
      "type": "ayah_fill_gap",
      "verseUthmani": "قُلْ أَعُوذُ بِرَبِّ [.....]",
      "targetWord": "الْفَلَقِ",
      "options": ["الْفَلَقِ", "النَّاسِ", "الصَّمَدِ", "الْخَنَّاسِ"],
      "fullVerse": "قُلْ أَعُوذُ بِرَبِّ الْفَلَقِ",
      "audioTimestamp": { "startMs": 0, "endMs": 4200 }
    }
  ]
}
```

---

## 🕌 القسم الثالث: واحة فقه العبادات اليومية (Daily Fiqh Oasis)
- **مسار الواجهة الأمامية**: `lib/features/learn/` (Category: `fiqh`)
- **المفهوم**: مسار عملي لترسيخ فقه الطهارة، الوضوء، الصلاة، أحكام السهو والجنائز والزكاة بأسلوب المسائل الواقعية والتطبيقات التفاعلية.

### مخطط بيانات واحة الفقه (`fiqh_nodes`)
```json
{
  "_id": "ObjectId",
  "category": "fiqh",
  "topic": "صفة وضوء النبي ﷺ",
  "nodeIndex": 1,
  "level": "foundation",
  "exercises": [
    {
      "exerciseId": "f_ex_01",
      "type": "multipleChoice",
      "question": "ما هو الترتيب الصحيح لفرائض الوضوء المذكورة في سورة المائدة؟",
      "correctOption": "غسل الوجه، ثم اليدين للمرفقين، ثم مسح الرأس، ثم غسل الرجلين للكعبين",
      "options": [
        "غسل الوجه، ثم اليدين للمرفقين، ثم مسح الرأس، ثم غسل الرجلين للكعبين",
        "المضمضة، والاستنشاق، وغسل الوجه، وغسل القدمين",
        "مسح الرأس، وغسل الوجه، وغسل اليدين، وغسل الرجلين",
        "غسل اليدين، ثم القدمين، ثم الوجه، ثم مسح الرأس"
      ],
      "explanation": "لقوله تعالى: {يَا أَيُّهَا الَّذِينَ آمَنُوا إِذَا قُمْتُمْ إِلَى الصَّلَاةِ فَاغْسِلُوا وُجُوهَكُمْ وَأَيْدِيَكُمْ إِلَى الْمَرَافِقِ وَامْسَحُوا بِرُءُوسِكُمْ وَأَرْجُلَكُمْ إِلَى الْكَعْبَيْنِ}"
    }
  ]
}
```

---

## 🧭 القسم الرابع: منظومة خريطة الأذان واتجاه القبلة وبعد الكعبة (Prayer Location & Qibla Map)
- **مسار الواجهة الأمامية**: `lib/features/prayer_times/screens/prayer_location_map_screen.dart`
- **المفهوم**: شاشة مستقلة توفر:
  1. حساب زاوية القبلة الدقيقة من موقع المستخدم إلى الكعبة المشرفة (Great-Circle Bearing).
  2. حساب المسافة المباشرة بالكيلومتر إلى الكعبة المشرفة بمكة المكرمة (Haversine Formula: R=6371km).
  3. محاكاة بصرية لخط انحناء أذان الصلاة الحية على الخريطة (Live Adhan Terminator Curve).
  4. محرك بحث مباشر عن المدن والمعالم وتحديث الهيئة الفقهية تلقائياً.

### 1. واجهات برمجة التطبيقات للموقع والقبلة:
- `GET /api/v1/prayer/qibla?lat={lat}&lng={lng}`: استرجاع زاوية القبلة والمسافة للكعبة مع إحداثيات خط الأذان الحي.
- `GET /api/v1/prayer/geocode/search?q={query}`: بحث نصي عن المدن والمواقع الجغرافية.
- `GET /api/v1/prayer/timings?lat={lat}&lng={lng}&method={methodId}`: جلب مواقيت الصلاة الدقيقة للهيئة المحددة.

---

## 📖 القسم الخامس: منظومة الورد القرآني متعدد الروايات والتفاعل مع الآيات (Smart Wird Multi-Riwayah)
- **مسار الواجهة الأمامية**: `lib/features/quran_wird/smart_wird_screen.dart`
- **المفهوم**: تجربة قراءة وتدبر نقية خالية من الحشو البصري، توفر:
  1. **تعدد الروايات**: التبديل الفوري بين **رواية حفص عن عاصم** و **رواية ورش عن نافع (طريق الأزرق)** وحفظ تفضيل المستخدم محلياً وسحابياً.
  2. **التفاعل مع الآيات المفردة**: الضغط على رقم الآية لفتح نافذة سفلية مخصصة للنسخ السريع، حفظ العلامة المرجعية (Bookmark)، وتجهيز واجهة السماعيات لكل آية بصوت القارئ المختار.
  3. **التوثيق السحابي وغرس النخيل**: عند إتمام قراءة وتدبر الصفحة (بعد انقضاء مؤقت التدبر)، يتم تسجيل الصفحة وغرس نخلة باسم المستخدم أو المهداة له في الواحة.

### 1. واجهات برمجة التطبيقات للمصحف والروايات:
- `GET /api/v1/quran/page/:pageNumber?riwayah={hafs|warsh}`: جلب نص الآيات بالرسم العثماني المعتمد للرواية المختارة.
- `GET /api/v1/quran/ayah/:surah/:ayah/audio?reciter={reciterId}&riwayah={hafs|warsh}`: جلب الرابط الصوتي لمقطع الآية المفردة.
- `POST /api/v1/quran/bookmark`: حفظ أو مزامنة العلامات المرجعية للمستخدم عبر الأجهزة.
- `POST /api/v1/quran/offline-status`: تسجيل وتحديث حالة تحميل المصحف الشريف في جهاز المستخدم (لمعرفة من حمّل المصحف كاملاً ومن يتصفح أونلاين).
- `GET /api/v1/quran/analytics/mushaf-downloads`: إحصائيات لوحة التحكم لمتابعة نسب تحميل المصحف محلياً حسب الرواية والجهاز.

### 2. مخططات قاعدة البيانات لحالة تحميل المصحف (`users` collection fields):
```json
{
  "deviceUUID": "String",
  "mushafDownloaded": false,          // هل قام المستخدم بتحميل صفحات المصحف كاملة محلياً (أوفلاين)
  "mushafDownloadedAt": "ISODate",    // تاريخ اكتمال التحميل
  "mushafRiwayah": "hafs",            // الرواية المحملة: hafs | warsh
  "mushafStorageSizeMB": 92.5,        // حجم المساحة المحفوظة على جهاز المستخدم بالميجابايت
  "mushafDownloadChoice": "download_all" // download_all (تحميل كامل) | stream_and_cache (تصفح مع كاش تلقائي)
}
```

### 3. منظومة تحميل وعرض المصحف (SVG & JSON Engine)
بناءً على التحديث الجديد للعرض اللانهائي الدقة (Infinite Scaling)، يتم استضافة المصحف كملف ZIP مجمع:
- **نقطة النهاية (Endpoint)**: `GET /api/v1/quran/download/:riwayah.zip` (مثال: `hafs.zip`).
- **المحتوى (ZIP Content)**: 
  - مجلد `svg`: يحتوي على 604 صورة SVG بجودة فائقة لصفحات المصحف.
  - مجلد `json`: يحتوي على 604 ملف JSON للإحداثيات (Polygons) الخاصة بكل آية لرسم التظليل فوقها.
- **الترويسات الضرورية (Headers)**: يجب أن يرجع السيرفر ترويسة `Content-Length` صحيحة ليتمكن تطبيق Flutter (باستخدام مكتبة `dio`) من حساب نسبة التحميل وعرض شريط تقدم دقيق للمستخدم.

---

## 📐 معايير التصميم المعتمدة لهذه الميزة
- **Canvas**: أسود نقي `#000000` (الوضع الداكن) / أبيض نقي `#FFFFFF` (الوضع الفاتح).
- **التباين**: عالي معكوس (أبيض على أسود / أسود على أبيض).
- **الخطوط**: `GoogleFonts.notoSansArabic` للعناوين والأسئلة، `GoogleFonts.inter` للأرقام والـ XP، و `GoogleFonts.amiri` للآيات القرآنية الشريفة.
- **الحاويات**: لا حاويات ثقيلة أو رمادية، بل خلفية مباشرة مع حدود دقيقة `hairline` وزجاج مصنفر `GlassContainer` للأشرطة العائمة.
- **الهوية البصرية للأيقونات**: جميع الأيقونات تعتمد الحواف المنحنية الناعمة وتخلو من الزوايا الحادة والمستقيمة.

