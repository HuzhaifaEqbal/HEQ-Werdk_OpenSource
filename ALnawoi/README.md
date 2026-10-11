# 📜 الأربعون النووية — دليل المطور واستدعاء البيانات
## (An-Nawawi 40 Hadiths Dataset — Developer & API Integration Guide)

> **Repository:** [https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource](https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource)  
> **Direct Raw Endpoint:** `https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/ALnawoi/`  
> **Global Fast CDN (jsDelivr):** `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/`  
> **Format:** 100% Validated UTF-8 JSON | **Total Hadiths:** 40 | **Features:** Isnad Chains, Takhrij, Fiqh Topics

---

## 🌍 نظرة عامة (Overview)

### 🇸🇦 بالعربية
يوفر هذا المستودع قاعدة بيانات رقمية معيارية لـ **الأربعين النووية** للإمام يحيى بن شرف النووي رحمه الله. تتميز البيانات بالمتن المشكول بدقة، وتخريج الحديث، وسلسلة رجال السند (`isnadChain`) من شيخ المصنف وحتى الصحابي الجليل مع معرّفات فريدة للرواة (`narratorId`)، بالإضافة إلى القضايا الفقهية المستنبطة (`coreFiqhTopics`) والمعنى الإجمالي والفوائد التربوية.

### 🇬🇧 In English
This dataset provides a production-ready, structured digital edition of **Imam Al-Nawawi's Forty Hadiths**. Key features include fully vocalized Arabic Matn, academic authentication (Takhrij), relational transmission chains (`isnadChain`) with standardized narrator IDs (`narratorId`) suitable for network graph visualization, extracted jurisprudential subjects (`coreFiqhTopics`), and pedagogical lessons.

---

## ⚡ روابط الاستدعاء المباشر (Direct Endpoints)

### 1. المتن الكامل الموحد (Complete 40 Hadiths in One File)
* **jsDelivr CDN:**
  ```http
  https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_complete.json
  ```
* **Raw GitHub:**
  ```http
  https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/ALnawoi/nawawi_40_complete.json
  ```

### 2. الدفعات المقسمة (Batches: 10 Hadiths Each)
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_01.json
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_02.json
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_03.json
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_04.json
```

### 3. الفهرس الديناميكي (Dynamic Discovery Manifest)
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/manifest.json
```

---

## 📐 هيكل سجل الحديث (JSON Hadith Schema)

```json
{
  "hadithId": "nawawi_40_01",
  "number": 1,
  "title": "إنما الأعمال بالنيات",
  "matn": "عَنْ أَمِيرِ الْمُؤْمِنِينَ أَبِي حَفْصٍ عُمَرَ بْنِ الْخَطَّابِ رَضِيَ اللَّهُ عَنْهُ قَالَ: سَمِعْتُ رَسُولَ اللَّهِ صَلَّى اللَّهُ عَلَيْهِ وَسَلَّمَ يَقُولُ: «إِنَّمَا الأَعْمَالُ بِالنِّيَّاتِ...»",
  "primarySahabi": "عمر بن الخطاب رضي الله عنه",
  "takhrij": "رواه البخاري ومسلم في صحيحهما",
  "authenticity": "صحيح متفق عليه",
  "isnadChain": [
    {
      "step": 1,
      "narratorId": "narr_umar_01",
      "name": "عمر بن الخطاب",
      "role": "صحابي",
      "generation": "الصحابة",
      "grade": "صحابي جليل",
      "deathYearHijri": 23,
      "city": "المدينة المنورة"
    }
  ],
  "coreFiqhTopics": [
    "النية شرط لصحة الأعمال",
    "الإخلاص في العبادة",
    "الهجرة إلى الله ورسوله"
  ],
  "briefMeaning": "بيان أن صحة العمل وقبوله عند الله مرتبطان بقصد القلب وابتغاء وجه الله تعالى.",
  "pedagogicalPoints": [
    "أهمية مراقبة القصد في كل عمل",
    "التحذير من إرادة الدنيا بأعمال الآخرة"
  ]
}
```

---

## 💻 أكواد الاستدعاء الجاهزة (Ready Code Snippets)

### 📱 Flutter / Dart
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class NawawiHadithService {
  static const String completeUrl = 
      'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_complete.json';

  static Future<List<dynamic>> fetchAllHadiths() async {
    final response = await http.get(Uri.parse(completeUrl));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load Nawawi 40 dataset');
  }
}
```

### 🌐 JavaScript / TypeScript
```typescript
const NAWAWI_URL = 'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_complete.json';

async function getFortyHadiths() {
  const response = await fetch(NAWAWI_URL);
  if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
  return await response.json();
}

// Example usage:
getFortyHadiths().then(hadiths => {
  console.log('Total hadiths loaded:', hadiths.length);
  console.log('Hadith 1 Title:', hadiths[0].title);
});
```

### 🐍 Python
```python
import requests

url = "https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_complete.json"
resp = requests.get(url)
resp.raise_for_status()
resp.encoding = 'utf-8'
hadiths = resp.json()

print(f"Successfully loaded {len(hadiths)} hadiths.")
```

---

*Waqf & License: Open-source Prophetic Hadith dataset for scholars, developers, and educational platforms.*
