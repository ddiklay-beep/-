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
- [[project-file-inventory]] — קובץ-טופיק שתועד בו הסשן הזה
