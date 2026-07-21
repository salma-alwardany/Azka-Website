# موقع Azka — دليل النشر على هوستنجر

موقع ثابت (HTML / CSS / JavaScript) بيتنشر على استضافة هوستنجر عن طريق الربط التلقائي مع GitHub.

---

## آلية العمل

أي تعديل بيترفع على فرع `main` في GitHub، بيشتغل GitHub Actions تلقائي ويرفع الملفات على هوستنجر عن طريق الـ FTP جوه مجلد `public_html`.

```
تعديل على الكود  →  git push  →  GitHub Actions  →  FTP  →  public_html على هوستنجر  →  الموقع اتحدّث
```

---

## خطوات الإعداد لمرة واحدة

### خطوة 1 — ارفعي ملفات الموقع على الريبو

من جهازك، جوه مجلد `D:/Azka`:

```bash
cd D:/Azka
git init
git remote add origin https://github.com/salma-alwardany/Azka-Website.git
git add .
git commit -m "أول رفع لملفات الموقع"
git branch -M main
git push -u origin main
```

> أو بدون سطر أوامر: من صفحة الريبو على GitHub اضغطي **Add file → Upload files** واسحبي كل محتويات مجلد `D:/Azka` جوه، وبعدين **Commit changes**.

### خطوة 2 — هاتي بيانات الـ FTP من هوستنجر

من **hPanel → Files → FTP Accounts**، هتلاقي:

- **FTP hostname / server** (مثال: `ftp.your-domain.com` أو IP)
- **FTP username**
- **FTP password** (لو نسيتيه، اعملي Reset من نفس الصفحة)

### خطوة 3 — حطي البيانات دي كـ Secrets في GitHub

من صفحة الريبو على GitHub:
**Settings → Secrets and variables → Actions → New repository secret**

وضيفي التلات أسرار دول (بنفس الأسماء بالظبط):

| اسم السر (Name) | القيمة (Value) |
|---|---|
| `FTP_SERVER` | عنوان السيرفر بتاع الـ FTP |
| `FTP_USERNAME` | اسم مستخدم الـ FTP |
| `FTP_PASSWORD` | باسورد الـ FTP |

### خطوة 4 — خلاص!

من دلوقتي، أي مرة تعملي `git push` على فرع `main`، الموقع هينشر تلقائي على هوستنجر.
تقدري كمان تشغّلي النشر يدوي من تبويب **Actions** في الريبو (زرار **Run workflow**).

---

## هيكل المشروع

```
Azka-Website/
├── index.html          ← الصفحة الرئيسية (لازم تكون موجودة)
├── ...                 ← باقي ملفات الموقع (CSS / JS / صور)
├── README.md           ← الملف ده (مش بيتنشر على السيرفر)
└── .github/workflows/
    └── deploy.yml      ← إعداد النشر التلقائي
```
