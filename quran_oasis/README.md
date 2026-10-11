# 🕋 واحة القرآن الكريم — دليل المطور واستدعاء بيانات الحفظ المصغر
## (Quran Oasis Micro-Hifz Curriculum — Developer & API Integration Guide)

> **Repository:** [https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource](https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource)  
> **Direct Raw Endpoint:** `https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/quran_oasis/`  
> **Global Fast CDN (jsDelivr):** `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/`  
> **Script:** Uthmanic Arabic Script (الرسم العثماني المعتمد)  
> **Core Principle:** **ممنوع البعثرة مطلقاً (STRICTLY NO SCRAMBLING)**  
> **Format:** 100% Validated UTF-8 JSON

---

## 🌍 نظرة عامة (Overview)

### 🇸🇦 بالعربية
توفر واحة القرآن الكريم هيكلية بيانات قرآنية مبتكرة تعتمد على أسلوب **الحفظ المصغر (Micro-Hifz)**. يتم تقسيم كل سورة قرآنية إلى عقد تعليمية صغيرة ومتسلسلة (تتراوح بين 3 إلى 5 آيات لكل عقدة)، تتضمن أنشطة تفاعلية لترسيخ الحفظ:
1. **تحدي الكلمة المفقودة بالرسم العثماني (`fill_in_the_blank`):** اختبار المتشابهات ورسم الكلمات دون تشتيت.
2. **تحدي تخمين الآية التالية (`next_ayah`):** تمكين روابط الوصل بين الآيات ومنع التردد.
3. **سياق المعلم الذكي (`tutorContext`):** معاني الآيات والمحور الموضوعي للرد الفوري على أسئلة الطالب.
> **قاعدة شرعية صارمة:** يُحظر تماماً أي نشاط لبعثرة أو إعادة ترتيب كلمات القرآن الكريم أو الآيات احتراماً لقدسية كلام الله عز وجل.

### 🇬🇧 In English
The Quran Oasis repository delivers an innovative, bite-sized Quran memorization dataset (Micro-Hifz Architecture). Each Surah is structured into sequential micro-learning nodes (3 to 5 verses per node) containing interactive memorization reinforcement activities:
1. **Uthmanic Fill-in-the-Blank (`fill_in_the_blank`):** Testing accurate recall with authentic mutashabihat distractors.
2. **Next Ayah Recall (`next_ayah`):** Reinforcing cognitive transitions between consecutive verses.
3. **Smart Tutor Context (`tutorContext`):** Verse meanings and thematic overviews for conversational AI agents.
> **Sacred Rule:** Strictly no scrambled words or disordered verses are permitted in any activity, preserving the sanctity and exact order of the Noble Quran.

---

## ⚡ روابط الاستدعاء المباشر (Direct Endpoints)

### 1. عبر خادم GitHub الخام (Raw GitHub API)
```http
https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/quran_oasis/{JUZ_FOLDER}/{NODE_FILE}
```
**Examples:**
* An-Naba Node 1 (Juz 30):
  ```http
  https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/quran_oasis/juz_30/node_078_01.json
  ```
* Al-Mulk Node 1 (Juz 29):
  ```http
  https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/quran_oasis/juz_29/node_067_01.json
  ```

### 2. عبر شبكة التوزيع العالمية فائقة السرعة (jsDelivr CDN)
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/{JUZ_FOLDER}/{NODE_FILE}
```
**Example:**
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_30/node_078_01.json
```

### 3. الفهرس الديناميكي المجمع (Dynamic Discovery Manifest)
```http
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/manifest.json
```

---

## 📐 هيكل بيانات العقدة القرآنية (JSON Node Schema)

```json
{
  "nodeId": "hifz_078_01",
  "title": "سورة النبأ - المقطع الأول (النبأ العظيم)",
  "surahId": 78,
  "ayahStart": 1,
  "ayahEnd": 5,
  "activities": [
    {
      "type": "fill_in_the_blank",
      "ayahNumber": 1,
      "missingWord": "يَتَسَاءَلُونَ",
      "missingWordPosition": 2,
      "options": ["يَتَسَاءَلُونَ", "يَخْتَلِفُونَ", "يَتَذَكَّرُونَ"]
    },
    {
      "type": "next_ayah",
      "currentAyahNumber": 1,
      "correctNextAyahNumber": 2,
      "wrongOptionsAyahNumbers": [3, 4]
    }
  ],
  "tutorContext": {
    "surahName": "النبأ",
    "juz": 30,
    "theme": "بيان عظمة يوم القيامة ودلائل قدرة الله في الكون والرد على المشركين.",
    "ayahMeanings": {
      "1": "عن أي شأن عظيم يتساءل هؤلاء المشركون؟",
      "2": "عن القرآن والبعث والرسالة النبوية التي اختلفوا فيها."
    }
  }
}
```

---

## 💻 أكواد الاستدعاء الجاهزة (Ready Code Snippets)

### 📱 Flutter / Dart
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class QuranOasisService {
  static const String baseUrl = 
      'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis';

  // 1. Fetch Dynamic Manifest
  static Future<Map<String, dynamic>> fetchManifest() async {
    final response = await http.get(Uri.parse('$baseUrl/manifest.json'));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load Quran Oasis manifest');
  }

  // 2. Fetch Specific Quran Node
  static Future<Map<String, dynamic>> fetchNode(String juzFolder, String nodeFile) async {
    final response = await http.get(Uri.parse('$baseUrl/$juzFolder/$nodeFile'));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load Quran node: $nodeFile');
  }
}
```

### 🌐 JavaScript / TypeScript
```typescript
const QURAN_BASE_URL = 'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis';

async function getQuranNode(juzFolder: string, nodeFile: string) {
  const response = await fetch(`${QURAN_BASE_URL}/${juzFolder}/${nodeFile}`);
  if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
  return await response.json();
}

// Example usage:
getQuranNode('juz_30', 'node_078_01.json')
  .then(data => console.log('Loaded node activities:', data.activities.length));
```

### 🐍 Python
```python
import requests

QURAN_BASE_URL = "https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis"

def fetch_quran_node(juz_folder: str, node_file: str) -> dict:
    url = f"{QURAN_BASE_URL}/{juz_folder}/{node_file}"
    resp = requests.get(url)
    resp.raise_for_status()
    resp.encoding = 'utf-8'
    return resp.json()

# Example:
node = fetch_quran_node("juz_30", "node_078_01.json")
print("Surah ID:", node['surahId'], "Title:", node['title'])
```

---

## 🗂️ فهرس الأجزاء والسور (Ajzaa & Surahs Index)

| الجزء (Juz) | المسار (Path) | نطاق السور | عدد العقد (Nodes) | نوع الأنشطة |
|-------------|--------------|------------|--------------------|--------------|
| **جزء عمّ (Juz 30)** | `juz_30/` | سورة 78 (النبأ) إلى سورة 114 (الناس) | 128 عقدة كاملة | فراغات + تخمين الآية التالية |
| **جزء تبارك (Juz 29)** | `juz_29/` | سورة 67 (الملك) إلى سورة 77 (المرسلات) | سورة الملك والقلم والحاقة والمعارج... | فراغات + تخمين الآية التالية |
| **جزء ألم (Juz 1)** | `juz_01/` | سورة 1 (الفاتحة) وسورة 2 (البقرة) | عقد الفاتحة وبدايات البقرة | فراغات + تخمين الآية التالية |

---

*Waqf & License: Open-source Quranic memorization technology for Muslim developers and learners globally.*
