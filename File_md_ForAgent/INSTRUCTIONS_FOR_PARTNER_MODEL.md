# 🕋 الدليل الهندسي لتوليد عقد واحة القرآن الكريم بالذكاء الاصطناعي
## (Quran Oasis Micro-Hifz Data Engineering & AI Directive Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **توجيه نماذج الذكاء الاصطناعي (AI Data Structuring Directive):** استخراج الآيات والموضوعات وتحويلها إلى عقد حفظ تفاعلية مصغرة (`Micro-learning Hifz Nodes`) بصيغة JSON.
> * **القواعد الشرعية والتعليمية الصارمة:** حظر بعثرة الآيات، وضبط حجم العقدة (من 3 إلى 5 آيات، واستثناءات الآيات الطويلة كآية الكرسي والدَّيْن).
> * **مخطط الـ JSON المعياري والتسميات:** توحيد معرفات العقد والأنشطة (`nodeId`, `activityId`) وتفاصيل تحديات الكلمة المفقودة وتخمين الآية التالية.
> * **الفئة المستهدفة:** مهندسو البيانات، مصممو المناهج القرآنية، ونماذج الذكاء الاصطناعي المولدة للمحتوى القرآني.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس بيانات ومناهج قرآنية رقمية (Quran Data Engineer & Curriculum Architect):
> مهمتك هي استخراج ونمذجة عقد الحفظ المصغر (Micro-Hifz Learning Nodes) لسور القرآن الكريم بدقة متناهية وبصيغة JSON معيارية، متضمنة تحديات ملء الفراغ، والآية التالية، وسياق المعلم الذكي.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. مسارات العمل: احفظ الملفات الناتجة داخل `your_project/backend/data/quran_oasis/juz_XX/node_{surahId}_{nodeIndex}.json`.
> 2. مرجع التوثيق: حدّث خريطة الهيكل في `your_project/backend/data/quran_oasis/STRUCTURE_MAP.md`.
> 3. القواعد الشرعية الصارمة: يُمنع منعاً باتاً بعثرة كلمات القرآن الكريم، والتزم بحجم العقد ومخطط الـ JSON الموضح في هذا الدليل.
> ```

---

## 📁 1. مسارات العمل الأساسية (File Paths)

1. **مصدر البيانات الخام:**
   ```
   your_project/data/raw/DATA.md
   ```
   *(نصوص الآيات وتفسيرها وموضوعاتها المقسمة للسور والأجزاء).*

2. **مجلد إخراج ملفات الـ JSON (Target Directory):**
   ```
   your_project/backend/data/quran_oasis/juz_01/
   ```
   *(تُحفظ فيه ملفات العقد بصيغة `node_001_01.json`, `node_002_01.json`... وهكذا).*

3. **ملف التوثيق والخريطة الهيكلية (Documentation File):**
   ```
   your_project/backend/data/quran_oasis/STRUCTURE_MAP.md
   ```
   *(عند الانتهاء من توليد أي عقد أو سورة، يتم توثيقها في هذا الملف في قسم مخصص لكل جزء).*

4. **المرجع الهندسي الشامل للتطبيق:**
   ```
   your_project/docs/QURAN_OASIS_BRIDGE.md
   ```

---

## ⚠️ 2. القواعد الصارمة والشرعية (Sacred Rules)

1. **ممنوع البعثرة مطلقاً (STRICTLY NO SCRAMBLING):**
   - يُمنع منعاً باتاً برمجة أو توليد أي نشاط يعتمد على بعثرة أو ترتيب كلمات الآية القرآنية أو الآيات.
   - الأنشطة المعتمدة في الواحة فقط هي: **الاستماع والتلاوة**، **ملء الكلمة المفقودة (`fill_in_the_blank`)**، و**تخمين الآية التالية (`next_ayah`)**.

2. **حجم العقدة التعليمية (Bite-sized Hifz Nodes):**
   - كل عقدة تحتوي عادة من **3 إلى 5 آيات**، وبحد أقصى **7 آيات** (في حال الآيات القصيرة).
   - **تنبيه خاص لسورة البقرة:** في الآيات الطويلة جداً (مثل **آية الكرسي 255**، أو **آية الدَّيْن 282**، أو أواخر البقرة 285-286)، يمكن أن تكون العقدة عبارة عن **آية واحدة أو آيتين فقط** منعاً للإثقال على الحافظ.

3. **التسلسل والترابط التام (No Gaps, No Overlaps):**
   - يجب أن يبدأ ترقيم الآيات في السورة من الآية `1`.
   - بداية كل عقدة `ayahStart` يجب أن تساوي تماماً نهاية العقدة السابقة `ayahEnd + 1`.
   - نهاية العقدة الأخيرة في السورة يجب أن تطابق إجمالي عدد آيات السورة (الفاتحة: 7 آيات، البقرة: 286 آية).

4. **تسمية الملفات والمُعرفات (Naming Conventions):**
   - صيغة اسم الملف: `node_{surahId:03d}_{nodeIndex:02d}.json`
     - مثال سورة الفاتحة: `node_001_01.json`, `node_001_02.json`
     - مثال سورة البقرة: `node_002_01.json`, `node_002_02.json`, ..., `node_002_50.json`
   - صيغة معرف العقدة داخل الملف: `"nodeId": "node_001_01"`
   - صيغة معرف النشاط: `"activityId": "act_001_01_01"`, `"act_001_01_02"`...

---

## 📐 3. الهيكل القياسي للملف (Exact JSON Schema)

كل ملف عقدة يجب أن يكون كائن JSON صالح 100% يحتوي على الحقول الرئيسية التالية:

```json
{
  "nodeId": "node_001_01",
  "title": "سورة الفاتحة: أم الكتاب وحمد الله والثناء عليه",
  "surahId": 1,
  "ayahStart": 1,
  "ayahEnd": 4,
  "activities": [
    {
      "activityId": "act_001_01_01",
      "type": "fill_in_the_blank",
      "ayahNumber": 1,
      "missingWordPosition": 2,
      "options": [
        "ٱللَّهِ",
        "ٱلرَّحْمَٰنِ",
        "ٱلرَّبِّ",
        "ٱلْخَالِقِ"
      ]
    },
    {
      "activityId": "act_001_01_02",
      "type": "next_ayah",
      "currentAyahNumber": 1,
      "correctNextAyahNumber": 2,
      "wrongOptionsAyahNumbers": [
        3,
        4
      ]
    }
  ],
  "tutorContext": {
    "surahName": "الفاتحة",
    "juz": 1,
    "theme": "بيان فضل البسملة وحمد الله سبحانه والثناء عليه بربوبيته للعالمين ورحمته وملكه ليوم الدين.",
    "ayahMeanings": {
      "1": "أبدأ قراءتي مستعيناً باسم الله العظيم، الرحمن ذي الرحمة الواسعة، الرحيم بالمؤمنين.",
      "2": "الثناء الكامل والشكر الخالص لله وحده، مالك جميع الخلائق ومدبر أمورهم.",
      "3": "الرحمن الذي وسعت رحمته كل شيء، الرحيم بعباده المؤمنين.",
      "4": "المالك وحده ليوم الجزاء والحساب وهو يوم القيامة."
    }
  }
}
```

---

## 🎯 4. تفاصيل بناء الأنشطة (Activity Specifications)

### أ) نشاط ملء الفراغ (`fill_in_the_blank`):
- **الهدف:** اختبار تثبيت الكلمات المفتاحية والمتشابهات.
- **الحقول:**
  - `"activityId"`: مُعرف فريد تسلسلي (مثال: `"act_002_01_01"`).
  - `"type"`: دائمًا `"fill_in_the_blank"`.
  - `"ayahNumber"`: رقم الآية المستهدفة ضمن نطاق العقدة.
  - `"missingWordPosition"`: الترتيب العددي للكلمة في الآية (1-indexed، مع استبعاد علامات الوقف `char_type_name == 'word'`).
  - `"options"`: مصفوفة تحتوي على **4 خيارات** بالرسم العثماني.
    - الخيار الأول `options[0]` هو الكلمة الصحيحة المطابقة للنص القرآني في هذا الموضع.
    - الخيارات الثلاثة الباقية `options[1..3]` مشتتات ذكية من القرآن بنفس الوزن والنوع الإعرابي (مثال: `["ٱلْمُتَّقِينَ", "ٱلصَّـٰلِحِينَ", "ٱلْمُفْلِحِينَ", "ٱلْمُحْسِنِينَ"]`).

### ب) نشاط الآية التالية (`next_ayah`):
- **الهدف:** تمكين روابط الحفظ وتفادي انقطاع التسلسل بين الآيات.
- **الحقول:**
  - `"activityId"`: مُعرف فريد تسلسلي.
  - `"type"`: دائمًا `"next_ayah"`.
  - `"currentAyahNumber"`: رقم الآية التي يقرؤها الحافظ الآن.
  - `"correctNextAyahNumber"`: رقم الآية التالية مباشرة (دائمًا `currentAyahNumber + 1`).
  - `"wrongOptionsAyahNumbers"`: مصفوفة من رقمين على الأقل (أرقام آيات أخرى من نفس السورة أو السياق)، يُشترط **ألا تتضمن** رقم الآية الصحيحة.

### ج) أسلوب التوزيع التناوبي (Interleaving):
- يتم وضع نشاطين إلى ثلاثة أنشطة فراغ لكل آية، ثم يُتبع بنشاط `next_ayah` للانتقال إلى الآية التي تليها، وتتكرر الدورة حتى نهاية آيات العقدة.

---

## 🧠 5. سياق المعلم الذكي (`tutorContext`)
في كل عقدة، يجب توفير كائن `tutorContext`:
- `"surahName"`: اسم السورة باللغة العربية (مثال: `"الفاتحة"` أو `"البقرة"`).
- `"juz"`: رقم الجزء (`1`).
- `"theme"`: فقرة موجزة وبليغة (2-3 أسطر) تشرح المحور العام والتربوي لآيات هذا المقطع.
- `"ayahMeanings"`: قاموس يحتوي على شرح ميسر ومضبوط لكل آية ضمن نطاق العقدة (`"1": "..."`, `"2": "..."`)، ليستعين به الذكاء الاصطناعي الصوتي عند تلميح وتصحيح أخطاء الطالب.

---

## 📝 6. بروتوكول التوثيق في `STRUCTURE_MAP.md`

عند الانتهاء من توليد أي عقد، يجب فتح ملف:
`your_project/backend/data/quran_oasis/STRUCTURE_MAP.md`

وإضافة/تحديث الجداول في قسم مخصص للجزء، على النمط التالي:

```markdown
## 📋 جدول عقد سورة الفاتحة كاملة (Surah 01: Al-Fatihah) — 7 آيات ✅

| المعرف (nodeId) | الملف | القسم الموضوعي | نطاق الآيات | عدد الأنشطة | الحالة |
| :--- | :--- | :--- | :---: | :---: | :---: |
| `node_001_01` | `node_001_01.json` | القسم 1: أم الكتاب والثناء على الله بربوبيته ورحمته | 1 - 4 | 7 أنشطة | ✅ تم التوليد والتدقيق |
| `node_001_02` | `node_001_02.json` | القسم 2: إخلاص العبادة والاستعانة ودعاء الصراط المستقيم | 5 - 7 | 8 أنشطة | ✅ تم التوليد والتدقيق |
```

---

## 🔍 7. سكريبت التحقق البرمجي السريع (Quick Validation Script)

يمكنك فحص ملفاتك المولدة في مسار `your_project/backend/data/quran_oasis/` للتأكد من خلوها من أي أخطاء:

```python
import json, glob, os

juz_dir = "your_project/backend/data/quran_oasis/juz_01"
files = sorted(glob.glob(os.path.join(juz_dir, "node_*.json")))
print(f"Checking {len(files)} files in juz_01...")

errors = []
for fpath in files:
    fname = os.path.basename(fpath)
    with open(fpath, 'r', encoding='utf-8') as f:
        data = json.load(f)
    
    # Check root keys
    for k in ["nodeId", "title", "surahId", "ayahStart", "ayahEnd", "activities", "tutorContext"]:
        if k not in data:
            errors.append(f"{fname}: Missing root key {k}")
            
    # Check activities
    for act in data.get("activities", []):
        atype = act.get("type")
        if atype == "fill_in_the_blank":
            if not act.get("missingWordPosition") or len(act.get("options", [])) < 2:
                errors.append(f"{fname} {act.get('activityId')}: Invalid blank config")
        elif atype == "next_ayah":
            if act.get("correctNextAyahNumber") in act.get("wrongOptionsAyahNumbers", []):
                errors.append(f"{fname} {act.get('activityId')}: Correct ayah found in wrong options!")

if not errors:
    print("✅ All files in juz_01 are 100% valid and compliant!")
else:
    print(f"❌ Found {len(errors)} issues:")
    for err in errors[:10]:
        print(" -", err)
```

---

*دليل مهندسي البيانات ونماذج الذكاء الاصطناعي — مشروع المصحف والتطبيقات الإسلامية المفتوحة (Digital Waqf)*
