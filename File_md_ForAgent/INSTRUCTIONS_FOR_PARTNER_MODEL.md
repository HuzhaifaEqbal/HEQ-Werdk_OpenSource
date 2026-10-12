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

2. **حجم العقدة التعليمية وطول المقاطع:**
   - عدد العقد وطول كل عقدة غير ثابتين بصورة جامدة؛ إذ يتحددان بناءً على خوارزميات التقسيم وطول المقطع وسياق المعنى القرآني.
   - في الآيات الطويلة (مثل آية الكرسي أو آية الدَّيْن)، قد تكون العقدة آية واحدة أو آيتين فقط تيسيراً على الحافظ.

3. **التسلسل والترابط التام (No Gaps, No Overlaps):**
   - يجب أن يبدأ ترقيم الآيات في السورة من الآية `1`.
   - بداية كل عقدة `ayahStart` يجب أن تساوي تماماً نهاية العقدة السابقة `ayahEnd + 1`.
   - نهاية العقدة الأخيرة في السورة يجب أن تطابق إجمالي عدد آيات السورة (الفاتحة: 7 آيات، البقرة: 286 آية).

4. **تسمية الملفات والمُعرفات (Naming Conventions):**
   - صيغة اسم الملف: `node_{surahId:03d}_{nodeIndex:02d}.json`
     - مثال سورة الفاتحة: `node_001_01.json`, `node_001_02.json`
     - مثال سورة البقرة: `node_002_01.json`, `node_002_02.json`...
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
    "theme": "بيان فضل البسملة وحمد الله سبحانه والثناء عليه بربوبيته للعالمين ورحمته وملكه ليوم الدين."
  }
}
```

---

## 🎯 4. تفاصيل بناء الأنشطة (Activity Specifications)

### أ) نشاط ملء الفراغ (`fill_in_the_blank`):
- **الهدف:** اختبار تثبيت الكلمات المفتاحية والمتشابهات بالرسم العثماني.
- **الحقول:**
  - `"activityId"`: مُعرف فريد تسلسلي (مثال: `"act_002_01_01"`).
  - `"type"`: دائمًا `"fill_in_the_blank"`.
  - `"ayahNumber"`: رقم الآية المستهدفة ضمن نطاق العقدة.
  - `"missingWordPosition"`: الترتيب العددي للكلمة في الآية (1-indexed، مع استبعاد علامات الوقف).
  - `"options"`: مصفوفة تحتوي على **4 خيارات** بالرسم العثماني (الخيار الصحيح وثلاثة مشتتات من القرآن).

### ب) نشاط الآية التالية (`next_ayah`):
- **الهدف:** تمكين روابط الحفظ وتفادي انقطاع التسلسل بين الآيات.
- **الحقول:**
  - `"activityId"`: مُعرف فريد تسلسلي.
  - `"type"`: دائمًا `"next_ayah"`.
  - `"currentAyahNumber"`: رقم الآية التي يقرؤها الحافظ الآن.
  - `"correctNextAyahNumber"`: رقم الآية التالية مباشرة (`currentAyahNumber + 1`).
  - `"wrongOptionsAyahNumbers"`: مصفوفة من رقمين على الأقل لا تتضمن رقم الآية الصحيحة.

---

## 🧠 5. سياق المعلم الذكي (`tutorContext`) واستدعاء التفسير

في كل عقدة، يتم توفير كائن `tutorContext` بالمحاور التالية:
- `"surahName"`: اسم السورة باللغة العربية (مثال: `"الفاتحة"` أو `"البقرة"`).
- `"juz"`: رقم الجزء.
- `"theme"`: فقرة موجزة تشرح المحور العام والتربوي لآيات هذا المقطع.

> 💡 **طريقة استدعاء التفسير:**  
> لا يتم تخزين تفاسير مكررة للآيات داخل ملفات العقد؛ بل يجلب التطبيق تفسير الآيات عند حاجة المستخدم عبر API يختاره المطوّر (مثل `your_API_ForTafseer` كـ placeholder توضيحي يحدده التطبيق).

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
