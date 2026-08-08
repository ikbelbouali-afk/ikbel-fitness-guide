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

## آلة حاسبة السعرات

قسم `#calc` — vanilla JS، بلا مكتبات:

- **BMR** بمعادلة Mifflin-St Jeor: `10×كغ + 6.25×سم − 5×سنة + (5 راجل / −161 مرا)`
- **TDEE** = BMR × معامل النشاط (1.2 → 1.9)
- **الهدف**: تنشيف `−500` · ثبات `0` · تضخيم `+300` سعرة
- **البروتين**: 1.6–2.2غ لكل كغ من وزن الجسم

النتيجة مقرّبة لأقرب 10 سعرات. التعديل في الـ `<script>` في آخر `index.html` (كائن `GOALS`).

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
