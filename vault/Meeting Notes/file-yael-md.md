---
title: .claude/agents/yael.md
tags:
  - file-doc
  - owner/yael
  - agent
aliases:
  - yael-agent
  - yael.md
status: committed
---

# .claude/agents/yael.md

> [!info] Sub-agent
> - **נתיב:** `.claude/agents/yael.md`
> - **בעלות:** יעל (sub-agent ראשון בפרויקט)
> - **סוג:** Claude Code sub-agent (Markdown עם YAML frontmatter)
> - **מצב גיט:** מקומיט; נטען אוטומטית ע"י Claude Code כשראובן מעריך שהמשימה מתאימה ליעל

## תפקיד
הסוכן הראשון ב-`.claude/agents/`. אחראי על שכתוב/עריכה/תרגום/סיכום של תוכן: לוקחת מאמר גלם מ-`Content/`, מיישמת `yael/style-guide.md` ואת הדוגמאות מ-`yael/reference/`, ושומרת תוצרים ב-`Output/` בשתי גרסאות (`.md` + `.html` עצמאי עם CSS משובץ).

## תוכן עיקרי

**Frontmatter:**
- `name: yael` (kebab-case ASCII — חובה ל-Claude Code)
- `description:` כולל את כל trigger keywords בעברית ובאנגלית, להפעלה אוטומטית של auto-delegation ע"י ראובן
- `tools: Read, Write, Edit, Glob, Grep` — בדיוק 5 כלים, ללא Bash/WebFetch/Skill/Agent

**Body (system prompt):** הצגה עצמית, תפקיד, טעינת קונטקסט חובה בתחילת סשן, workflow 5-שלבי, פורמט HTML ידני (אין converter), כללי כתיבה (לא להוסיף קישורים/CTAs של המחבר המקורי; מותגים בסיפור נשארים), ומה היא לא יכולה לעשות.

## קבצים קשורים
- [[file-claude-md]] — ראובן המנכ"ל הוא זה שמנתב משימות אל יעל
- [[file-gitkeep-agents]] — placeholder של תיקיית הסוכנים שעדיין שם (טכנית מיותר עכשיו)
- [[file-gitkeep-content]] — מקור הקלט של יעל
- [[file-gitkeep-output]] — יעד הפלט של יעל
- [[file-gitkeep-yael-reference]] — דוגמאות סגנון שיעל קוראת בתחילת סשן
- [[skill-writing-skills]] — קונבנציות לכתיבת system prompts יעילים לסוכנים
- [[skill-obsidian-markdown]] — לא בשימוש ע"י יעל עצמה (אין לה Skill tool), אבל רלוונטי לאופן שהמסמך הזה נכתב
- [[file-yuval-md]] — sub-agent שמקבל את ה-placeholders שיעל מסמנת (יוצר את התמונות בפועל)
- [[skill-gpt-image-gen]] — הסקיל שיובל מפעיל אחרי שיעל מסמנת מקומות לתמונות
- [[project-file-inventory]] — קובץ-טופיק שתועד בו הסשן הזה

## Session Log

### 2026-05-13 — יעל מסמנת placeholders לתמונות [shipped]

- **What was done:**
  - הוספת שלב 4 ל-Workflow ב-`.claude/agents/yael.md`: "זיהוי מקומות לתמונות (image placeholders)". בכל מקום שראוי לתמונה, יעל מכניסה placeholder באותו מיקום ב-MD וב-HTML:
    ```
    {{IMAGE_NEEDED: "תיאור מפורט של התמונה, כולל סגנון רצוי ליובל"}}
    ```
  - עדכון שלב הדיווח: בנוסף לסיכום הרגיל, יעל מצרפת בלוק `## Image placeholders` עם רשימה של כל placeholder שהשאירה (מיקום + תיאור). אם אין — מציינת במפורש "No images needed for this piece."
  - עדכון ה-`description` ב-frontmatter שמזכיר את האחריות החדשה (אבל לא משנה את הכלים — יעל עדיין `Read, Write, Edit, Glob, Grep`, היא לא יוצרת תמונות).

- **Decisions:**
  - **התיאור ב-placeholder חייב להיות עצמאי** — יובל קורא אותו בלי ההקשר של המאמר. כולל subject, mood, palette hints, composition, exclusions.
  - **Placeholder זהה ב-MD וב-HTML** — באותו מיקום בדיוק. ראובן עושה אחר כך literal string replacement בשני הקבצים.
  - **לא לכלול תמונה אם לא צריך** — יעל יכולה (וצריכה) להחזיר "No images needed for this piece." אם המאמר טקסטואלי טהור.

- **Notes / Caveats:**
  - יעל **לא קוראת ליובל ישירות** — אין לה Skill או Agent. היא משאירה placeholders ומדווחת לראובן; ראובן הוא זה שמשגר את יובל.
  - אם המקור הגולמי במקרה מכיל את המחרוזת `{{IMAGE_NEEDED:` — collision. כדאי לבדוק בעת ביקורת איכות.

- **Related:** [[file-yael-md]], [[file-yuval-md]], [[skill-gpt-image-gen]], [[file-claude-md]], [[file-gitkeep-output-images]]
