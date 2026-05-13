---
title: skill — verification-before-completion
tags:
  - skill-doc
  - owner/external
  - source/superpowers
aliases:
  - verification-before-completion
---

# Skill: verification-before-completion

> [!info] סקיל מותקן
> - **נתיב:** `.claude/skills/verification-before-completion/`
> - **מקור:** Superpowers (v5.1.0)
> - **בעלות:** חיצוני

## תפקיד
"Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always."

## מתי להפעיל
לפני **כל הכרזה** של "סיימתי / תוקן / עובר". להריץ פקודות אימות בפועל ולהציג פלט. ראיות לפני אמירות.

## קבצים בתיקייה
- `SKILL.md` — בלבד

## קבצים קשורים
- [[skill-test-driven-development]] — הטסטים הם הראיה הראשית
- [[skill-systematic-debugging]] — אחרי תיקון באג, אימות שהוא נעלם באמת
- [[skill-finishing-a-development-branch]] — חובה לפני סגירת branch
- [[skill-obsidian-vault-workflow]] — Phase 2 של ה-vault-workflow כולל verification של ה-write
