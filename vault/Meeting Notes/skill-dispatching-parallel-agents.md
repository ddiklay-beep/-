---
title: skill — dispatching-parallel-agents
tags:
  - skill-doc
  - owner/external
  - source/superpowers
aliases:
  - dispatching-parallel-agents
---

# Skill: dispatching-parallel-agents

> [!info] סקיל מותקן
> - **נתיב:** `.claude/skills/dispatching-parallel-agents/`
> - **מקור:** Superpowers (v5.1.0)
> - **בעלות:** חיצוני

## תפקיד
"Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies."

## מתי להפעיל
כשיש לפחות 2 משימות עצמאיות שאין ביניהן תלות — אפשר להריץ אותן במקביל ע"י Agent calls בו-זמניים. ראובן יכול להפעיל את חן ואת יעל במקביל אם הן עוסקות בנושאים שונים.

## קבצים בתיקייה
- `SKILL.md` — בלבד

## קבצים קשורים
- [[skill-subagent-driven-development]] — תכנון של מי לשגר ולמה
- [[file-claude-md]] — ראובן הוא הדמות שמשגרת את חברי הצוות
- [[file-gitkeep-agents]] — מקום הסוכנים שיוגדרו וישוגרו
