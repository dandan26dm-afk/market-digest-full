# Market Digest 📊

תמונת סיכום שוק שנשלחת לדיסקורד בכל יום מסחר בשעה 17:00 שעון ישראל.
הנתונים נלקחים מ-Yahoo Finance ברגע הריצה.

## מבנה הריפו

```
digest.py                            # הנתונים, הטקסט והעיצוב (ה-HTML נמצא בתוך הקובץ)
watchlist.yaml                       # רשימת המניות
requirements.txt
README.md
.github/workflows/market-digest.yml  # התזמון ב-GitHub Actions
```

## הגדרות

- **Secret:** Settings ← Secrets and variables ← Actions ← New repository secret ←
  שם: `DISCORD_WEBHOOK_URL`, ערך: כתובת ה-Webhook של הדיסקורד. הכתובת לא נכנסת לשום קובץ בריפו.
- **הפעלה יומית:** מובנית ב-workflow. GitHub מנסה כמה פעמים בין 17:00 ל-17:45 שעון ישראל,
  וההרצה הראשונה שמצליחה שולחת. השאר מדלגות.
- **מומלץ ריפו פרטי (Private):** בריפו ציבורי GitHub מכבה תזמונים אוטומטית אחרי 60 יום בלי שינויים בריפו.

### גיבוי אופציונלי: cron-job.org

אם GitHub מאחר יותר מדי, אפשר להוסיף טריגר חיצוני. הוא לא יגרום לשליחה כפולה.
cron-job.org שולח בקשת POST לכתובת
`https://api.github.com/repos/USERNAME/REPO/actions/workflows/market-digest.yml/dispatches`
עם Headers: `Authorization: Bearer <token>`, `Accept: application/vnd.github+json` ו-Body: `{"ref":"main"}`.
תזמון: ימים ב'-ו', 17:05, אזור זמן Asia/Jerusalem.

## בדיקה ידנית

Actions ← Market Digest ← Run workflow ← לסמן "להריץ גם מחוץ לשעות" ← Run workflow.
כדי רק לראות את התמונה בלי לשלוח: להוריד את הסימון מ"לשלוח לדיסקורד?". התמונה נשמרת ב-Artifacts של ההרצה.

בדיקה במחשב, בלי אינטרנט: `python digest.py --demo --no-send` (התמונה נשמרת בתיקייה `out/`).

## עריכת הרשימה

כל השינויים נעשים ב-`watchlist.yaml`. הסימולים כמו ב-Yahoo Finance.

## איך התמונה נבנית

- **רקע:** לפי ה-S&P 500. ירוק חזק מ-1%+, ירקרק מ-0.25%+, ניטרלי בין 0.25%- ל-0.25%+, אדמדם עד 1%-, אדום חזק מתחת ל-1%-.
- **באנר VIX:** עד 20: "השוק רגוע יחסית". מעל 20: "Vix > 20 🛒 / סטטיסטיקה לטובתנו 🛒". מעל 30: "Vix > 30 / קנייה🛒🛒🛒 / קנייה גם כשמגעיל".
- **רשימות:** 5 החזקות ו-5 החלשות מתוך watchlist.yaml.

## הערות

- בסופי שבוע ובחגים בבורסה לא נשלח כלום.
- הרצה שמתעכבת מעבר ל-19:30 שעון ישראל לא שולחת תמונה.
- כל מחיר שנכנס לתמונה מודפס ביומן ההרצה (Actions), כדי שאפשר יהיה להשוות מול Yahoo Finance.
