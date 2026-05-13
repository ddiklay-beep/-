---
title: .env.example
tags:
  - file-doc
  - owner/team
  - infra/secrets
aliases:
  - dot-env-example
status: committed
---

# .env.example

> [!info] תבנית
> - **נתיב:** `.env.example` (שורש הפרויקט)
> - **בעלות:** צוות (תבנית משותפת)
> - **סוג:** Markdown של משתני סביבה (ללא ערכים)
> - **מצב גיט:** מקומיט; משמש כמסמך התבניות הציבורי של הפרויקט

## תפקיד
תבנית ל-[[file-env]]. מציג לכל מפתח חדש שמצטרף איזה משתני סביבה צריך למלא ב-`.env` המקומי שלו. אסור לשים כאן ערכים אמיתיים — רק שמות מפתחות והערות הסבר.

## תוכן עיקרי
- `ANTHROPIC_API_KEY=` — מפתח API של Anthropic
- `ANTHROPIC_MODEL=` — מודל ברירת-מחדל
- הערות על מתי כל משתנה דרוש

## קבצים קשורים
- [[file-env]] — ה"תאום" המקומי עם הערכים האמיתיים
- [[file-gitignore]] — מוודא ש-`.env` לא ידלוף, אבל מאפשר ל-`.env.example` להיות מקומיט
- [[project-file-inventory]] — הקובץ הזה נוסף לפרויקט בסשן 2026-05-13
