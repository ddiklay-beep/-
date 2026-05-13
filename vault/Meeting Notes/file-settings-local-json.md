---
title: .claude/settings.local.json
tags:
  - file-doc
  - owner/team
  - infra/claude-code
aliases:
  - settings-local
status: gitignored
---

# .claude/settings.local.json

> [!warning] לוקלי בלבד
> - **נתיב:** `.claude/settings.local.json`
> - **בעלות:** מפתח-בודד (פרטי לכל מכונה)
> - **סוג:** JSON של הגדרות Claude Code
> - **מצב גיט:** **gitignored** (ראו [[file-gitignore]])

## תפקיד
קובץ הגדרות פר-מכונה של Claude Code — בעיקר רשימת הרשאות (permissions) שהמשתמש אישר באופן מקומי, מצבי הרצה (sandbox/permission-mode), והעדפות אישיות. אינו מועבר בין מפתחים כי כל אחד מאשר הרשאות אצלו אחרת.

## תוכן עיקרי
- רשימת tool calls מאושרים (allowlist/denylist)
- העדפות UI/UX מקומיות
- (פוטנציאלית) מצב הרשאה ברירת-מחדל

## קבצים קשורים
- [[file-gitignore]] — החוק שמחריג את הקובץ הזה מ-Git
- [[file-claude-md]] — הגדרות פרויקטיות שכן חולקות (לעומת זה)
- [[project-file-inventory]] — הקובץ הזה נשאר מקומי ולכן לא יעלה לעולם ל-GitHub
