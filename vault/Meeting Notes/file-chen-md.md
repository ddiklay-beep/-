---
title: .claude/agents/chen.md
tags:
  - file-doc
  - owner/chen
  - agent
aliases:
  - chen-agent
  - chen.md
status: committed
---

# .claude/agents/chen.md

> [!info] Sub-agent
> - **נתיב:** `.claude/agents/chen.md`
> - **בעלות:** חן (sub-agent שלישי בפרויקט)
> - **סוג:** Claude Code sub-agent (Markdown עם YAML frontmatter)
> - **מצב גיט:** מקומיט; נטען אוטומטית ע"י Claude Code כשראובן מעריך שהמשימה דורשת מחקר רשת

## תפקיד
חוקרת הרשת של הצוות. מקבלת מראובן בקשת מחקר על נושא, בודקת את [[file-chen-memory-searches|chen/Memory/searches.md]] כדי לראות אם חיפשה דבר דומה ב-30 הימים האחרונים, ואם לא — מחפשת ב-WebSearch, מאחזרת את התוצאות המבטיחות ב-WebFetch, מסננת לפי קריטריונים (מקורות ראשוניים, פרסומים מקצועיים, פרסומים מ-12 חודשים אחרונים), שומרת את המקור הטוב ביותר ל-[[file-gitkeep-content|Content/]] בקובץ `<YYYY-MM-DD>-<slug>.md` עם YAML frontmatter שמתעד את המקור (`source_url`, `source_title`, `source_date`, `fetched_at`, `query`), מוסיפה entry ל-`Memory/searches.md`, ומחזירה לראובן שם קובץ + לינק + סיכום של 1-2 משפטים.

## תוכן עיקרי

**Frontmatter:**
- `name: chen` (kebab-case ASCII — חובה ל-Claude Code)
- `description:` כולל trigger keywords בעברית ובאנגלית, להפעלת auto-delegation ע"י ראובן
- `tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep` — 7 כלים. אין Bash, אין Skill, אין Agent. WebSearch/WebFetch הם הכלים הייחודיים שמבדילים אותה מ-LLM ידע-בלבד.

**Body (system prompt):** הצגה עצמית, תפקיד והערך המוסף ("מידע עכשווי, מקורות אמיתיים, לא הזיות"), טעינת קונטקסט חובה (`Read` + `Grep` של `chen/Memory/searches.md`), הגדרת "נושא דינמי", workflow 8-שלבי (זיכרון → WebSearch → WebFetch → סינון → טיפול בכישלון עד 3 שאילתות → שמירה ל-Content עם frontmatter → לוג ב-Memory → דיווח), קריטריונים למקור איכותי (מקורות ראשוניים/פרסומים מקצועיים מול אגרגטורים/פורומים/clickbait), פורמט entry קבוע ב-`Memory/searches.md`, ומגבלות (לא מייצרת תמונות, לא משכתבת, לא מפעילה סוכנים, לא נוגעת ב-`Output/`/`yael/`/`yuval/`/`vault/`).

## קבצים קשורים
- [[file-claude-md]] — ראובן מנתב משימות מחקר לחן
- [[file-yael-md]] — מקבלת את הקובץ של חן מ-`Content/` כקלט לשכתוב
- [[file-chen-memory-searches]] — לוג החיפושים של חן (cache + audit trail)
- [[file-gitkeep-content]] — יעד הפלט של חן (`Content/<YYYY-MM-DD>-<slug>.md`)
- [[project-file-inventory]] — קובץ-טופיק שבו תועד הסשן הזה

## Open Questions
- חלון 30 יום מקודד-קשיח ב-system prompt של חן. האם להגמיש (parameter בבקשה מראובן)?
- אין עדיין רפרנס לסגנון/אורך מועדף של מאמר ב-`Content/`. כשתצטבר קולקציה — אולי כדאי `chen/reference/` עם דוגמאות "מאמר טוב לתחילת זרימה" (במקביל ל-`yael/reference/`).
- מודל ל-chen נשאר `inherit` (כמו יעל ויובל). WebFetch+סינון איכותי מצדיק `sonnet` או `opus`?
- האם יעל באמת מתעלמת מ-YAML frontmatter? לפי ה-spec שלה היא מתחילה לקרוא מהגוף, אבל לא נבדק end-to-end.
- בדיקת אינטגרציה: שיגור "מצאי מאמר על X" צריך לטריגר את חן בלבד; "מצאי ושכתבי" צריך לעשות chain חן→יעל. עדיין לא נבדק.

## Session Log

### 2026-05-13 — יצירת sub-agent chen (חוקרת הרשת) [shipped]

- **What was done:**
  - יצירת [[file-chen-md|.claude/agents/chen.md]] — sub-agent שלישי בפרויקט. Frontmatter עם `name: chen`, `tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep`, ו-`description` שמכיל trigger keywords בעברית ובאנגלית (חפש/מצא/מחקר vs. search/find/research). Body (system prompt) בעברית: תפקיד והערך-המוסף, טעינת קונטקסט חובה (`Read` + `Grep` של `chen/Memory/searches.md`, חלון 30 יום), הגדרת "נושא דינמי", workflow מלא, קריטריונים למקור איכותי, פורמט entry קבוע ב-Memory, ומגבלות.
  - יצירת תיקיית עבודה [[file-chen-memory-searches|chen/Memory/searches.md]] עם header והפניה לפורמט ב-`chen.md`.
  - יצירת `chen/Memory/.gitkeep` — עקבי עם שאר הפרויקט (placeholder לתיקיות שלא תמיד מלאות).
  - עדכון [[file-claude-md|CLAUDE.md]]: (a) שורת חן הקצרה ("החוקרת. אוספת מידע") הוחלפה בבלוק מלא בסגנון של יעל/יובל עם לינק לקובץ, triggers, ומגבלות; (b) הוספת סעיף חדש "תהליך מחקר → תוכן → תמונות" מעל "תהליך מאמר עם תמונות" שמתאר את הזרימה החדשה (חן → (אופציונלי) יעל → (אופציונלי) יובל) ואת תנאי הסיום (רק חן אם הבקשה הייתה רק מחקר); (c) הוספת `chen/Memory/` למבנה התיקיות והרחבת הסעיף של `Content/` כדי לציין שחן יכולה להניח שם קבצים עם frontmatter; (d) עדכון "הערה" התחתונה מ"חן עדיין לא הוגדרה" ל"שלושת הסוכנים מוגדרים — השלב הבא: slash commands".

- **Decisions:**
  - **7 כלים** (WebSearch, WebFetch, Read, Write, Edit, Glob, Grep) — בלי Bash (אין צורך בקריאות API; WebSearch/WebFetch built-in), בלי Skill (אין סקיל שחן צריכה), בלי Agent (לא מפעילה סוכנים אחרים).
  - **קובץ flat ולא תיקייה** — תואם ל-[[file-yael-md|yael]] ול-[[file-yuval-md|yuval]] ולדוקומנטציה של Claude Code.
  - **`chen/Memory/` ולא `chen/cache/`** — Memory מבטא יותר מ-cache: זה גם audit trail (מה נוסה ונכשל), לא רק החלפה לחיפוש חוזר.
  - **חלון 30 יום קשיח ב-prompt** (לא parameter) — להחלטה פשוטה ועקבית. הפיכת זה לפרמטר תורחב אם תתעורר צורך.
  - **פורמט YAML frontmatter ב-`Content/`** — אושר עם המשתמש (לעומת שורת מקור בלבד). יעל קוראת רק את הגוף, ה-frontmatter קיים לאודיט.
  - **3 ניסיונות לפני failure** — מספר שרירותי שעובד טוב בפועל. גם הכישלון נרשם ב-Memory כדי שחיפוש עתידי באותו נושא לא יחזור על אותן 3 שאילתות.
  - **אוטו-chaining ב-CLAUDE.md** — ההחלטה אם להמשיך מ"חן → יעל → יובל" שייכת לראובן (ה-orchestrator), לא לחן. החוק: triggers של חן בלבד = עוצרים בחן; חן+יעל triggers = chain.

- **Notes / Caveats:**
  - לא בוצע smoke test end-to-end. צריך לשגר "מצאי לי מאמר על Anthropic MCP" בסשן חדש ולוודא: (a) Claude Code מטריגר את חן (לא את יעל), (b) חן עושה Grep ריק על Memory, (c) WebSearch מבוצע בלי prompt הרשאה — אם כן: להוסיף ל-allow list, (d) הקובץ נוצר ב-`Content/` עם frontmatter תקין, (e) entry נוסף ל-`Memory/searches.md`.
  - חן **לא מעדכנת את ה-vault בעצמה** — זה אחריות ראובן, כמו אצל יעל ויובל.
  - שלא כמו יעל/יובל, חן לא קוראת `chen/reference/` בתחילת סשן — אין עדיין תיקייה כזו ולא מובן מה הסטנדרט שצריך לרפרנס. אולי יווצר בעתיד.

- **Related:** [[file-chen-md]], [[file-chen-memory-searches]], [[file-claude-md]], [[file-yael-md]], [[file-yuval-md]], [[file-gitkeep-content]]
