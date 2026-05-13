---
title: skill — subagent-driven-development
tags:
  - skill-doc
  - owner/external
  - source/superpowers
aliases:
  - subagent-driven-development
---

# Skill: subagent-driven-development

> [!info] סקיל מותקן
> - **נתיב:** `.claude/skills/subagent-driven-development/`
> - **מקור:** Superpowers (v5.1.0)
> - **בעלות:** חיצוני

## תפקיד
"Use when executing implementation plans with independent tasks in the current session."

## מתי להפעיל
כשיש תוכנית עם משימות עצמאיות שכדאי להריץ אותן דרך sub-agents בתוך הסשן הנוכחי. רלוונטי במיוחד לראובן כשהוא מנתב משימה ל-יעל/יובל/חן.

## קבצים בתיקייה
- `SKILL.md`
- `implementer-prompt.md` — פרומפט ל-sub-agent מבצע
- `code-quality-reviewer-prompt.md` — פרומפט ל-sub-agent בודק איכות
- `spec-reviewer-prompt.md` — פרומפט ל-sub-agent בודק ספק

## קבצים קשורים
- [[skill-dispatching-parallel-agents]] — להפעלה במקביל של מספר sub-agents
- [[skill-executing-plans]] — לרוב משלבים את שניהם
- [[file-claude-md]] — ראובן הוא ה"orchestrator" של ה-sub-agents בפרויקט
- [[file-gitkeep-agents]] — מקום הסוכנים שייווצרו
