# 🌐 دليل روابط الاستدعاء المباشر لمهندس الموقع (Web Developer CDN Directory)

> **موجّه لمهندس ومطور الموقع:** هذا الملف يحتوي على جميع روابط الـ CDN المباشرة لاستدعاء مجموعات البيانات الإسلامية (JSON) والوسائط دون الحاجة للدخول إلى مستودع GitHub.
> الروابط مفعّلة عبر شبكة توزيع المحتوى العالمية **jsDelivr CDN** ومزودة بـ CORS مفتوح افتراضياً لتعمل فوراً في تطبيقات الويب والهواتف بدون أي قيود أو حدود للمعدل (Rate Limits).

---

## 📌 الصيغة القياسية للروابط (URL Pattern)

```text
https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/{DIRECTORY}/{FILE_PATH}
```

* **المستودع الأساسي:** `HuzhaifaEqbal/HEQ-Werdk_OpenSource`
* **الفرع:** `main`
* **بروتوكول الاستدعاء:** `HTTPS GET`
* **نوع الاستجابة:** `application/json` (أو صيغ الوسائط للصور والخطوط)

---

## 🗂️ 1. فهارس المانيفست الديناميكية (Master Manifests)

> **💡 أفضل ممارسة للموقع:** بدلاً من كتابة روابط جميع الدروس يدوياً، يمكن للموقع استدعاء ملف `manifest.json` مرة واحدة لبناء القوائم والتصنيفات ديناميكياً ثم جلب ملف الدرس المختار.

| المسار التعليمي | رابط المانيفست (jsDelivr CDN) | الغرض والاستخدام |
| :--- | :--- | :--- |
| **أحكام التجويد** | [`tajweed/manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/manifest.json) | فهرس 10 أبواب و 50 درساً تفاعلياً مع مستويات الصعوبة والـ XP |
| **الفقه الشافعي** | [`fiqh/manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/manifest.json) | شجرة الفقه (الطهارة، الصلاة، الصيام) مع مستوياتها وأسئلتها |
| **واحة القرآن (الحفظ المصغر)** | [`quran_oasis/manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/manifest.json) | فهرس أجزاء عمّ (128 عقدة)، تبارك، والفاتحة بدون أي خلط |
| **السيرة النبوية التفاعلية** | [`AlSera_Alnabaoia/manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/manifest.json) | التسلسل الزمني لـ 8 حقب من المولد الشريف حتى الوفاة |
| **الأربعين النووية** | [`ALnawoi/manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/manifest.json) | فهرس الأحاديث الـ 42 مع روابط الدفعات والأسانيد والتخريج |
| **خريطة السيرة الجغرافية** | [`seerah_map/manifest.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/seerah_map/manifest.json) | فهرس أحداث السيرة مع إحداثيات GPS وروابط الآيات |

---

## 📖 2. روابط البيانات المباشرة حسب المسار (Direct Endpoints)

---

### 🟢 أولاً: مسار الأربعين النووية (`/ALnawoi`)

| الملف | الرابط المباشر (jsDelivr CDN) | وصف المحتوى ووظيفته |
| :--- | :--- | :--- |
| **المتون الكاملة (جميع الـ 42 حديث)** | [`nawawi_40_complete.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_complete.json) | يحتوي على جميع الأحاديث الـ 42 كاملة مع المتن، السند، التخريج، والمفردات في ملف واحد |
| **الدفعة 1 (الأحاديث 1 - 10)** | [`nawawi_40_batch_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_01.json) | أحاديث النية، أركان الإسلام والإيمان، النهي عن الابتداع، الحلال والحرام، النصيحة |
| **الدفعة 2 (الأحاديث 11 - 20)** | [`nawawi_40_batch_02.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_02.json) | الورع والشك، ترك ما لا يعني، حب الخير للمؤمنين، حرمة دم المسلم، إكرام الجار، الحياء |
| **الدفعة 3 (الأحاديث 21 - 30)** | [`nawawi_40_batch_03.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_03.json) | الاستقامة، أبواب الخير والصدقة، كف اللسان، حدود الله وفرائضه |
| **الدفعة 4 (الأحاديث 31 - 42)** | [`nawawi_40_batch_04.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/ALnawoi/nawawi_40_batch_04.json) | الزهد، لا ضرر ولا ضرار، البينة على المدعي، تغيير المنكر، فضل الذكر ومغفرة الذنوب |

---

### 🗺️ ثانياً: مسار خريطة السيرة الجغرافية المكانية (`/seerah_map`)

| الملف | الرابط المباشر (jsDelivr CDN) | وصف المحتوى ووظيفته |
| :--- | :--- | :--- |
| **أحداث وغزوات السيرة (الدفعة 1)** | [`seerah_major_events_batch_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/seerah_map/seerah_major_events_batch_01.json) | نقاط جغرافية مجهزة بـ `latitude` و `longitude` لغزوة بدر، أحد، الخندق، صلح الحديبية، وفتح مكة لعرضها على خرائط Mapbox / Leaflet / Google Maps |

---

### 🕌 ثالثاً: مسار السيرة النبوية الشريفة (`/AlSera_Alnabaoia`)

| الحقبة الزمنية | الرابط المباشر (jsDelivr CDN) | وصف المحتوى ووظيفته |
| :--- | :--- | :--- |
| **1. المولد والنشأة بمكة** | [`era_01_pre_islamic_and_birth.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/01_makka_w_wlada_alrasul.json) | أحوال جزيرة العرب قبل الإسلام، عام الفيل، رضاعته ﷺ، وكفالة جده وعمه |
| **2. الوحي والدعوة المكية** | [`era_02_dawah_in_makkah.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/02_alwahy_waldawa_fi_makka.json) | نزول الوحي في غار حراء، الدعوة السرية والجهرية، وصبر الصحابة |
| **3. التمهيد للهجرة** | [`era_03_altamhid_lilhijra.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/03_altamhid_lilhijra.json) | رحلة الطائف، الإسراء والمعراج، وبيعتي العقبة الأولى والثانية |
| **4. الهجرة وبناء المدينة** | [`era_04_alhijra_wbina_almadina.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/04_alhijra_wbina_almadina.json) | الهجرة النبوية، بناء المسجد النبوي، والمؤاخاة بين المهاجرين والأنصار |
| **5. الدفاع وبناء الدولة** | [`era_05_tathbit_almujtama.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/05_tathbit_almujtama_waldifaa.json) | معارك الدفاع عن المجتمع الإسلامي والتشريعات المدنية |
| **6. اتساع الدعوة وفتح مكة** | [`era_06_ittisaa_aldawa.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/06_ittisaa_aldawa_wfath_makka.json) | مكاتبة الملوك، صلح الحديبية، فتح مكة الأعظم، وتطهير الكعبة |
| **7. حجة الوداع والوفود** | [`era_07_hajjat_alwadaa.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/07_hajjat_alwadaa_walwufud.json) | عام الوفود، خطبة حجة الوداع، وتقرير حقوق الإنسان في الإسلام |
| **8. الرفيق الأعلى وأثر الرسالة** | [`era_08_akhir_hayat_alrasul.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/AlSera_Alnabaoia/08_akhir_hayat_alrasul_wathar_alrisala.json) | مرض النبي ﷺ ووفاته، وصاياه الأخيرة، وخلود الأثر الرسالي |

---

### ⚖️ رابعاً: مسار الفقه الشافعي الميسر (`/fiqh`)

#### 1. قسم الطهارة (`fiqh/01_Taharah`)
| الدرس | الرابط المباشر (jsDelivr CDN) | المحتوى |
| :--- | :--- | :--- |
| **أنواع المياه وأحكامها** | [`01_water_and_purity.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/01_Taharah/01_water_and_purity.json) | الماء المطلق، المستعمل، النجس، والمتغير |
| **فروض الوضوء وسننه** | [`02_wudu_fard_and_sunnah.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/01_Taharah/02_wudu_fard_and_sunnah.json) | الأركان الستة للوضوء مع السنن الشافعية |
| **نواقض الوضوء** | [`03_nullifiers_of_wudu.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/01_Taharah/03_nullifiers_of_wudu.json) | خروج الخارج، زوال العقل، مس الفرج، لمس البشرة |
| **الغسل وموجباته** | [`04_ghusl_and_major_purification.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/01_Taharah/04_ghusl_and_major_purification.json) | موجبات الغسل الأكبر وفروضه وكيفيته |
| **التيمم والمسح** | [`05_tayammum_and_wiping.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/01_Taharah/05_tayammum_and_wiping.json) | شروط التيمم، المسح على الخفين والجبيرة |
| **اختبار التحدي للطهارة** | [`06_boss_level_taharah.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/01_Taharah/06_boss_level_taharah.json) | أسئلة نوازل وسيناريوهات فقهية مجمعة |

#### 2. قسم الصلاة (`fiqh/02_Salah`)
* **المستوى 1 (الشروط والأركان والسنن):**
  - شروط الصلاة: [`level_1/01_conditions_of_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_1/01_conditions_of_prayer.json)
  - أركان الصلاة (13 أو 17 ركناً): [`level_1/02_pillars_of_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_1/02_pillars_of_prayer.json)
  - سنن الأبعاض والهيئات: [`level_1/03_sunan_of_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_1/03_sunan_of_prayer.json)
  - مبطلات الصلاة: [`level_1/04_invalidators_of_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_1/04_invalidators_of_prayer.json)
  - اختبار المستوى الأول: [`level_1/05_boss_level_salah_basics.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_1/05_boss_level_salah_basics.json)
* **المستوى 2 (الجماعة، المسافر، الجمعة، السهو):**
  - سجود السهو والتلاوة: [`level_2/01_sujud_al_sahw_and_tilawah.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_2/01_sujud_al_sahw_and_tilawah.json)
  - صلاة الجماعة والإمامة: [`level_2/02_congregational_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_2/02_congregational_prayer.json)
  - صلاة المسافر (القصر والجمع): [`level_2/03_traveler_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_2/03_traveler_prayer.json)
  - صلاة الجمعة وأحكامها: [`level_2/04_friday_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_2/04_friday_prayer.json)
  - صلاة الجنازة: [`level_2/05_funeral_prayer.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_2/05_funeral_prayer.json)
  - اختبار المستوى المتقدم: [`level_2/06_boss_level_salah_advanced.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/02_Salah/level_2/06_boss_level_salah_advanced.json)

#### 3. قسم الصيام (`fiqh/04_Sawm`)
* **المستوى 1 (الأركان والمفطرات):**
  - أركان الصيام وشروطه: [`level_1/01_sawm_pillars_and_conditions.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/04_Sawm/level_1/01_sawm_pillars_and_conditions.json)
  - مفطرات الصوم ومكروهاته: [`level_1/02_sawm_nullifiers.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/04_Sawm/level_1/02_sawm_nullifiers.json)
  - اختبار الصوم الميسر: [`level_1/03_boss_level_sawm_basics.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/04_Sawm/level_1/03_boss_level_sawm_basics.json)
* **المستوى 2 (القضاء والأعذار وزكاة الفطر):**
  - رخص الإفطار والقضاء والكفارة: [`level_2/01_sawm_exemptions_and_qada.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/04_Sawm/level_2/01_sawm_exemptions_and_qada.json)
  - زكاة الفطر وصيام التطوع: [`level_2/02_zakat_alfitr_and_sunnah_fasting.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/04_Sawm/level_2/02_zakat_alfitr_and_sunnah_fasting.json)
  - اختبار الصيام المتقدم: [`level_2/03_boss_level_sawm_advanced.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fiqh/04_Sawm/level_2/03_boss_level_sawm_advanced.json)

---

### 🎙️ خامساً: مسار أحكام التجويد (`/tajweed`)

يحتوي على 10 أبواب، كل باب يتألف من 5 دروس تفاعلية:

| الباب التعليمي | رابط الدرس الأول (نموذج) | رابط درس التحدي (Boss Level) |
| :--- | :--- | :--- |
| **1. المبادئ والمخارج** | [`01_intro_and_importance.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/01_Basics_and_Makharij/01_intro_and_importance.json) | [`05_boss_level_makharij.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/01_Basics_and_Makharij/05_boss_level_makharij.json) |
| **2. صفات الحروف** | [`01_sifat_intro.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/02_Sifat_Al_Huroof/01_sifat_intro.json) | [`05_boss_level_sifat.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/02_Sifat_Al_Huroof/05_boss_level_sifat.json) |
| **3. النون الساكنة والتنوين** | [`01_izhar_halqi.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/03_Nun_Sakinah_and_Tanween/01_izhar_halqi.json) | [`05_boss_level_nun.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/03_Nun_Sakinah_and_Tanween/05_boss_level_nun.json) |
| **4. الميم الساكنة والمشددة** | [`01_ikhfa_shafawi.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/04_Meem_Sakinah_and_Mushaddadah/01_ikhfa_shafawi.json) | [`05_boss_level_meem.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/04_Meem_Sakinah_and_Mushaddadah/05_boss_level_meem.json) |
| **5. المدود (الجزء الأول)** | [`01_madd_tabii.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/05_Madd_Rules_Part_1/01_madd_tabii.json) | [`05_boss_level_madd_1.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/05_Madd_Rules_Part_1/05_boss_level_madd_1.json) |
| **6. المدود (الجزء الثاني)** | [`01_madd_muttasil.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/06_Madd_Rules_Part_2/01_madd_muttasil.json) | [`05_boss_level_madd_2.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/06_Madd_Rules_Part_2/05_boss_level_madd_2.json) |
| **7. التفخيم والترقيق** | [`01_tafkheem_and_tarqeeq_basics.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/07_Tafkheem_and_Tarqeeq/01_tafkheem_and_tarqeeq_basics.json) | [`05_boss_level_tafkheem.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/07_Tafkheem_and_Tarqeeq/05_boss_level_tafkheem.json) |
| **8. علاقات الحروف** | [`01_mutamathilayn.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/08_Relations_Between_Letters/01_mutamathilayn.json) | [`05_boss_level_relations.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/08_Relations_Between_Letters/05_boss_level_relations.json) |
| **9. همزة الوصل والوقف** | [`01_hamzat_wasl_verbs.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/09_Hamzat_and_Waqf/01_hamzat_wasl_verbs.json) | [`05_boss_level_waqf.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/09_Hamzat_and_Waqf/05_boss_level_waqf.json) |
| **10. المقطوع والموصول والخاتمة** | [`01_maqtoo_and_mawsool_basics.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/10_Maqtoo_Mawsool_and_Conclusion/01_maqtoo_and_mawsool_basics.json) | [`05_boss_level_grand_finale.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/tajweed/10_Maqtoo_Mawsool_and_Conclusion/05_boss_level_grand_finale.json) |

---

### 🌿 سادساً: مسار واحة القرآن والحفظ المصغر (`/quran_oasis`)

* **سورة الفاتحة (الجزء 1):**
  - الآيات (1-7): [`juz_01/node_001_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_01/node_001_01.json)
* **سورة الملك (الجزء 29):**
  - المقطع الأول: [`juz_29/node_067_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_29/node_067_01.json)
* **جزء عمّ (الجزء 30 - 128 عقدة حفظ مصغر):**
  - سورة النبأ (المقطع 1): [`juz_30/node_078_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_30/node_078_01.json)
  - سورة الإخلاص: [`juz_30/node_112_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_30/node_112_01.json)
  - سورة الفلق: [`juz_30/node_113_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_30/node_113_01.json)
  - سورة الناس: [`juz_30/node_114_01.json`](https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/quran_oasis/juz_30/node_114_01.json)

---

## 🎨 3. مسار الوسائط والأصول البصرية (Media & UI Assets)

يمكن للموقع تضمين الأيقونات والصور والخلفيات والخطوط مباشرة في الـ CSS أو الـ `<img>` tags:

| نوع الأصل | الرابط القياسي المباشر |
| :--- | :--- |
| **الخطوط (Fonts)** | `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/fonts/{FONT_NAME}.ttf` |
| **الأيقونات (Icons)** | `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/icons/{ICON_NAME}.svg` |
| **الخلفيات (Wallpapers)** | `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/wallper/{IMAGE_NAME}.jpg` |
| **الملفات الصوتية (Audio)** | `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/audio/{AUDIO_FILE}.mp3` |

---

## 💻 4. نماذج أكواد جاهزة للنسخ المباشر للموقع (Copy-Paste Code Snippets)

### 1️⃣ جافاسكريبت نقية (Vanilla JavaScript / Fetch API)

```javascript
// دالة عامة لاستدعاء أي ملف من المستودع
async function fetchIslamicData(path) {
  const BASE_URL = 'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/';
  try {
    const response = await fetch(`${BASE_URL}${path}`);
    if (!response.ok) throw new Error(`HTTP Error: ${response.status}`);
    return await response.json();
  } catch (error) {
    console.error('Failed to load dataset:', error);
    return null;
  }
}

// مثال: استدعاء متن الأربعين النووية كاملاً
fetchIslamicData('ALnawoi/nawawi_40_complete.json').then(data => {
  console.log(`تم تحميل ${data.total_hadiths} حديث بنجاح!`);
  console.log('الحديث الأول:', data.hadiths[0].matn);
});
```

---

### 2️⃣ رياكت / نيكست جي اس (React / Next.js Hook)

```tsx
import { useState, useEffect } from 'react';

export function useIslamicManifest(track: 'tajweed' | 'fiqh' | 'ALnawoi' | 'AlSera_Alnabaoia') {
  const [manifest, setManifest] = useState<any>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const url = `https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/${track}/manifest.json`;
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        setManifest(data);
        setLoading(false);
      })
      .catch((err) => {
        console.error('Error fetching manifest:', err);
        setLoading(false);
      });
  }, [track]);

  return { manifest, loading };
}
```

---

### 3️⃣ فلاتر / دارت (Flutter / Dart Service)

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class IslamicCdnService {
  static const String baseUrl = 'https://cdn.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main';

  static Future<Map<String, dynamic>?> getSeerahMapEvents() async {
    final uri = Uri.parse('$baseUrl/seerah_map/seerah_major_events_batch_01.json');
    final response = await http.get(uri);
    if (response.statusCode == 200) {
      return jsonDecode(utf8.decode(response.bodyBytes));
    }
    return null;
  }
}
```

---

## ⚡ 5. ملاحظات تقنية هامة لمهندس الموقع (Technical Notes)

1. **دعم الـ CORS:** جميع الروابط تدعم `Access-Control-Allow-Origin: *` افتراضياً، وتعمل عبر أي دومين.
2. **السرعة والكاش (Caching):** تقوم شبكة jsDelivr بتوزيع الملفات على مئات السيرفرات السحابية العالمية لتقليل زمن الاستجابة (Latency < 25ms).
3. **تحديث الكاش الفوري (Cache Purge):** عند رفع أي تحديث جديد إلى GitHub، يمكنك تفريغ كاش jsDelivr فوراً بطلب الرابط بالشكل:
   ```text
   https://purge.jsdelivr.net/gh/HuzhaifaEqbal/HEQ-Werdk_OpenSource@main/{DIRECTORY}/{FILE_PATH}
   ```
4. **تجنب مشاكل تشفير الحروف العربية:** تأكد دائماً من قراءة الاستجابة بترميز `UTF-8` في تطبيقك حتى لا تظهر الحروف العربية كرموز مشوهة.
