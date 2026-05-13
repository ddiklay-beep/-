---
title: gpt-image-gen (skill)
tags:
  - skill-doc
  - skill-type/project-local
  - owner/yuval
aliases:
  - gpt-image-gen
  - skill-gpt-image-gen
status: committed
---

# gpt-image-gen (skill)

> [!info] סקיל
> - **נתיב:** `.claude/skills/gpt-image-gen/SKILL.md`
> - **סוג:** סקיל פרויקט-מקומי (לא Superpowers, לא obsidian)
> - **משתמש עיקרי:** [[file-yuval-md|יובל]]
> - **מצב גיט:** מקומיט

## תפקיד
מעטפת קריאה ל-OpenAI Images API. מקבל `prompt` ו-`output` (נתיב יעד) וכותב קובץ PNG. שני מסלולים: `curl + jq` (כשיש jq) או python stdlib fallback (Git Bash on Windows, רוב הזמן בלי jq). **המודל קבוע: `gpt-image-2`** — לא להחליף.

## תוכן עיקרי

- **Frontmatter:** `name: gpt-image-gen`, `description` תיאור קצר שמטריגר auto-delegation כשסוכן צריך לייצר תמונה (בעיקר יובל).
- **Body:** אזהרה גדולה על קביעות שם המודל, רשימת קלטים (prompt/output חובה, size/quality אופציונליים), הסבר טעינת `OPENAI_API_KEY` מ-`.env` ע"י הקורא, שתי שיטות (A: curl+jq, B: python stdlib), טיפול בשגיאות בלי retry, אימות `-s` על הקובץ.

**מודל — חשוב:**
- `gpt-image-2` יצא ב-2026-04-21.
- ייתכן שמודל לא נכנס לידע פנימי ישן יותר; **זה לא אומר שהוא לא קיים**.
- אם הקריאה נכשלת — הבעיה ב-API key/parameters, לא בשם המודל.

## קבצים קשורים
- [[file-yuval-md]] — הצרכן העיקרי של הסקיל
- [[file-env]] — מקור `OPENAI_API_KEY`
- [[file-env-example]] — תבנית `.env` (כולל הערה על המפתח)
- [[file-gitignore]] — `yuval/outputs/*.png` ו-`Output/images/*.png` נכנסו לכאן בגלל הסקיל הזה
- [[file-claude-md]] — מתאר את התהליך המלא של מאמר עם תמונות (יעל → יובל → ראובן ממזג)
- [[skill-writing-skills]] — קונבנציות לכתיבת skills

## Open Questions
- מה לעשות אם הקריאה ל-`gpt-image-2` תיכשל עם content-policy על כל prompts באנגלית פשוטה? כרגע ההנחיה היא "לא retry, להעביר את ה-JSON של השגיאה לראובן". אם זה יהפוך לתבנית, להוסיף flowchart לפי קוד שגיאה ב-SKILL.
- האם להוסיף תמיכה בפרמטרים נוספים של API (background, response_format, n>1)?
- אם נחליט לכתוב את ה-Bash logic בקובץ `gpt-image-gen/generate.sh` (script מצורף לסקיל) במקום inside the SKILL.md — סוכנים אחרים יוכלו להשתמש בו ישר. נשקול אם יידרשו צרכנים נוספים מעבר ליובל.

## Session Log

### 2026-05-13 — יצירת סקיל gpt-image-gen [shipped]

- **What was done:**
  - יצירת `.claude/skills/gpt-image-gen/SKILL.md` עם frontmatter מינימלי (`name`, `description`) ו-body מקיף בעברית: אזהרה על קביעות המודל, טבלת קלטים, הוראות טעינת ה-key, שתי שיטות לקריאה ל-API (curl+jq ו-python stdlib), טיפול בשגיאות, ואימות הקובץ.
  - הוספת `OPENAI_API_KEY=` ל-[[file-env-example|.env.example]] עם הערה בעברית. ב-[[file-env|.env]] המקומי המפתח כבר קיים.
  - עדכון [[file-gitignore]] שיכלול `yuval/outputs/*.png` ו-`Output/images/*.png` (לא לבלוט את הגיט עם PNGs; ה-`.txt` של ה-prompts וה-`.gitkeep` כן בגיט).

- **Decisions:**
  - **שם הסקיל `gpt-image-gen`** (לא `image-gen` כללי) — מסמן במפורש שהמודל הוא של OpenAI ושיכולת הסקיל מצומצמת ל-API הזה.
  - **שתי שיטות (A/B) ב-SKILL במקום script מצורף:** קל יותר לקריאה ולתיקון, ויובל יבחר בשיטה B (python) ב-Windows.
  - **לא retry על שגיאות** — content-policy ו-billing/key לא נפתרים בניסיון נוסף; חבל לבזבז quota.
  - **המודל `gpt-image-2` קבוע ולא קונפיגורבילי.** המשתמש ביקש זאת מפורשות (יצא 2026-04-21, ייתכן שלא בידע פנימי ישן).
  - **השמירה של ה-prompt לצד ה-PNG** הוגדרה כאחריות הקורא (יובל), לא של הסקיל עצמו — הסקיל הוא thin wrapper סביב ה-API.

- **Notes / Caveats:**
  - שיטה A (jq) בפועל לא בטוחה ב-Git Bash on Windows — ב-environments ב-Windows אין jq מותקן כברירת מחדל. שיטה B (python stdlib) היא המומלצת בפועל; שיטה A נשארה לתיעוד וכ-fallback ב-environments עם jq.
  - הסקיל לא נבדק end-to-end (אין חיוב לבדוק עכשיו) — verification דורש `OPENAI_API_KEY` תקין + תקציב פעיל ב-OpenAI.

- **Related:** [[file-yuval-md]], [[file-env]], [[file-env-example]], [[file-gitignore]], [[file-claude-md]]
