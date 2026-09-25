# Ikbel Fitness Guide — موقع معلومات عامة عالفتنس

موقع ستاتيك (HTML/CSS بلا build، بلا Node) فيه معلومات عامة عالفتنس، مبني بنفس هوية
**Ikbel Coaching** (خلفية سوداء `#050505` + سماوي `#21CFFF` + ذهبي `#EFBF04`، خط IBM Plex Sans Arabic، RTL تونسي).

هدفه تثقيفي — يعرّف الناس بالأساسيات، و يوجّههم للكوتشينغ الشخصي مع الكوتش إقبال في الأخير.

## المحتوى (أقسام الصفحة)

Header → Hero → التغذية (سعرات/بروتين/كارب-دهون/ماء) → التدريب (حمل متدرّج/مركّبة/فورم/تنظيم)
→ الراحة و الاستشفاء (نوم/راحة/ضغط) → المكمّلات (واي/كرياتين/كافيين/D-أوميغا3) →
أخطاء شائعة → أرقام + فلسفة "STIMULATE, DON'T ANNIHILATE" → **آلة حاسبة السعرات** →
CTA للكوتشينغ + إخلاء مسؤولية → فوتر.

كل شي في `index.html` وحيد (CSS + JS inline). الخطوط من Google Fonts CDN.

## منتجات TREC (كود IKBEL −20٪)

قسم `#trec` بعد المكمّلات: 6 منتجات من https://trectunisie.com (Whey، Creatine، Boogieman،
Omega 3 + D3، Oat Gainer، Multivitamin) + صندوق كود مع زر نسخ. زادة رابط في الـ Hero،
رابط تحت قسم المكمّلات، و nudge تحت نتيجة الآلة الحاسبة (Whey للتنشيف/الثبات، Gainer للتضخيم).

- **البيانات:** مصفوفة `TREC` في الـ `<script>` (handle، اسم، وصف، طريقة الاستعمال، سوم احتياطي).
- **السوم و المخزون live:** كل زيارة تقرا `trectunisie.com/products/<handle>.js`
  (Shopify يسمح بالـ CORS). كان فشل، يبقى السوم الاحتياطي. كان المنتج نفذ كامل، البطاقة تولّي «نفذ مؤقتًا».
- **الصور:** مباشرة من `cdn.shopify.com` بـ `&width=500` — ما فماش صور في الـ repo.
- **زر الشراء:** `trectunisie.com/discount/IKBEL?redirect=/products/<handle>` — يحطّ الكود أوتوماتيك.
  الروابط `rel="sponsored"`.
- **باش تزيد منتج:** زيد object في `TREC` بالـ handle متاعو (آخر جزء من رابط المنتج).
- ⚠️ صلاحية الكود ما تتأكّدتش من صفحة الدفع — Shopify يقبل أي كود في الرابط.

## آلة حاسبة السعرات

قسم `#calc` — vanilla JS، بلا مكتبات:

- **BMR** بمعادلة Mifflin-St Jeor: `10×كغ + 6.25×سم − 5×سنة + (5 راجل / −161 مرا)`
- **TDEE** = BMR × معامل النشاط (1.2 → 1.9)
- **الهدف**: تنشيف `−500` · ثبات `0` · تضخيم `+300` سعرة
- **الماكرو**: بروتين 1.9غ/كغ · دهون 25٪ من السعرات · كربوهيدرات = الباقي

النتيجة مقرّبة لأقرب 10 سعرات. التعديل في الـ `<script>` في آخر `index.html` (كائن `GOALS`).

### حدّين مهمّين في الحساب (ما تنحّيهمش)

1. **سقف البروتين عند 35٪ من السعرات.** البروتين محسوب على الوزن الكلّي، فالناس
   الثقال وقت التنشيف كان يوكل الميزانية كامل و يخلّي الكربوهيدرات شبه صفر
   (مثال: مرا 110كغ → 23غ كارب قبل الإصلاح، ولّات 153غ بعدو).
2. **أرضية سعرات آمنة: 1500 راجل / 1200 مرا.** كان العجز ينزل تحتها، الآلة ترفّع
   و تبيّن تحذير. بلاش هالحد، حالات كيف مرا 45كغ قليلة الحركة تطلع بـ ~610 سعرة/يوم.

الدهون عندها أرضية 40غ (دهون أساسية/هرمونات).

## التشغيل محليًا

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File serve.ps1 -Port 8140
# http://localhost:8140 — أو preview config "fitness" من Claude Code
```

## البنية

```
ikbel-fitness-guide/
├─ index.html   ← الصفحة الكاملة (SEO + OG + كل الأقسام + CSS/JS inline)
├─ serve.ps1    ← سيرفر ستاتيك محلي (بورت 8140، SendChunked)
└─ .claude/launch.json  ← preview config "fitness"
```

## النشر

الـ remote محضّر مسبقًا على `https://github.com/ikbelonline/ikbel-fitness-guide.git`
و الفرع `main` (كيف بقية المشاريع). باش تنشر أول مرّة:

1. اعمل repo فارغ باسم `ikbel-fitness-guide` من https://github.com/new
   (**بلا** README/gitignore/license).
2. بعدها:

```powershell
git push -u origin main
```

3. في Netlify: **Add new site → Import from Git** → اختار الـ repo.
   بلا build command، و publish directory = `/` (موقع ستاتيك). بعدها كل `git push` ينشر تلقائيًا.

## ملاحظات

- `serve.ps1` لازمو `SendChunked = $true` (موجود) — ما تنحّيهاش.
- زر "الكوتشينغ الشخصي" و CTA النهائي يوجّهو لـ `https://ikbel123.netlify.app/`.
- المحتوى **معلومات عامة**، فيه إخلاء مسؤولية طبي — راجعو قبل أي نشر رسمي.
- يحترم `prefers-reduced-motion`، mobile-first، RTL عربي تونسي.
