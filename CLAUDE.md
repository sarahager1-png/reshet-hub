# CLAUDE.md — מרכז המערכות · רשת אהלי יוסף יצחק (רשת חינוך חב"ד)

This file provides guidance to Claude Code when working with this repository.


> **עדכון 21/9/2026:** `index.html` הוא עכשיו אותו דף בדיוק כמו **https://reshet-maarachot.surge.sh** ("מרכז המערכות" — 31 מערכות חיות, כרטיס + QR להתקנה, סינון וחיפוש, כרטיסים סטטיים ב-HTML ולא מערך JS). מעדכנים את שניהם יחד: מוסיפים כרטיס, מעדכנים את המונה, דוחפים לכאן וגם `surge ./deploy reshet-maarachot.surge.sh`. תיאורי המבנה הישנים למטה (מערך systems, אימוג'י) כבר לא תקפים.

## Commands

אין build, אין npm. הריפו כולו = `index.html` אחד (standalone) + `logo`-less.

```bash
cmd /c start "" "C:\tmp\work\reshet-hub\index.html"
```

## Deploy

- **URL:** `https://sarahager1-png.github.io/reshet-hub/`
- **Platform:** GitHub Pages — repo `sarahager1-png/reshet-hub`, **branch `main`, path `/`** (legacy build)
- כל push ל-`main` מתפרסם אוטומטית. commit כ-`sarahager1@gmail.com`.

## Environment variables

אין. דף סטטי ציבורי, בלי סודות ובלי API.

## Stack

HTML + CSS + Vanilla JS בקובץ אחד. CDN חיצוני: Google Fonts בלבד (Heebo + Rubik).

## Brand

```
--purple:      #4B2E83   /* ראשי */
--purple-deep: #341A66
--violet:      #7B2ED6   /* גרדיאנט אריח + כותרות */
--teal:        #00B4CC   /* אקסנט */
--teal-2:      #38BDF8
--ink:         #1A0B35   --ink-2: #4a4060   --ink-3: #8b82a3
--line:        #e9e4f3   --bg:    #f6f3fc
```

- `dir="rtl"`, כותרות Rubik italic 900, גוף Heebo.
- רקע ambient: שני radial-gradients + נקודות (`body::before` / `body::after`).
- כרטיסים: זכוכית (`rgba(255,255,255,.82)` + `backdrop-filter: blur(8px)`), רדיוס 22px, פס גרדיאנט עליון.
- **ב״ה** ימין-למעלה (`.bh`), ושורת הקרדיט בפוטר: `בנוי ופיתוח: שרה הגר · 0503339770 · יעוץ ארגוני | פתרונות דיגיטליים · מהבנת הארגון לפתרון שעובד.`

## Architecture

כל תוכן הדף נבנה מ-JS בתחתית `index.html`:

| מערך | תפקיד |
|------|-------|
| `LIVE` | מערכות פעילות — `{ icon, teal, name, desc, url }` → `liveCard()` → `#liveGrid` |
| `DEV`  | מערכות בפיתוח — `{ icon, name, desc }` (בלי URL) → `devCard()` → `#devGrid` |

הספירות ב-`#liveCount` / `#devCount` מחושבות מאורך המערכים — **לעדכן רק את המערכים**, לא את הספירות.

**להוספת מערכת:** להוסיף אובייקט למערך המתאים. מעבר מפיתוח→פעיל = להעביר בין המערכים ולהוסיף `url` + `teal`.

## reshet-showcase — קשור אך נפרד

`C:\tmp\work\reshet-showcase` הוא **דף תצוגה/שיווק בלבד** ("רשת חינוך חב״ד · מערכות חכמות") —
`index.html` עצמאי המציג את ~25 המערכות ב-6 אשכולות תמטיים, עם צילומי מסך (`preview-*.png`, `v2/v3/v4-*.png`).
**אין בו git, אין לו remote ואין לו דיפלוי מהתיקייה הזו.** הוא לא מקור התוכן של reshet-hub —
אין בו קישורים למערכות, ואין סנכרון בין השניים. אם מוסיפים מערכת לאחד, זה לא מתעדכן בשני.
**אין לכתוב לו CLAUDE.md נפרד.**

## Gotchas

- **הקישורים כאן משוכפלים ידנית** מכל מערכת. כשכתובת מערכת משתנה — לעדכן גם כאן.
  ה-URLs הרשומים כרגע: hamidrasha (Vercel preview-style URL), chagim-venehenim, atudot-lachinuch.co.il,
  giuus, chabadsummer.co.il, school-schedule-teal, trip-consent, gan-madrichot.surge.sh.
- **קיים דף "מרכז מערכות" נוסף ב-`https://reshet-maarachot.surge.sh`** (17 מערכות + QR להתקנה בנייד),
  שנבנה מקובץ standalone אחר ולא מהריפו הזה. שני הדפים חיים במקביל — לברר עם שרה איזה מהם היא משתפת
  לפני שמשקיעים בעדכון. *(לא מאומת שהם אמורים להתמזג.)*
- `</style>` חסר בקובץ standalone = דף לבן חי. לרנדר מקומית לפני push
  (ראה זיכרון `headless-edge-blank-standalone-html`).
- הקובץ מכיל עברית — לערוך עם Edit, לא דרך bash heredoc (`bash-hebrew-literal-corruption`).
