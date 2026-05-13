---
title: CLAUDE.md
tags:
  - file-doc
  - owner/reuven
  - infra/project-root
aliases:
  - CLAUDE.md
status: committed
---

# CLAUDE.md

> [!info] קובץ
> - **נתיב:** `CLAUDE.md` (שורש הפרויקט)
> - **בעלות:** **ראובן** (המנכ"ל)
> - **סוג:** Markdown — הוראות מערכת לפרויקט
> - **מצב גיט:** מקומיט; נטען אוטומטית בכל סשן של Claude Code בפרויקט

## תפקיד
זהו ה"מוח" של ראובן. הקובץ מציג את ראובן בגוף ראשון, מתאר את הפרויקט (מערכת צוות סוכנים ליצירת תוכן), מונה את חברי הצוות (יעל, יובל, חן), ומתאר את מבנה תיקיית `.claude/`. בשלב מאוחר יותר יתווספו כאן הוראות ניתוב מפורטות (מתי להפעיל איזה סוכן) וכללי עבודה אוטומטיים.

## תוכן עיקרי
- הצגה עצמית של ראובן בגוף ראשון
- הצוות: יעל (כותבת), יובל (מעצב תמונות), חן (חוקרת — עדיין לא הוגדרה)
- כל סוכן עם trigger keywords בעברית ובאנגלית + פירוט "מה אין לו"
- סעיף **"תהליך מאמר עם תמונות"** — flow מקצה לקצה (יעל מסמנת placeholders → יובל מפיק תמונות → ראובן ממזג ב-Output/)
- מבנה `.claude/` + תיקיות עבודה בשורש (כולל `yuval/`, `Output/images/`)
- נוהל ה-vault החובה דרך [[skill-obsidian-vault-workflow]]

## קבצים קשורים
- [[file-yael-md]] — sub-agent שראובן מנתב אליו לכתיבה
- [[file-yuval-md]] — sub-agent שראובן מנתב אליו ליצירת תמונות
- [[skill-gpt-image-gen]] — הסקיל שיובל קורא לו (מוזכר ב-CLAUDE.md)
- [[file-gitkeep-agents]] — תיקיית הסוכנים
- [[file-gitkeep-commands]] — מקום עתידי ל-slash commands
- [[file-gitkeep-skills]] — תיקיית הסקילים
- [[file-gitkeep-output-images]] — היעד שראובן מעתיק אליו תמונות במהלך ה-flow
- [[file-settings-local-json]] — הגדרות מקומיות של Claude Code שמשפיעות על אופן הריצה של ראובן
- [[skill-obsidian-vault-workflow]] — הסקיל שמעוגן ב-CLAUDE.md ומחייב את ראובן לקרוא/לכתוב ל-vault סביב כל משימה
- [[project-file-inventory]] — קובץ-הטופיק שמתעד את הסשנים

## Session Log

### 2026-05-13 — הוספת ניתוב יובל + תהליך מאמר עם תמונות [shipped]

- **What was done:**
  - הרחבת שורת יובל מ-stub חד-שורתי ל-Yael-shaped block: קישור ל-[[file-yuval-md|.claude/agents/yuval.md]], קישור לסקיל [[skill-gpt-image-gen]], trigger keywords (עברית + אנגלית), והבהרה של "מה אין לו".
  - הוספת סעיף חדש **"תהליך מאמר עם תמונות"** — 6 שלבים שמגדירים את ה-flow המלא: יעל כותבת `Output/<name>.md` ו-`.html` עם placeholders → ראובן משגר את יובל לכל placeholder → יובל שומר ב-`yuval/outputs/` → ראובן מעתיק ל-`Output/images/` → substitution ליטרלי של ה-placeholders ב-MD ו-HTML → אימות.
  - הרחבת מבנה התיקיות שיכלול את `yuval/reference/`, `yuval/outputs/`, ו-`Output/images/`.
  - עדכון "הערה" — יעל ויובל מוגדרים, חן עוד לא.

- **Decisions:**
  - **גישת merge — Copy to Output/images/** (נבחר אחרי AskUserQuestion). שומר `Output/` self-contained.
  - **Placeholders ב-MD וב-HTML** (לא רק MD + רגנרציה של HTML). פשוט יותר, deterministic.
  - **ראובן הוא ה-merger** — לא יעל ולא יובל. כל אחד נשאר בתחום שלו.

- **Notes / Caveats:**
  - ה-substitution הוא literal string replacement — `{{IMAGE_NEEDED: "..."}}` חייב להיות ייחודי במאמר. אם משתמש כותב את ה-string הזה בתוכן הגלם, יהיה collision.
  - אין מנגנון ל-multiple sizes או quality פר-תמונה כרגע — יובל בוחר defaults (`1024x1024`, `medium`). אפשר להוסיף ל-placeholder spec אם יידרש.

- **Related:** [[file-yuval-md]], [[skill-gpt-image-gen]], [[file-yael-md]], [[file-gitkeep-output-images]], [[file-gitkeep-yuval-outputs]], [[project-file-inventory]]
