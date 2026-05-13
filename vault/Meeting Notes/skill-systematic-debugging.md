---
title: skill — systematic-debugging
tags:
  - skill-doc
  - owner/external
  - source/superpowers
aliases:
  - systematic-debugging
---

# Skill: systematic-debugging

> [!info] סקיל מותקן
> - **נתיב:** `.claude/skills/systematic-debugging/`
> - **מקור:** Superpowers (v5.1.0)
> - **בעלות:** חיצוני

## תפקיד
"Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes."

## מתי להפעיל
**לפני** הצעת תיקון לבאג/בדיקה שנכשלה/התנהגות לא צפויה. לא לקפוץ לפתרון.

## קבצים בתיקייה
- `SKILL.md` — ההגדרה הראשית
- `condition-based-waiting.md` + `condition-based-waiting-example.ts` — הימנעות מ-sleep ב-tests
- `defense-in-depth.md` — ריבוי שכבות הגנה
- `root-cause-tracing.md` — טכניקות איתור שורש
- `find-polluter.sh` — סקריפט לאיתור test polluter
- `test-academic.md`, `test-pressure-1.md`, `test-pressure-2.md`, `test-pressure-3.md` — דוגמאות tests
- `CREATION-LOG.md` — היסטוריית יצירת הסקיל

## קבצים קשורים
- [[skill-test-driven-development]] — דיבוג מתחיל בלכתוב טסט שמשחזר את הבעיה
- [[skill-receiving-code-review]] — לאמת טענות "יש כאן באג" באופן שיטתי
- [[skill-verification-before-completion]] — אחרי תיקון, לוודא שהבאג נעלם באמת
