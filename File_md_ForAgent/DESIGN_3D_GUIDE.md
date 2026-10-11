# 🎨 دليل ومواصفات الأصول ثلاثية الأبعاد (3D Assets)
## (3D Spatial Assets, Animations & Styling Specification)

> ### 📌 الوظائف والمهام الأساسية لهذا الملف (File Functions & Scope):
> * **توثيق مكتبة الأصول ثلاثية الأبعاد (Glaze 3D Icons):** تصنيف الأشكال المجسمة (23 مجانياً + 80 مدفوعاً) وصيغ PNG / SVG.
> * **محرك التحريك والمؤثرات البرمجية:** كود التحريك الانسيابي (Float Animation)، تأثير النبض (Pulse)، والتلاشي والظلال الاحترافية في CSS وفلاتر.
> * **قواعد وضوابط الاستخدام في واجهات المستخدم:** متى تُستخدم الأصول ثلاثية الأبعاد (الإنجازات، الترحيب، العقد الكبرى) ومتى تُمنع (لتجنب التشتيت).
> * **الفئة المستهدفة:** مصممو الرسوميات (Graphic Designers)، مهندسو الواجهات الأمامية، ومطورو الويب والموبايل.

---

> ### 🤖 برومبت التوجيه للذكاء الاصطناعي (Master AI Prompt to Copy-Paste):
> **انسخ النص التالي ووجهه مباشرة إلى نموذج الذكاء الاصطناعي (Claude / GPT / Gemini):**
> ```text
> بصفتك مهندس مؤثرات بصرية وواجهات تفاعلية (Frontend Animation & Visual Effects Engineer):
> مهمتك هي دمج الأصول البصرية ثلاثية الأبعاد وتطبيق تأثيرات الحركة الانسيابية (Floating, Pulse, Glow Shadows) في واجهات الويب وتطبيقات الهاتف الذكي.
> 
> إرشادات التطبيق وبيئة العمل:
> 1. مسار المشروع: نظم الأصول البصرية داخل `your_project/assets/3d/` و `your_project/lib/core/widgets/animations/`.
> 2. استدعاء ملفات الـ Lottie و 3D: استخدم مسارات عامة بصيغة `your_project/assets/animations/your_file.json`.
> 3. التزم بقواعد الأداء والتحريك السلس وتجنب التشتيت البصري وفق الضوابط الموضحة أدناه.
> ```

---

## 📦 المصدر المستخدم: Glaze 3D Icons

| التفاصيل | القيمة |
|---------|-------|
| **الاسم** | Glaze – 3D Icons FREE SAMPLE |
| **المصدر** | Figma Community (GRAFIK STASH) |
| **رابط Figma** | https://www.figma.com/design/7XLWhj3b5c0xYByKyDVJNy/Glaze |
| **المصدر الرسمي** | https://grafikstash.com |
| **العدد (المجاني)** | 23 شكل 3D |
| **العدد (المدفوع)** | 80+ شكل |
| **الصيغ** | PNG / SVG |
| **التوافق** | Figma, Sketch, أي مشروع ويب أو موبايل |

---

## 🧠 ما هي هذه الملفات تقنياً؟

هي **صور جاهزة (PNG)** مُصدَّرة من محرك 3D داخل Figma.
**ليست كوداً ثلاثي الأبعاد قابلاً للتحريك** — بل أشكال مجسّمة جميلة يمكن استخدامها كأصول بصرية.

```
✅ أشكال 3D مجردة وألوان زاهية جذابة
✅ قابلة لتغيير الألوان داخل Figma
✅ خفيفة وسريعة التحميل عند الاستخدام كـ PNG
❌ لا يمكن تعديل شكلها الهندسي برمجياً
❌ تغيير الألوان برمجياً محدود (تقريبي)
```

---

## ✅ ما الذي نستطيع فعله برمجياً بهذه الصور؟

### 1. التحريك والتدوير (CSS)
```css
.glaze-shape {
  animation: float 4s ease-in-out infinite;
  transform-origin: center;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50%       { transform: translateY(-20px) rotate(5deg); }
}
```

### 2. تأثير النبض (Pulse)
```css
@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 0.9; }
  50%       { transform: scale(1.08); opacity: 1; }
}
```

### 3. إضافة ظل احترافي
```css
.glaze-shape {
  filter: drop-shadow(0px 20px 40px rgba(108, 99, 255, 0.4));
}
```

### 4. تغيير اللون (تقريبي)
```css
/* تغيير الصبغة اللونية */
.glaze-shape { filter: hue-rotate(90deg); }

/* تحويل للأزرق */
.glaze-shape { filter: sepia(1) hue-rotate(190deg) saturate(2); }
```

### 5. تأثير Parallax (JavaScript)
```javascript
window.addEventListener('mousemove', (e) => {
  const shape = document.querySelector('.glaze-shape');
  const x = (e.clientX / window.innerWidth - 0.5) * 30;
  const y = (e.clientY / window.innerHeight - 0.5) * 30;
  shape.style.transform = `translate(${x}px, ${y}px)`;
});
```

### 6. في React Native (مشروعنا)
```jsx
import { Animated, Image } from 'react-native';

const spinValue = new Animated.Value(0);

Animated.loop(
  Animated.timing(spinValue, {
    toValue: 1,
    duration: 6000,
    useNativeDriver: true,
  })
).start();

const rotate = spinValue.interpolate({
  inputRange: [0, 1],
  outputRange: ['0deg', '360deg'],
});

// الاستخدام
<Animated.Image
  source={require('./assets/glaze_shape.png')}
  style={{
    width: 200,
    height: 200,
    transform: [{ rotate }],
    opacity: 0.9,
  }}
/>
```

---

## ❌ ما الذي لا نستطيع فعله مع PNG؟

| المطلوب | السبب |
|---------|-------|
| تغيير شكل الجسم الهندسي | الصورة ثابتة، ليست نموذج 3D حقيقي |
| تغيير لون دقيق احترافي | الألوان مدمجة في الـ pixels |
| إضافة إضاءة ديناميكية | لا يوجد محرك 3D حقيقي |
| التفاعل مع الفيزياء (جاذبية، اصطدام) | يحتاج Three.js أو محرك حقيقي |

---

## 🔥 البدائل الأقوى: التحكم الكامل برمجياً

### الخيار 1: Three.js (الأقوى)

**المصدر:** https://threejs.org
**npm:** `npm install three`

```javascript
import * as THREE from 'three';

// إنشاء المشهد
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });

// إضافة شكل
const geometry = new THREE.TorusKnotGeometry(10, 3, 100, 16);
const material = new THREE.MeshStandardMaterial({
  color: 0x6C63FF,
  roughness: 0.3,
  metalness: 0.7,
});
const mesh = new THREE.Mesh(geometry, material);
scene.add(mesh);

// إضافة إضاءة
const light = new THREE.DirectionalLight(0xffffff, 1);
light.position.set(5, 5, 5);
scene.add(light);

// تدوير تلقائي
function animate() {
  requestAnimationFrame(animate);
  mesh.rotation.x += 0.01;
  mesh.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();
```

| المميزات | التفاصيل |
|---------|---------|
| تحكم 100% | الشكل، اللون، الإضاءة، الحركة |
| تفاعلي | يستجيب للمس والماوس |
| أي شكل هندسي | كرة، مكعب، TorusKnot، وغيرها |
| المشروع | مفتوح المصدر ومجاني |

---

### الخيار 2: Spline (الأسهل والأجمل) ⭐ **موصى به للمبتدئين**

**المصدر:** https://spline.design
**توثيق React:** https://docs.spline.design/doc/react

```bash
npm install @splinetool/react-spline @splinetool/runtime
```

```jsx
import Spline from '@splinetool/react-spline';

export default function App() {
  return (
    <Spline scene="https://prod.spline.design/your-scene-url/scene.splinecode" />
  );
}
```

| المميزات | التفاصيل |
|---------|---------|
| واجهة بصرية سهلة | مثل Figma لكن بالـ 3D |
| تصدير مباشر | كـ React Component أو iframe |
| تفاعلي | أنيميشن عند Hover أو Click |
| مجاني | للمشاريع الصغيرة |
| جودة عالية | نتائج احترافية بدون خبرة 3D |

---

### الخيار 3: React Three Fiber (Three.js + React)

**المصدر:** https://docs.pmnd.rs/react-three-fiber
**npm:** `npm install @react-three/fiber @react-three/drei three`

```jsx
import { Canvas } from '@react-three/fiber';
import { OrbitControls, MeshDistortMaterial } from '@react-three/drei';

export default function Scene() {
  return (
    <Canvas>
      <ambientLight intensity={0.5} />
      <directionalLight position={[10, 10, 5]} />
      <mesh>
        <torusKnotGeometry args={[1, 0.3, 128, 16]} />
        <MeshDistortMaterial
          color="#6C63FF"
          distort={0.4}
          speed={2}
        />
      </mesh>
      <OrbitControls enableZoom={false} />
    </Canvas>
  );
}
```

---

### الخيار 4: CSS 3D Transforms (الأخف والأبسط)

لا يحتاج مكتبات. مناسب للأشكال البسيطة:

```css
.cube {
  width: 100px;
  height: 100px;
  transform-style: preserve-3d;
  animation: rotateCube 8s linear infinite;
}

@keyframes rotateCube {
  from { transform: rotateX(0deg) rotateY(0deg); }
  to   { transform: rotateX(360deg) rotateY(360deg); }
}
```

---

## 📊 مقارنة الخيارات — اختر الأنسب

| المعيار | Glaze PNG | CSS 3D | Spline | Three.js / R3F |
|---------|:---------:|:------:|:------:|:--------------:|
| سهولة الاستخدام | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐ |
| أداء الموبايل | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| جودة بصرية | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| تحكم كامل بالألوان | ❌ | ✅ | ✅ | ✅ |
| تفاعلية حقيقية | ⭐ | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| وقت التنفيذ | ساعة | يوم | يومان | أسبوع+ |
| مناسب لـ React Native | ✅ | ❌ | ❌ | ✅ (expo-three) |

---

## 🎯 التوصية لمشروع HEQ Werdk تحديداً

### الشاشات البسيطة (Onboarding, Splash):
```
✅ استخدم Glaze PNG → أسرع، أخف، لا مشاكل أداء
```

### شاشة Boss Level (الاختبار النهائي):
```
✅ Glaze PNG مع CSS Animation → تأثير درامي بدون ثقل
```

### لو أردنا تجربة تفاعلية مستقبلاً:
```
✅ Spline → أسهل طريقة للحصول على 3D تفاعلي جميل
```

---

## 🔗 روابط مهمة

| المصدر | الرابط |
|--------|--------|
| Glaze Figma File | https://www.figma.com/design/7XLWhj3b5c0xYByKyDVJNy |
| GRAFIK STASH (مصدر رسمي) | https://grafikstash.com |
| UIBundle (تحميل مجاني) | https://uibundle.com/glaze-3d-icons |
| Three.js | https://threejs.org |
| Three.js مثال مباشر | https://threejs.org/examples |
| React Three Fiber | https://docs.pmnd.rs/react-three-fiber |
| Spline | https://spline.design |
| توثيق Spline + React | https://docs.spline.design/doc/react |
| CSS 3D Transforms (MDN) | https://developer.mozilla.org/en-US/docs/Web/CSS/transform-style |
| Lottie (أنيميشن JSON خفيف) | https://lottiefiles.com |

---

## 💡 نصيحة إضافية: Lottie Files

إذا أردت **أيقونات متحركة** بدون ثقل 3D:

**المصدر:** https://lottiefiles.com
```bash
npm install lottie-react-native
```

```jsx
import LottieView from 'lottie-react-native';

<LottieView
  source={require('./animation.json')}
  autoPlay
  loop
  style={{ width: 200, height: 200 }}
/>
```

- ملفات JSON خفيفة جداً
- آلاف الأنيميشن المجانية
- مثالية لأيقونات التجويد والتعليم

---

*آخر تحديث: سبتمبر 2026 — Open Islamic App Design Team*
