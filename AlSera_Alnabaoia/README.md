# 📜 واحة السيرة النبوية الشريفة — دليل المطور واستدعاء البيانات
## (Prophetic Seerah Interactive Curriculum — Developer & API Integration Guide)

> **Repository:** [https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource](https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource)  
> **Direct Raw Endpoint:** `https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/AlSera_Alnabaoia/`  
> **Global Fast CDN (jsDelivr):** `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/`  
> **Structure:** 8 Chronological Chapters | **Format:** 100% Validated UTF-8 JSON

---

## 🌍 نظرة عامة (Overview)

### 🇸🇦 بالعربية
يوفر مسار السيرة النبوية الشريفة تسلسلاً تاريخياً وتربوياً متكاملاً لحياة النبي محمد ﷺ، مقسماً إلى **8 أبواب زمنية** من مكة قبل البعثة والنشأة وحتى حجة الوداع وأثر الرسالة. يتميز المنهج بالاعتماد على الروايات الثابتة وتوثيق كل بطاقة شرح (`concept`) بالمصادر المعتمدة (الرحيق المختوم، سيرة ابن هشام، وتاريخ الطبري) بروابط إلكترونية للمكتبة الشاملة، مع أسئلة تفاعلية متنوعة تشمل ترتيب الأحداث زمنياً (`scrambled_words`) ومواقف الصحابة والسيناريوهات النبوية (`scenario_based`).

### 🇬🇧 In English
The Prophetic Seerah Curriculum offers a verified chronological journey through the life of Prophet Muhammad ﷺ, divided into **8 historical chapters** spanning pre-Islamic Mecca and his birth to the Farewell Pilgrimage and the enduring impact of his message. Each concept card is paired with classical historical citations (Ar-Raheeq Al-Makhtum, Sirah Ibn Hisham) and direct library links, followed by contextual activities including timeline chronology ordering (`scrambled_words`), historical scenarios (`scenario_based`), and knowledge checkpoints.

---

## ⚡ روابط الاستدعاء المباشر (Direct Endpoints)

### 1. عبر خادم GitHub الخام (Raw GitHub API)
```http
https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/AlSera_Alnabaoia/data/{CHAPTER_FILE}
```
**Examples:**
* Chapter 1 (Birth & Upbringing):
  ```http
  https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/AlSera_Alnabaoia/data/01_makka_w_wlada_alrasul.json
  ```
* Chapter 4 (Migration & Medina):
  ```http
  https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/AlSera_Alnabaoia/data/04_alhijra_wbina_almadina.json
  ```

### 2. عبر شبكة التوزيع السحابية فائقة السرعة (jsDelivr CDN)
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/data/{CHAPTER_FILE}
```
**Example:**
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/data/01_makka_w_wlada_alrasul.json
```

### 3. الفهرس الديناميكي المجمع (Dynamic Discovery Manifest)
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/manifest.json
```

---

## 📐 هيكل بيانات السيرة (JSON Schema)

```json
{
  "lesson_id": "01_makka_before_islam",
  "title": "مكة والبيت الحرام في زمن قريش",
  "steps": [
    {
      "type": "concept",
      "title": "مكانة مكة وقريش في جزيرة العرب",
      "content": "كانت مكة مركزاً تجارياً ودينياً بفضل الكعبة المشرفة ورحلتي الشتاء والصيف...",
      "sources": [
        {
          "book": "الرحيق المختوم - المباركفوري",
          "link": "https://shamela.ws/book/115/15"
        }
      ]
    },
    {
      "type": "question",
      "question_type": "scrambled_words",
      "question_text": "رتب أحداث تجديد بناء الكعبة الشريفة بالترتيب الصحيح:",
      "correct_order": [
        "سيل جارف يصدع جدران الكعبة",
        "اتفاق قريش على إعادة البناء بمال حلال",
        "الخلاف على من يضع الحجر الأسود",
        "تحكيم أول داخل وهو النبي الأمين ﷺ"
      ],
      "explanation": "أعادت قريش بناء الكعبة واختلفت في وضع الحجر الأسود حتى رأت محمداً ﷺ فرضيت بحكمه."
    }
  ]
}
```

---

## 💻 أكواد الاستدعاء الجاهزة (Ready Code Snippets)

### 📱 Flutter / Dart
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class SeerahService {
  static const String baseUrl = 
      'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia';

  // 1. Fetch Dynamic Manifest
  static Future<Map<String, dynamic>> fetchManifest() async {
    final response = await http.get(Uri.parse('$baseUrl/manifest.json'));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load Seerah manifest');
  }

  // 2. Fetch Specific Seerah Chapter
  static Future<List<dynamic>> fetchChapter(String chapterFile) async {
    final response = await http.get(Uri.parse('$baseUrl/data/$chapterFile'));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load Seerah chapter: $chapterFile');
  }
}
```

### 🌐 JavaScript / TypeScript
```typescript
const SEERAH_BASE_URL = 'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia';

async function getSeerahChapter(chapterFile: string) {
  const response = await fetch(`${SEERAH_BASE_URL}/data/${chapterFile}`);
  if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
  return await response.json();
}

// Example usage:
getSeerahChapter('01_makka_w_wlada_alrasul.json')
  .then(lessons => console.log('Loaded lessons count:', lessons.length));
```

### 🐍 Python
```python
import requests

SEERAH_BASE_URL = "https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia"

def fetch_seerah_chapter(chapter_file: str) -> list:
    url = f"{SEERAH_BASE_URL}/data/{chapter_file}"
    resp = requests.get(url)
    resp.raise_for_status()
    resp.encoding = 'utf-8'
    return resp.json()

# Example:
chapter = fetch_seerah_chapter("04_alhijra_wbina_almadina.json")
print("Total lessons in migration chapter:", len(chapter))
```

---

## 🗂️ فهرس الأبواب الزمنية (Chronological Chapters Index)

| الباب (#) | اسم الملف (File) | العنوان بالعربية | English Title | عدد الدروس |
|---|---|---|---|---|
| 01 | `01_makka_w_wlada_alrasul.json` | مكة قبل البعثة والمولد والنشأة | Pre-Islamic Mecca, Birth & Upbringing | 8 دروس |
| 02 | `02_alwahy_waldawa_fi_makka.json` | بدء الوحي والدعوة في مكة | Revelation & Meccan Call | 10 دروس |
| 03 | `03_altamhid_lilhijra.json` | التمهيد للهجرة والبيعات | Preparations for Hijrah | 5 دروس |
| 04 | `04_alhijra_wbina_almadina.json` | الهجرة وبناء المجتمع المدني | Migration & Establishing Medina | 8 دروس |
| 05 | `05_tathbit_almujtama_waldifaa.json` | تثبيت المجتمع والدفاع عن الرسالة | Defending the Message & Battles | 10 دروس |
| 06 | `06_ittisaa_aldawa_wfath_makka.json` | اتساع الدعوة وفتح مكة | Spread of Islam & Mecca Conquest | 8 دروس |
| 07 | `07_hajjat_alwadaa_walwufud.json` | عام الوفود وحجة الوداع | Delegations & Farewell Pilgrimage | 7 دروس |
| 08 | `08_akhir_hayat_alrasul_wathar_alrisala.json` | آخر حياة النبي ﷺ وأثر الرسالة | Final Days & Enduring Legacy | 8 دروس |

---

*Waqf & License: Open-source Prophetic Seerah dataset for non-profit Islamic educational development worldwide.*
