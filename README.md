# 🌟 المنظومة الإسلامية الرقمية المفتوحة — الوقف التقني
# Open Islamic Tech Architecture & Developer Datasets (Digital Waqf)

[![License Status](https://img.shields.io/badge/license-Under%20Review%20%2F%20قيد%20التحديد-yellow.svg)](#-الترخيص-وحقوق-الاستخدام--license)
[![Format](https://img.shields.io/badge/format-JSON%20UTF--8-blue.svg)]()
[![CDN](https://img.shields.io/badge/CDN-jsDelivr%20Global-orange.svg)]()
[![Platform](https://img.shields.io/badge/supports-Flutter%20%7C%20Web%20%7C%20AI%20Models-purple.svg)]()

> **المستودع الرسمي:** [https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource](https://github.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource)  
> **شبكة التوزيع (jsDelivr CDN):** `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/`  
> **الرابط المباشر (Raw GitHub):** `https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/`  

---

## 📖 مقدمة عامة | General Introduction

### 🇸🇦 بالعربية
مرحباً بك في **المنظومة الإسلامية الرقمية المفتوحة (HEQ Werdk Open Source - Digital Waqf)**.  
هذا المستودع وقف تقني مفتوح يهدف إلى تزويد المطورين والمهندسين والباحثين ببيانات ومناهج إسلامية تفاعلية مصممة وفق أسلوب التعليم المصغر (Micro-learning)، بما يشمل تحفيظ القرآن الكريم بالرسم العثماني، الفقه الميسر، أحكام التجويد، والسيرة النبوية الشريفة.

يمكن استدعاء البيانات والدروس مباشرة في التطبيقات والمواقع عبر شبكة CDN أو عبر روابط GitHub المباشرة دون الحاجة لإعداد خوادم مستقلة للبيانات الثابتة.

### 🇬🇧 In English
Welcome to the **Open Islamic Tech Architecture & Datasets Ecosystem (Digital Waqf)**.  
This open repository serves as a Digital Waqf providing structured educational datasets for Islamic and Quranic application developers. Built with micro-learning principles, the datasets encompass Quranic micro-memorization in Uthmanic script, simplified Fiqh, Tajweed phonetics, and chronological Prophetic Seerah.

Developers can consume these datasets directly in mobile and web applications via CDN or direct raw endpoints.

---

## 🗂️ خريطة المناهج والبيانات المتاحة | Curriculum Catalog

| المسار (Path) | الوصف بالعربية | English Description | رابط الفهرس (Manifest) | الدليل الكامل (Guide) |
|---|---|---|---|---|
| [`/tajweed`](./tajweed/) | **10 أبواب و 50 ملف JSON** لأحكام ومخارج وصفات التجويد | 10 modules (50 files) covering phonetics, makharij, and rules | [`manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/manifest.json) | [دليل التجويد](./tajweed/README.md) |
| [`/fiqh`](./fiqh/) | **أحكام الطهارة والصلاة والصيام** (معتمدة على المذهب الشافعي حالياً) | Fiqh dataset covering Taharah, Salah, and Sawm (Shafi'i madhhab) | [`manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/manifest.json) | [دليل الفقه](./fiqh/README.md) |
| [`/quran_oasis`](./quran_oasis/) | **عقد قرآنية للحفظ المصغر** بالرسم العثماني (جزء عمّ، تبارك، والفاتحة) | Bite-sized Quran memorization nodes in Uthmanic script | [`manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/manifest.json) | [دليل القرآن](./quran_oasis/README.md) |
| [`/AlSera_Alnabaoia`](./AlSera_Alnabaoia/) | **8 أبواب زمنية تضم 59 درساً** لأحداث السيرة النبوية مرتبة تاريخياً | Chronological Seerah curriculum containing 59 interactive lessons | [`manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/manifest.json) | [دليل السيرة](./AlSera_Alnabaoia/README.md) |
| [`/ALnawoi`](./ALnawoi/) | **أحاديث الأربعين النووية** مع سلاسل الأسانيد والفوائد الفقهية والتخريج | Imam Al-Nawawi's Hadiths with transmission chains & Fiqh points | [`manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/manifest.json) | [دليل الحديث](./ALnawoi/README.md) |
| [`/seerah_map`](./seerah_map/) | **خريطة السيرة النبوية الجغرافية** مع إحداثيات GPS والربط القرآني | Geospatial Prophetic Seerah map with GPS coordinates | [`manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/seerah_map/manifest.json) | [دليل الخريطة](./seerah_map/README.md) |
| [`/File_md_ForAgent`](./File_md_ForAgent/) | **أدلة وبرومبتات الذكاء الاصطناعي** ومعمارية الأنظمة السحابية والـ SSO | AI Prompts, Flutter specs, mascot guides & system architectures | [فهرس البرومبتات](./File_md_ForAgent/README.md) | [دليل المعمارية](./File_md_ForAgent/README.md) |

---

## ⚡ كيف تستدعي البيانات في مشروعك؟ | How to Consume the Data

### 1. عبر الروابط المباشرة (Instant Endpoints)

* **رابط الـ CDN (jsDelivr):**
  ```http
  https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/{DIRECTORY}/{PATH_TO_JSON}
  ```
* **رابط GitHub الخام (Raw GitHub):**
  ```http
  https://raw.githubusercontent.com/HuzhaifaEqbal/HEQ-Werdk_OpenSource/main/{DIRECTORY}/{PATH_TO_JSON}
  ```

---

## 💻 أكواد الاستدعاء التوضيحية | Integration Snippets

### 📱 1. في تطبيقات Flutter / Dart
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class IslamicDataService {
  static const String cdnBase = 
      'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main';

  /// استدعاء فهرس أي مسار ديناميكياً (tajweed / fiqh / quran_oasis / AlSera_Alnabaoia)
  static Future<Map<String, dynamic>> fetchManifest(String track) async {
    final response = await http.get(Uri.parse('$cdnBase/$track/manifest.json'));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load $track manifest');
  }

  /// استدعاء أي درس JSON محدد
  static Future<Map<String, dynamic>> fetchLesson(String path) async {
    final response = await http.get(Uri.parse('$cdnBase/$path'));
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    throw Exception('Failed to load lesson from $path');
  }
}

// مثال عملي للاستخدام:
void loadSample() async {
  final lesson = await IslamicDataService.fetchLesson(
    'tajweed/03_Nun_Sakinah_and_Tanween/01_izhar_halqi.json'
  );
  print('عنوان المفهوم: ${lesson['steps'][0]['title']}');
}
```

---

### 🌐 2. في تطبيقات الويب (JavaScript / TypeScript / React / Next.js / Vue)
```typescript
const CDN_BASE = 'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main';

// دالة عامة لجلب البيانات
export async function getIslamicCurriculum(filePath: string) {
  try {
    const response = await fetch(`${CDN_BASE}/${filePath}`);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error('Failed to fetch dataset:', error);
    throw error;
  }
}

// مثال: جلب درس الطهارة الأول
getIslamicCurriculum('fiqh/01_Taharah/01_water_and_purity.json')
  .then(data => console.log('Loaded Steps Count:', data.steps.length));
```

---

### 🐍 3. في لغة بايثون (Python Backend / Data Processing)
```python
import requests

CDN_BASE = "https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main"

def fetch_json(file_path: str) -> dict:
    url = f"{CDN_BASE}/{file_path}"
    response = requests.get(url)
    response.raise_for_status()
    response.encoding = 'utf-8'
    return response.json()

# مثال: جلب عقدة من جزء عم
node = fetch_json("quran_oasis/juz_30/node_078_01.json")
print(f"Surah ID: {node['surahId']} - Title: {node['title']}")
print(f"Activities: {len(node['activities'])}")
```

---

### 📟 4. عبر أوامر cURL (Terminal / Testing)
```bash
# Fetch Tajweed Manifest
curl -s "https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/manifest.json"

# Fetch Seerah Chapter 1
curl -s "https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/01_makka_w_wlada_alrasul.json"
```

---

## 🛡️ المبادئ والضوابط المتبعة | Core Principles

1. **حظر بعثرة القرآن الكريم (Strictly No Scrambled Verses):** التزاماً بقدسية كلام الله عز وجل، لا تحتوي الأنشطة القرآنية على أي خلط أو بعثرة للآيات، بل تعتمد على الحفظ بالتكرار، ملء الفراغات الموضعية، ومعرفة الآية التالية.
2. **الاعتماد المذهبي في الفقه:** المحتوى الفقهي المتوفر حالياً في المستودع مبني وفق معتمد المذهب الشافعي مع توثيق المسائل من كتب المذهب المعتمدة (متن أبي شجاع، فتح القريب، كفاية الأخيار).
3. **التوثيق التاريخي في السيرة:** التسلسل الزمني للأحداث مبني وفق المشهور والمحقق في مصادر السيرة النبوية (الرحيق المختوم، سيرة ابن هشام).

---

## 📄 الترخيص وحقوق الاستخدام | License & Rights

> ⚠️ **ملاحظة حول الترخيص:** نوع الترخيص القانوني المعتمد قيد التحديد والمراجعة حالياً من قبل صاحب المشروع لضمان التوافق مع حقوق الخطوط، الصوتيات، الأصول البصرية، والمراجع الشرعية.  
> المشروع متاح كوقف تقني مفتوح لأغراض التعلم والتطوير غير الربحي لخدمة المحتوى الإسلامي والقرآني.

---

*Waqf initiative for Islamic tech development and open educational resources.*
