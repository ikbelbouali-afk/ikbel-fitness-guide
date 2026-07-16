# Ikbel Fitness Guide — موقع معلومات عامة عالفتنس

موقع ستاتيك (HTML/CSS بلا build، بلا Node) فيه معلومات عامة عالفتنس، مبني بنفس هوية
**Ikbel Coaching** (خلفية سوداء `#050505` + سماوي `#21CFFF` + ذهبي `#EFBF04`، خط IBM Plex Sans Arabic، RTL تونسي).

هدفه تثقيفي — يعرّف الناس بالأساسيات، و يوجّههم للكوتشينغ الشخصي مع الكوتش إقبال في الأخير.

## المحتوى (أقسام الصفحة)

Header → Hero → التغذية (سعرات/بروتين/كارب-دهون/ماء) → التدريب (حمل متدرّج/مركّبة/فورم/تنظيم)
→ الراحة و الاستشفاء (نوم/راحة/ضغط) → المكمّلات (واي/كرياتين/كافيين/D-أوميغا3) →
أخطاء شائعة → أرقام + فلسفة "STIMULATE, DON'T ANNIHILATE" → CTA للكوتشينغ + إخلاء مسؤولية → فوتر.

كل شي في `index.html` وحيد (CSS inline). الخطوط من Google Fonts CDN.

## التشغيل محليًا

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File serve.ps1 -Port 8140
# http://localhost:8140 — أو preview config "fitness" من Claude Code
```

## البنية

```
ikbel-fitness-guide/
├─ index.html   ← الصفحة الكاملة (SEO + OG + كل الأقسام + CSS inline)
├─ serve.ps1    ← سيرفر ستاتيك محلي (بورت 8140، SendChunked)
└─ .claude/launch.json  ← preview config "fitness"
```

## ملاحظات

- `serve.ps1` لازمو `SendChunked = $true` (موجود) — ما تنحّيهاش.
- زر "الكوتشينغ الشخصي" و CTA النهائي يوجّهو لـ `https://ikbel123.netlify.app/`.
- المحتوى **معلومات عامة**، فيه إخلاء مسؤولية طبي — راجعو قبل أي نشر رسمي.
- يحترم `prefers-reduced-motion`، mobile-first، RTL عربي تونسي.
