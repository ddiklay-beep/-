---
title: skill — obsidian-vault-workflow
tags:
  - skill-doc
  - owner/external
  - source/obsidian-skills
  - meta-skill
  - mandatory
aliases:
  - obsidian-vault-workflow
---

# Skill: obsidian-vault-workflow

> [!important] סקיל חובה
> - **נתיב:** `.claude/skills/obsidian-vault-workflow/`
> - **מקור:** obsidian-skills (חיצוני)
> - **בעלות:** חיצוני
> - **סטטוס:** **חובה לכל משימה** — מעוגן ב-CLAUDE.md

## תפקיד
"Enforce the mandatory Obsidian vault read/write protocol for this project. Use at the START of every task (to locate the topic file, read its Overview + Session Log, plus recent Meeting Notes / Content Briefs / Brand Guidelines) and at the END of every task (to append a dated compact summary to the topic file and update the Overview if scope changed)."

## מתי להפעיל
**כל משימה.** קוד, תוכן, ארכיטקטורה, UI, באגים, ביקורות, refactors. רק שאלות read-only טהורות פטורות.

## הזרימה
1. **Phase 1 — לפני המשימה:** איתור קובץ-הטופיק, קריאתו (Overview + Session Log + Open Questions), קריאת 2-3 Meeting Notes אחרונים, סריקת Content Briefs ו-Brand Guidelines.
2. **Phase 2 — אחרי המשימה:** עדכון Overview אם השתנה ה-scope, עדכון Open Questions, צירוף `### YYYY-MM-DD — title [status]` לתחתית ה-Session Log עם `[[wikilinks]]`, ואימות ה-write בקריאה חוזרת.

## קבצים בתיקייה
- `SKILL.md` — מסמך 228 שורות עם פרוטוקול מלא, אנטי-פטרנים, וצ'קליסט

## מבנה תיקיות שהסקיל דורש
- `vault/Meeting Notes/`, `vault/Content Briefs/`, `vault/Publishing Log/`, `vault/Brand Guidelines/`
- בכל תיקייה: `_index.md` + topic-files

## Status tags לסשן
`[shipped]`, `[spiked]`, `[wip]`, `[reverted]`, `[planned]`, `[debug]`

## קבצים קשורים
- [[skill-obsidian-markdown]] — התחביר שבו נכתבים הקבצים
- [[skill-obsidian-bases]] — תצוגות מתקדמות מעל ה-vault
- [[skill-using-superpowers]] — מטא-סקיל-אח, גם הוא לטעינה בכל סשן
- [[file-claude-md]] — מקום העגינה של חובת ההפעלה
- [[project-file-inventory]] — הקובץ הזה הופעל לראשונה בסשן 2026-05-13
