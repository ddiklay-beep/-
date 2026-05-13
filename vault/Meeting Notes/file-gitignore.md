---
title: .gitignore
tags:
  - file-doc
  - owner/team
  - infra/git
aliases:
  - dot-gitignore
status: committed
---

# .gitignore

> [!info] חוקי git
> - **נתיב:** `.gitignore` (שורש הפרויקט)
> - **בעלות:** צוות (תקף לכל המפתחים)
> - **סוג:** רשימת patterns להחרגה ממעקב git
> - **מצב גיט:** מקומיט

## תפקיד
מגדיר אילו קבצים לא יעלו ל-GitHub גם אם הם קיימים מקומית. שומר על שני סוגי קבצים מחוץ לריפו: סודות (`.env`) והגדרות מקומיות של Claude Code (`settings.local.json`).

## תוכן עיקרי
- `.claude/settings.local.json` — הגדרות לוקליות של Claude Code (לא חולקים)
- `.env` / `.env.local` / `.env.*.local` — קבצי סודות

## קבצים קשורים
- [[file-env]] — מוחרג ע"י החוק `.env`
- [[file-env-example]] — **לא** מוחרג; משמש כתבנית פתוחה
- [[file-settings-local-json]] — מוחרג ע"י `.claude/settings.local.json`
- [[file-claude-md]] — לא מוחרג; CLAUDE.md חייב להיות מקומיט כדי שהוא ייטען בכל סשן
