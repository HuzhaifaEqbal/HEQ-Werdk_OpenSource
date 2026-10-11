# 📐 مواصفة وسجل مواءمة الحجم والثيم (Scale & Theme Migration Specification)
## (Flutter UI Multi-Scale Sizing & Dynamic Theme Architecture Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **إدارة تحجيم النصوص والعناصر (Multi-Scale Sizing):** التحكم الشامل بـ 4 مقاييس (صغير جداً، صغير، متوسط، كبير) عبر `MediaQuery` و `textScaler`.
> * **دعم الوضعين الفاتح والداكن (Light/Dark Mode System):** تكييف كافة العناصر المشتركة وشاشات الواحات والصلوات مع الحفاظ على الأسطح الزجاجية والأنيميشن.
> * **سجل التغطية البرمجية (77 ملفاً):** توثيق تدقيق وتحديث كل ويدجت وشاشة في المشروع عبر 5 مراحل معمارية.
> * **الفئة المستهدفة:** مهندسو الواجهات الأمامية (Flutter)، ومطورو إمكانية الوصول والتصميم المتجاوب (Responsive UI).

---

## 📌 المرحلة 1: التأسيس والبنية المركزية (Core System & Navigation)
- [x] `lib/core/theme/app_theme_provider.dart` *(تأسيس مزود الحالة المركزي للحجم والثيم)*
- [x] `lib/main.dart` *(ربط المزود المركزي والتحجيم عبر MediaQuery ودعم Light/Dark)*
- [x] `lib/features/profile/screens/account_settings_screen.dart` *(إضافة خيارات واجهة التحكم بالحجم والثيم)*
- [x] `lib/core/widgets/heq_icon.dart` *(التحجيم التلقائي للأيقونات والـ SVG وتكيف الألوان مع الثيم)*
- [x] `lib/core/theme/app_typography.dart` *(مواءمة الخطوط والنصوص ودعم الوضع الفاتح)*
- [x] `lib/core/theme/app_colors.dart` *(لوحة الألوان المتكيفة مع الثيم)*
- [ ] `lib/core/services/api_service.dart`
- [ ] `lib/core/services/heq_sso_service.dart`
- [x] `lib/features/home/main_navigation_screen.dart` *(شريط التنقل السفلي الزجاجي المتكيف مع الثيم)*
- [x] `lib/features/splash/screens/preload_screen.dart` *(شاشة التحميل المسبق - متكيفة مع الثيم والألوان ومحفوظ فيها الأنميشن بالكامل)*

## 📌 المرحلة 2: العناصر المشتركة (Core Shared Widgets)
- [x] `lib/core/widgets/glass_container.dart` *(تحسين البلور المصنفر الحقيقي والتكيف التلقائي مع Light/Dark Mode وحدود واضحة)*
- [x] `lib/core/widgets/stadium_pill_button.dart` *(تحجيم تلقائي للارتفاع وحجم الخط وتكيف التباين الفاتح/الداكن)*
- [x] `lib/core/widgets/direct_text_field.dart` *(تحجيم الخطوط والمسافات بدقة، مع ألوان نصوص وخط فاصل متكيفة تماماً مع الوضعين)*
- [x] `lib/core/widgets/duolingo_prayer_card.dart` *(الاعتماد على GlassContainer المطور مع بلور مصنفر حقيقي وحدود ذهبية واضحة وألوان نصوص متكيفة)*
- [x] `lib/core/widgets/floating_snack_bar.dart` *(تحجيم الخطوط والمسافات مع حواف زجاجية محددة بارزة في الوضعين)*
- [x] `lib/core/widgets/mini_audio_player.dart` *(تحويل شريط التحكم ونافذة المؤقت إلى معيار البلور المصنفر المتكيف بالكامل مع الوضعين)*
- [x] `lib/core/widgets/simple_markdown_text.dart` *(تكيف لون النصوص الافتراضي مع الثيم الفاتح/الداكن وربطه بـ textScaler العام)*
- [x] `lib/core/widgets/standard_bottom_sheet.dart` *(الستايل الزجاجي الداكن الفاخر للنوافذ السفلية)*

## 📌 المرحلة 3: شاشات التعلم والواحات والهدهد (Learn & Fiqh Oasis)
- [x] `lib/features/learn/widgets/mascot_widget.dart` *(تحجيم أبعاد الهدهد تلقائياً بحسب إعدادات الحجم مع الحفاظ الكامل على أنميشن الـ WebP وسلاسته الكاشية)*
- [x] `lib/features/learn/screens/lesson_session_screen.dart` *(تطوير نافذة التقييم بالبلور المصنفر المتكيف، وتوافق تام لزر تحقق والخيارات والأبعاد مع مقياس الحجم ومقياس الثيم)*
- [x] `lib/features/fiqh_oasis/widgets/animated_classroom_board.dart` *(تكييف ألوان النص التفسيري مع الوضعين الفاتح والداكن، وربطها بنظام التحجيم مع الحفاظ 100% على حركات اللوح والهدهد)*
- [x] `lib/features/fiqh_oasis/screens/fiqh_session_screen.dart` *(تطوير شريط الإجراءات والتقييم بالبلور المصنفر المتكيف مع الوضعين الفاتح والداكن وربط الأزرار بالحجم العام دون المساس بالأنميشن)*
- [x] `lib/features/fiqh_oasis/screens/fiqh_map_screen.dart` *(الحفاظ الصارم 100% على مسار خريطة الفقه وأيقونات العقد والأمواج المائية المخصصة وألوان الفصول)*
- [x] `lib/features/fiqh_oasis/widgets/concept_chat_widget.dart` *(ربط النصوص التفسيرية بمقياس الخط العام مع الحفاظ الصارم 100% على فقاعات المحادثة وألوانها والردود السريعة)*
- [x] `lib/features/learn/learn_path_screen.dart` *(إصلاح كراش شجرة ListView، وتكييف ألوان العقد المكتملة والمسار في الوضع الفاتح مع Cyan بدلاً من الأسود، وحماية 100% لتصميم الخريطة والأنميشن)*
- [x] `lib/features/learn/models/learn_models.dart` *(نماذج البيانات لا تتطلب تعديلات الواجهة)*
- [x] `lib/features/learn/screens/himma_status_screen.dart` *(تكيف كامل مع الثيمين والألوان ووضوح النصوص)*
- [x] `lib/features/learn/screens/learn_tab_gateway_screen.dart` *(تطوير نافذة الواحات باستخدام GlassContainer الزجاجي الحديث والزر البيضاوي)*
- [x] `lib/features/learn/screens/lesson_result_screen.dart` *(تكييف بطاقات الإحصاءات والألوان وتجاوز المحتوى ليناسب الثيمين الفاتح والداكن)*
- [x] `lib/features/learning_path/screens/oases_map_screen.dart` *(تكييف خلفية الشاشة وفقاعات العناوين مع الوضعين الفاتح والداكن)*
- [x] `lib/features/learning_path/screens/session_screen.dart` *(تم التكييف مع الألوان الأساسية، رغم أن التطبيق يعتمد حالياً على lesson_session_screen)*
- [x] `lib/features/learning_path/services/learning_path_service.dart` *(خدمة لا تتطلب تعديلات واجهة)*
- [x] `lib/features/learning_path/widgets/audio_example_widget.dart` *(تطوير مشغل الصوت التعليمي ليتكيف مع ألوان الثيم الفاتح والداكن بدلاً من الأزرق الثابت)*
- [x] `lib/features/tutor/screens/smart_tutor_bottom_sheet.dart` *(تطوير نافذة المعلم الذكي وتكييفها مع الوضع الداكن والفاتح)*

## 📌 المرحلة 4: شاشات الكون ومواقيت الصلاة والمصادقة (Cosmic, Prayer & Auth)
- [x] `lib/features/cosmic_scale/cosmic_scale_screen.dart` *(إصلاح قص شريط المقياس الكوني، تم استبدال القائمة الأفقية الثابتة وجعلها مرنة وتجنب القص أسفل الشاشة)*
- [x] `lib/features/cosmic/screens/not_alone_screen.dart` *(تكييف الألوان بشكل متناسق وتحديث تصميم الهيدر)*
- [x] `lib/features/prayer_times/prayer_times_screen.dart` *(الستايل الزجاجي للشريط العلوي ونوافذ التوثيق البصري الفاخرة)*
- [x] `lib/features/prayer_times/screens/full_screen_adhan_screen.dart` *(جاهز ومكتمل فقهياً ولونياً)*
- [x] `lib/features/prayer_times/screens/prayer_location_map_screen.dart` *(جاهز ومتوافق)*
- [x] `lib/features/prayer_times/screens/prayer_settings_screen.dart` *(شاشة الإعدادات متكاملة)*
- [x] `lib/features/auth/screens/welcome_login_screen.dart` *(شاشة الترحيب تتبنى الثيمين الفاتح والداكن بدقة)*
- [x] `lib/features/auth/screens/login_with_password_screen.dart`
- [x] `lib/features/auth/screens/email_signup_screen.dart`
- [x] `lib/features/auth/screens/forgot_password_screen.dart`
- [x] `lib/features/auth/screens/otp_verification_screen.dart`
- [x] `lib/features/auth/screens/reset_password_screen.dart`
- [x] `lib/features/auth/screens/guest_info_screen.dart`
- [x] `lib/features/auth/widgets/heq_link_sso_button.dart`
- [x] `lib/features/auth/widgets/six_digit_otp_field.dart`

## 📌 المرحلة 5: القرآن الكريم والورد والمكتبة الصوتية والأنشطة (Quran, Audio & Profile)
- [ ] `lib/features/quran_wird/smart_wird_screen.dart`
- [ ] `lib/features/quran_wird/svg_mushaf_page_widget.dart`
- [ ] `lib/features/quran_wird/tajweed_text_renderer.dart`
- [ ] `lib/features/quran_wird/quran_tab_screen.dart`
- [ ] `lib/features/quran_wird/quran_index_sheet.dart`
- [ ] `lib/features/quran_wird/audio_timing_service.dart`
- [ ] `lib/features/quran_wird/global_ayah_helper.dart`
- [ ] `lib/features/quran_wird/mushaf_download_service.dart`
- [ ] `lib/features/quran_wird/quran_ayah_bounds.dart`
- [ ] `lib/features/quran_wird/quran_metadata.dart`
- [ ] `lib/features/quran_wird/quran_polygon_parser.dart`
- [ ] `lib/features/quran_oasis/screens/quran_juz_screen.dart`
- [ ] `lib/features/quran_oasis/screens/quran_map_screen.dart`
- [ ] `lib/features/quran_oasis/screens/quran_session_screen.dart`
- [ ] `lib/features/quran_oasis/screens/voice_challenge_screen.dart`
- [ ] `lib/features/audio_library/models/reciter.dart`
- [x] `lib/features/audio_library/screens/audio_library_screen.dart` *(تم التكييف مع الألوان المضيئة والداكنة)*
- [x] `lib/features/audio_library/screens/reciter_surahs_screen.dart` *(تم إضافة ميزة البحث وتجميل أزرار التنزيل والتشغيل مع التكييف اللوني)*
- [ ] `lib/features/audio_library/services/audio_download_service.dart`
- [ ] `lib/features/audio_library/services/background_audio_service.dart`
- [x] `lib/features/profile/profile_screen.dart`
- [x] `lib/features/profile/screens/achievements_center_screen.dart`
- [x] `lib/features/profile/screens/edit_profile_screen.dart`
- [x] `lib/features/profile/screens/public_profile_screen.dart`
- [x] `lib/features/onboarding/screens/interactive_onboarding_screen.dart`
- [x] `lib/features/onboarding/screens/learning_path_setup_screen.dart`
- [x] `lib/features/sadaqah_hub/sadaqah_hub_screen.dart`
- [x] `lib/features/tasbih/tasbih_screen.dart`
