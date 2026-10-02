# Market Digest 📊

תמונת סיכום שוק שנשלחת לדיסקורד בכל יום מסחר, שעה אחרי הפתיחה בוול סטריט (17:30 שעון ישראל).

## מבנה הריפו

```
digest.py
watchlist.yaml
requirements.txt
README.md
templates/digest.html
.github/workflows/market-digest.yml
```

## הגדרות

- **Secret:** Settings ← Secrets and variables ← Actions ← `DISCORD_WEBHOOK_URL` (כתובת ה-Webhook של הדיסקורד).
- **הפעלה יומית:** cron-job.org שולח בקשת POST לכתובת
  `https://api.github.com/repos/USERNAME/REPO/actions/workflows/market-digest.yml/dispatches`
  עם Headers: `Authorization: Bearer <token>`, `Accept: application/vnd.github+json` ו-Body: `{"ref":"main"}`.
  תזמון: ימים ב'-ו', 10:30, אזור זמן America/New_York.

## בדיקה ידנית

Actions ← Market Digest ← Run workflow ← לסמן "להריץ גם מחוץ לשעות" ← Run workflow.

## עריכת הרשימה

כל השינויים נעשים ב-`watchlist.yaml`. הסימולים כמו ב-Yahoo Finance.

## הערות

- בסופי שבוע ובחגים בבורסה לא נשלח כלום.
- הרצה שמתעכבת מעבר ל-19:30 שעון ישראל לא שולחת תמונה.
