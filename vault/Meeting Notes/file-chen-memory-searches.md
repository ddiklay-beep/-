---
title: chen/Memory/searches.md
tags:
  - file-doc
  - owner/chen
  - working-folder
aliases:
  - chen-memory-searches
  - chen-searches-log
status: committed
---

# chen/Memory/searches.md

> [!info] Working file
> - **נתיב:** `chen/Memory/searches.md`
> - **בעלות:** [[file-chen-md|חן]] בלבד
> - **סוג:** Markdown — לוג append-only של חיפושי רשת
> - **מצב גיט:** מקומיט. גודל הקובץ יגדל לאט עם הזמן; זה רצוי (audit trail).

## תפקיד
המקום היחיד שחן בודקת לפני שהיא מחפשת ברשת, וגם המקום היחיד שהיא כותבת אליו אחרי כל חיפוש. הקובץ משרת שתי מטרות:
1. **Cache 30 יום** — חן `Grep`-ית במילות מפתח לפני חיפוש; אם יש hit באותו נושא תוך 30 יום ולא מדובר בנושא דינמי (חדשות / מחירים / השקות) → היא לא מבזבזת WebSearch.
2. **Audit trail** — כל חיפוש שנעשה, כולל שאילתות שכושלו, רשום עם תאריך, מקורות שהושוו, ודירוג כוכבים. מאפשר חזרה למקור קודם, ניתוח מאקרו של איכות מקורות, וזיהוי דפוסי חיפוש שלא עבדו.

## תוכן עיקרי

הקובץ נפתח עם header קצר והפניה לפורמט המלא ב-[[file-chen-md|.claude/agents/chen.md]]. אחרי ה-`---` הראשון, חן מוסיפה entries בפורמט קבוע:

```markdown
## YYYY-MM-DD HH:MM | <נושא החיפוש>
**מילות מפתח:** keyword1, keyword2
**שאילתות שנעשו:** "query 1", "query 2"
**מקורות שנמצאו:**
- [כותרת](URL) - איכות: ⭐⭐⭐⭐ - <הערה>
- [כותרת](URL) - איכות: ⭐⭐⭐ - <הערה>
**נבחר:** <המקור הנבחר ולמה>
**קובץ ב-Content:** <filename>.md
---
```

**Failure entries** (3 ניסיונות בלי תוצאה) רשומים באותו פורמט אבל `נבחר:` ⛔ failed, `קובץ ב-Content:` —. חשוב לא פחות מהצלחות: מונע מחן לחזור על אותן 3 שאילתות בנושא דומה.

## קבצים קשורים
- [[file-chen-md]] — חן עצמה (מגדירה את הפורמט)
- [[file-gitkeep-content]] — היעד של חן ב-`Content/<YYYY-MM-DD>-<slug>.md`
- [[file-claude-md]] — ראובן הוא זה שמשגר את חן

## Open Questions
- חלון 30 יום קשיח ב-prompt. אם יצטבר ניסיון שזה לא הגיוני (למשל ברפרנסים evergreen — סביר ל-90 יום) — להגמיש.
- האם לפצל את הקובץ לפי שנה ("searches-2026.md") כשיגיע לאלפי שורות? לדחות עד שיהיה רלוונטי.
- האם יעל / יובל יקראו את הקובץ הזה? לפי ה-spec — לא. הוא של חן בלבד.

## Session Log

### 2026-05-13 — יצירת הקובץ עם header בלבד [shipped]

- **What was done:**
  - יצירת `chen/Memory/searches.md` עם header של "Searches Log — חן" והפניה לפורמט ב-`chen.md`. הקובץ עדיין ריק מ-entries (חן לא הופעלה עדיין).
  - יצירת `chen/Memory/.gitkeep` — placeholder עקבי עם שאר תיקיות העבודה בפרויקט.

- **Decisions:**
  - **תיקיית `Memory/` תחת `chen/`** — מקבילה ל-`yael/reference/`, `yuval/reference/`, `yuval/outputs/`. שמירה על דפוס "כל סוכן עם תיקייה משלו בשורש".
  - **שם `Memory/` ולא `cache/` ולא `logs/`** — מבטא גם cache (חיפוש מהיר) וגם audit trail (היסטוריה לטווח ארוך).

- **Notes / Caveats:**
  - הקובץ ריק כרגע; ה-entry הראשון ייווצר ע"י חן בשיגור הראשון שלה.

- **Related:** [[file-chen-md]], [[file-gitkeep-content]], [[file-claude-md]]
