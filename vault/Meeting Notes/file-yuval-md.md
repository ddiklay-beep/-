---
title: .claude/agents/yuval.md
tags:
  - file-doc
  - owner/yuval
  - agent
aliases:
  - yuval-agent
  - yuval.md
status: committed
---

# .claude/agents/yuval.md

> [!info] Sub-agent
> - **נתיב:** `.claude/agents/yuval.md`
> - **בעלות:** יובל (sub-agent שני בפרויקט)
> - **סוג:** Claude Code sub-agent (Markdown עם YAML frontmatter)
> - **מצב גיט:** מקומיט; נטען אוטומטית ע"י Claude Code כשראובן מעריך שהמשימה דורשת תמונה

## תפקיד
מעצב התמונות של הצוות. מקבל מראובן בקשה לתמונה בודדת (בדרך כלל בעקבות placeholder שיעל השאירה), קורא את `yuval/reference/` ללמוד את הסגנון הוויזואלי של הפרויקט, ומפיק קובץ PNG ל-`yuval/outputs/<YYYY-MM-DD>-<slug>.png` יחד עם `.txt` סמוך שמכיל את ה-prompt המלא שנשלח ל-API. **המטרה היא עקביות ויזואלית בין כל התמונות שנוצרות בפרויקט.**

## תוכן עיקרי

**Frontmatter:**
- `name: yuval` (kebab-case ASCII — חובה ל-Claude Code)
- `description:` כולל trigger keywords בעברית ובאנגלית, להפעלת auto-delegation ע"י ראובן
- `tools: Read, Write, Bash, Glob` — 4 כלים. Bash דרוש כי הקריאה ל-API היא דרך הסקיל `gpt-image-gen` שעובד עם curl/python.

**Body (system prompt):** הצגה עצמית, תפקיד, טעינת קונטקסט חובה (`yuval/reference/`), workflow 8-שלבי (קונטקסט → בחירת רכיבים → prompt → slug → קריאת הסקיל → שמירת `.txt` סמוך → אימות → דיווח), מגבלות (לא כותב מאמרים, אין web, אין דישפץ' לסוכנים אחרים, לא נוגע בקבצים מחוץ ל-`yuval/outputs/`).

## קבצים קשורים
- [[file-claude-md]] — ראובן הוא זה שמנתב משימות תמונה ליובל
- [[file-yael-md]] — יעל משאירה placeholders שיובל ממלא
- [[skill-gpt-image-gen]] — הסקיל שיובל קורא לו ליצירת התמונה בפועל
- [[file-env]] — ממנו נטען `OPENAI_API_KEY` הדרוש לסקיל
- [[file-gitkeep-yuval-reference]] — דוגמאות סגנון ויזואלי שיובל קורא
- [[file-gitkeep-yuval-outputs]] — יעד הפלט של יובל (ארכיון מקורי)
- [[file-gitkeep-output-images]] — יעד ההעתקה של ראובן ל-MD/HTML הסופיים
- [[project-file-inventory]] — קובץ-טופיק שבו תועד הסשן הזה

## Open Questions
- אין רפרנס סגנון ב-`yuval/reference/` עדיין — התמונה הראשונה שיובל יפיק תהיה זו שתגדיר את הסגנון של הפרויקט. כדאי שראובן ייצור אז note ב-vault שמתעד את הסגנון.
- האם להגדיר `model:` ליובל? Bash-heavy + prompt composition יכול להצדיק `sonnet` או `opus`.

## Session Log

### 2026-05-13 — יצירת sub-agent yuval (מעצב התמונות) [shipped]

- **What was done:**
  - יצירת [[file-yuval-md|.claude/agents/yuval.md]] — sub-agent שני בפרויקט. Frontmatter עם `name: yuval`, `tools: Read, Write, Bash, Glob`, ו-`description` שמכיל trigger keywords בעברית ובאנגלית (תמונה של / image of וכו'). Body (system prompt) בעברית מתאר workflow 8-שלבי: טעינת `yuval/reference/`, בחירת רכיבי סגנון, חיבור prompt באנגלית, slugify ל-kebab-case ASCII, הפעלת [[skill-gpt-image-gen]] דרך Bash, שמירת `.txt` סמוך עם ה-prompt, אימות `-s`, דיווח לראובן.
  - יצירת [[file-gitkeep-yuval-reference|yuval/reference/]] ו-[[file-gitkeep-yuval-outputs|yuval/outputs/]] עם `.gitkeep`.
  - יצירת [[file-gitkeep-output-images|Output/images/]] עם `.gitkeep` — היעד שראובן מעתיק אליו תמונות לאחר שיובל הפיק.

- **Decisions:**
  - **שם הסוכן `yuval`** (kebab-case ASCII).
  - **4 כלים** (`Read, Write, Bash, Glob`) — בלי Edit (יובל לא עורך קבצים קיימים), בלי Grep, בלי Skill (קורא לסקיל דרך Bash, לא דרך `Skill`-tool).
  - **קובץ flat ולא תיקייה** — תואם ל-[[file-yael-md|yael]] ולדוקומנטציה של Claude Code.
  - **שתי תיקיות פלט נפרדות:** `yuval/outputs/` (canonical archive עם ה-prompts), `Output/images/` (העתק לצריכה ע"י MD/HTML). הסיבה: לשמור על `Output/` self-contained וגם להחזיק היסטוריה מלאה של ה-prompts בנפרד.
  - **גישת merge — "Copy to Output/images/"** ולא "Reference yuval/outputs/ directly". נבחר אחרי שאלת הבהרה למשתמש.

- **Notes / Caveats:**
  - הסקיל [[skill-gpt-image-gen]] משתמש במודל `gpt-image-2` (יצא 2026-04-21). זה לא בידע פנימי ישן יותר — לא להחליף אותו ב-`dall-e-3` או אחר.
  - PNGs מ-`yuval/outputs/*.png` ומ-`Output/images/*.png` נוספו ל-[[file-gitignore]] — לא קומיטים אותם ל-git. ה-`.gitkeep` וקובצי ה-`.txt` של ה-prompts כן בגיט.
  - יובל **לא מעדכן את ה-vault בעצמו** — זה אחריות ראובן, כמו אצל יעל.

- **Related:** [[file-yuval-md]], [[file-claude-md]], [[file-yael-md]], [[skill-gpt-image-gen]], [[file-env]], [[file-env-example]], [[file-gitignore]], [[file-gitkeep-yuval-reference]], [[file-gitkeep-yuval-outputs]], [[file-gitkeep-output-images]]
