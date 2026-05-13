---
title: Project File Inventory
tags:
  - topic
  - architecture
  - documentation
aliases:
  - file-inventory
  - inventory
---

# Project File Inventory

## Overview

תיעוד מלא של כל קובצי הפרויקט "סדנא" — מערכת צוות סוכנים ליצירת תוכן (ראובן המנכ"ל + יעל/יובל/חן). כל קובץ מקבל note ייעודי ב-vault שמתאר:
1. **מה הקובץ עושה** (תפקיד),
2. **למי הוא שייך** (ראובן / צוות / חיצוני),
3. **קבצים קשורים** דרך `[[wikilinks]]`.

נכון ל-2026-05-13 הפרויקט מורכב מ-**8 קבצים שלי בשורש/`.claude/`** (CLAUDE.md, .env, .env.example, .gitignore, שלושת ה-.gitkeep ב-`.claude/*/`, plus settings.local.json הלוקלי) + **sub-agent יעל** ([[file-yael-md]] ב-`.claude/agents/yael.md`) ו-**3 תיקיות עבודה** שלו (`yael/reference/`, `Content/`, `Output/` — כל אחת עם `.gitkeep`) + **17 סקילים מותקנים** (14 מ-Superpowers, 3 obsidian skills). תיעוד הסקילים הוא ברמת ה-skill folder, לא ברמת קובץ פנימי.

ה-vault הזה נמצא ב-`vault/Meeting Notes/`. ה-`_index.md` שם מוביל לכל ה-notes. כל יצירה/עדכון של קובץ בפרויקט מחייבת הוספת note + עדכון ה-index.

## Open Questions

- **Sub-agents יובל וחן עדיין לא הוגדרו** ב-`.claude/agents/`. [[file-yael-md|יעל]] הושלמה ב-2026-05-13. כשייווצרו יובל וחן — להוסיף file-doc לכל אחד ולעדכן את [[file-gitkeep-agents]].
- `.claude/agents/.gitkeep` כעת **מיותר טכנית** (התיקייה כבר לא ריקה — יש בה את `yael.md`). להישאר בעקבות ההוראה הכוללת "לא לדרוס", או להסיר במעבר עתידי?
- האם להגדיר `model:` ל-[[file-yael-md|yael]] (sonnet/opus/haiku) או להישאר ב-`inherit` (ברירת-מחדל)? `sonnet` סביר לכתיבה; `opus` יקר אך איכותי יותר; `haiku` חלש מדי לתוכן.
- האם להוסיף `permissionMode: acceptEdits` ליעל, כדי שלא תייצר prompts בכל Write ל-`Output/`?
- כשהמשתמש ייצור את `yael/style-guide.md` ויוסיף דוגמאות ל-[[file-gitkeep-yael-reference|yael/reference/]] — מי יוסיף את ה-file-docs המתאימים ב-vault?
- אין עדיין slash commands ב-`.claude/commands/` — כנ"ל ל-[[file-gitkeep-commands]].
- האם להעמיק ל-per-internal-file לסקילים (helper.js, find-polluter.sh וכו')? כרגע נבחר scope של per-skill בלבד; אפשר להרחיב אם נדרש.
- האם ליצור `.base` ([[skill-obsidian-bases]]) שמציג טבלת file-docs מסוננת לפי `owner/*` ו-`status`?
- folders נוספים ב-vault (`Content Briefs/`, `Publishing Log/`, `Brand Guidelines/`) — לא נוצרו עדיין; ייווצרו "on first use" כשתגיע משימה רלוונטית, לפי ה-protocol של [[skill-obsidian-vault-workflow]].

## Session Log

### 2026-05-13 — הקמת vault ותיעוד ראשון של כל קובצי הפרויקט [shipped]

- **What was done:**
  - יצירת `vault/Meeting Notes/` עם `_index.md` המקושר לכל ה-notes.
  - 8 file-docs לקבצי הפרויקט: [[file-claude-md]], [[file-env]], [[file-env-example]], [[file-gitignore]], [[file-gitkeep-agents]], [[file-gitkeep-commands]], [[file-gitkeep-skills]], [[file-settings-local-json]].
  - 17 skill-docs (per-folder) ל-Superpowers (14) ו-obsidian-skills (3): [[skill-brainstorming]], [[skill-dispatching-parallel-agents]], [[skill-executing-plans]], [[skill-finishing-a-development-branch]], [[skill-receiving-code-review]], [[skill-requesting-code-review]], [[skill-subagent-driven-development]], [[skill-systematic-debugging]], [[skill-test-driven-development]], [[skill-using-git-worktrees]], [[skill-using-superpowers]], [[skill-verification-before-completion]], [[skill-writing-plans]], [[skill-writing-skills]], [[skill-obsidian-bases]], [[skill-obsidian-markdown]], [[skill-obsidian-vault-workflow]].
  - עדכון [[file-claude-md]] שיכלול הוראת חובה להפעלת [[skill-obsidian-vault-workflow]] בתחילת + סוף כל משימה (Phase 1 / Phase 2).
  - commit + push ל-`origin/main`.

- **Decisions:**
  - **גרניולריות:** per-file לקבצי הפרויקט, per-skill (לא per-internal-file) לסקילים מותקנים. סיבה: SKILL.md הוא ה-canonical interface של הסקיל; קבצים פנימיים הם implementation. אם יידרש בעתיד — ניתן להרחיב.
  - **שמות קבצים:** `file-<hyphenated>.md` ו-`skill-<hyphenated>.md` — מבדל בין שני הסוגים לעין ולחיפוש.
  - **placement:** הכל בתוך `vault/Meeting Notes/` במקום ליצור sub-folder, כי ה-_index.md מספיק לסיווג.
  - **Wikilinks דו-כיווניים:** כל note מקושר ל-2-4 קבצים קשורים מתוכן (Obsidian יבנה backlinks אוטומטית).
  - **תאם CLAUDE.md מצומצם:** מוסיפים סעיף קצר "Workflow rule" שמפנה ל-[[skill-obsidian-vault-workflow]], לא משכפלים את ההוראות (single source of truth).

- **Notes / Caveats:**
  - [[file-env]] ו-[[file-settings-local-json]] gitignored — ה-notes שלהם כן מקומיטים ב-vault, אבל הקבצים עצמם לא יישלחו לעולם ל-GitHub.
  - יש 4 system-reminders של TodoWrite שהתעלמתי מהם בכוונה — המשימה הזו זרמה ליניארית בלי תלויות סבוכות, לא דרשה todo list.
  - הסקילים הותקנו בסשן קודם (commit `f5356fb`); רק התיעוד נוסף עכשיו.
  - הסקיל [[skill-obsidian-vault-workflow]] עצמו דורש Phase 1 בתחילת המשימה — בפועל, ה-vault היה ריק לכן Phase 1 הצטמצם ל"אין topic file קיים, יוצרים חדש בסוף" וקריאת הסקילים הרלוונטיים ([[skill-obsidian-markdown]]).

- **Related:** [[skill-obsidian-vault-workflow]], [[skill-obsidian-markdown]], [[file-claude-md]], [[file-gitkeep-skills]]

### 2026-05-13 — יצירת sub-agent yael (כותבת התוכן) [shipped]

- **What was done:**
  - יצירת [[file-yael-md|.claude/agents/yael.md]] — ה-sub-agent הראשון בפרויקט. Frontmatter עם `name: yael`, `tools: Read, Write, Edit, Glob, Grep`, ו-`description` שמכיל trigger keywords בעברית ובאנגלית. Body (system prompt) בעברית: תפקיד, טעינת קונטקסט חובה (`yael/style-guide.md` + `yael/reference/`), workflow 5-שלבי, פורמט HTML ידני עם CSS משובץ ו-`dir="rtl"`, וכללי כתיבה (לא להוסיף קישורים/CTAs של המחבר; מותגים בסיפור נשארים).
  - יצירת מבני תיקיות העבודה: [[file-gitkeep-yael-reference|yael/reference/]], [[file-gitkeep-content|Content/]], [[file-gitkeep-output|Output/]] — כל אחת עם `.gitkeep`.
  - עדכון [[file-claude-md|CLAUDE.md]]: שורת יעל הורחבה עם קישור ל-`.claude/agents/yael.md`, רשימת trigger keywords (עברית + אנגלית), והבהרה של מה אין לה.
  - תיעוד 4 קבצים חדשים ב-vault: [[file-yael-md]], [[file-gitkeep-yael-reference]], [[file-gitkeep-content]], [[file-gitkeep-output]], ועדכון [[_index]] עם קטגוריה חדשה "תיעוד סוכנים".

- **Decisions:**
  - `tools: Read, Write, Edit, Glob, Grep` — בדיוק 5 כלים, לפי הוראת המשתמש. ללא Bash, WebFetch, Skill, ו-Agent. משמעות: יעל לא יכולה לקרוא ל-skills (כמו [[skill-obsidian-markdown]]), אז ה-system prompt שלה ספציפי ועצמאי.
  - `name: yael` ב-ASCII kebab-case (חובה ל-Claude Code לפי הדוקומנטציה). שם ההצגה העברי הוטמע ב-`description`.
  - HTML מיוצר ידנית (אין Bash → אין markdown→html converter). שלד מינימלי עם CSS משובץ ו-`dir="rtl"` נכלל ב-system prompt.
  - שדות `model`, `permissionMode` נשארו לא-מוגדרים (inherit). מועברים ל-Open Questions להחלטה.
  - `yael/style-guide.md` **לא** נוצר — המשתמש אמר שיצור בנפרד.
  - אומת פורמט ה-sub-agent מהדוקומנטציה הרשמית (code.claude.com/docs/en/sub-agents) דרך Explore agent לפני התכנון.

- **Notes / Caveats:**
  - ה-`description` ב-frontmatter מצרף trigger keywords בעברית ובאנגלית באותה שורה כדי שה-auto-delegation של ראובן יזהה גם קלט עברי וגם אנגלי.
  - יעל **לא מעדכנת את ה-vault בעצמה** — זה אחריות של ראובן (ה-orchestrator) בכל קריאה. אם בעתיד נרצה שגם sub-agents יתעדו, נצטרך להוסיף להן Skill / Edit access ל-vault או לעבור למודל hook-based.
  - `.claude/agents/.gitkeep` נשאר במקום (טכנית מיותר); זה ב-Open Questions.
  - בקרת איכות ידנית למשתמש: לבדוק שאוטו-דלגציה מטריגרת על "שכתבי בבקשה את `Content/X.md`", לוודא ש-`Output/X.md` ו-`Output/X.html` נוצרים, ולבדוק ש-יעל מסרבת בעדינות למשימות שדורשות WebFetch.

- **Related:** [[file-yael-md]], [[file-claude-md]], [[file-gitkeep-content]], [[file-gitkeep-output]], [[file-gitkeep-yael-reference]], [[file-gitkeep-agents]], [[skill-writing-skills]], [[skill-obsidian-markdown]]
