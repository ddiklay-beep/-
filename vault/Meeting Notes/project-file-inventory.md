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

נכון ל-2026-05-13 הפרויקט מורכב מ-**8 קבצים שלי בשורש/`.claude/`** (CLAUDE.md, .env, .env.example, .gitignore, שלושת ה-.gitkeep ב-`.claude/*/`, plus settings.local.json הלוקלי) + **שלושה sub-agents** ([[file-yael-md|יעל]] ב-`.claude/agents/yael.md`, [[file-yuval-md|יובל]] ב-`.claude/agents/yuval.md`, ו-[[file-chen-md|חן]] ב-`.claude/agents/chen.md`) ו-**6 תיקיות עבודה** (`yael/reference/`, `yuval/reference/`, `yuval/outputs/`, `chen/Memory/`, `Content/`, `Output/`, `Output/images/` — כל אחת עם `.gitkeep` או קובץ עוגן אחר) + **17 סקילים חיצוניים** (14 מ-Superpowers, 3 obsidian skills) + **סקיל פרויקט-מקומי [[skill-gpt-image-gen]]** ב-`.claude/skills/gpt-image-gen/`. תיעוד הסקילים הוא ברמת ה-skill folder, לא ברמת קובץ פנימי.

ה-vault הזה נמצא ב-`vault/Meeting Notes/`. ה-`_index.md` שם מוביל לכל ה-notes. כל יצירה/עדכון של קובץ בפרויקט מחייבת הוספת note + עדכון ה-index.

## Open Questions

- **שלושת ה-sub-agents מוגדרים** (יעל, יובל, חן — כולם ב-2026-05-13). השלב הבא: slash commands תחת `.claude/commands/` שיעטפו זרימות נפוצות (למשל `/article <נושא>` שמפעיל חן→יעל→יובל ברצף).
- **חלון cache של 30 יום** ב-[[file-chen-md|חן]] קשיח ב-prompt. אם תתעורר צורך — להגמיש (parameter בבקשה מראובן, או חלון שונה לפי tag כמו "evergreen"/"news").
- **אוטו-chain חן → יעל → יובל לא נבחן end-to-end.** הוגדר ב-[[file-claude-md|CLAUDE.md]] בסעיף "תהליך מחקר → תוכן → תמונות" אבל לא רץ בפועל.
- **WebSearch/WebFetch permissions** — לא הוספו ל-`.claude/settings.local.json`. בקריאה הראשונה של חן ייתכן prompt הרשאה למשתמש.
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

### 2026-05-13 — הוספת יובל (מעצב תמונות) + סקיל gpt-image-gen + תהליך מאמר עם תמונות [shipped]

- **What was done:**
  - **סקיל חדש** [[skill-gpt-image-gen]] ב-`.claude/skills/gpt-image-gen/SKILL.md` — מעטפת ל-OpenAI Images API, מודל `gpt-image-2` (יצא 2026-04-21). שתי שיטות (curl+jq, python stdlib fallback).
  - **Sub-agent חדש** [[file-yuval-md|יובל]] ב-`.claude/agents/yuval.md` — `tools: Read, Write, Bash, Glob`. Workflow 8-שלבי שכולל קריאת `yuval/reference/`, חיבור prompt, slugify, קריאת הסקיל, שמירת `.txt` סמוך, אימות, ודיווח.
  - **תיקיות עבודה חדשות:** [[file-gitkeep-yuval-reference|yuval/reference/]], [[file-gitkeep-yuval-outputs|yuval/outputs/]], [[file-gitkeep-output-images|Output/images/]].
  - **עדכון [[file-claude-md|CLAUDE.md]]:** הרחבת שורת יובל ל-Yael-shaped block עם triggers בעברית/אנגלית, הוספת סעיף "תהליך מאמר עם תמונות" (יעל → יובל → ראובן ממזג), עדכון מבנה התיקיות.
  - **עדכון [[file-yael-md|yael.md]]:** הוספת שלב 4 ב-workflow ("זיהוי מקומות לתמונות") שמכניס `{{IMAGE_NEEDED:"..."}}` placeholders ב-MD וב-HTML, ועדכון פורמט הדיווח לראובן עם בלוק `## Image placeholders`.
  - **עדכון [[file-env-example]]:** הוספת `OPENAI_API_KEY=` עם הערה בעברית. [[file-env]] המקומי כבר היה כולל מפתח.
  - **עדכון [[file-gitignore]]:** הוספת `yuval/outputs/*.png` ו-`Output/images/*.png`. ה-`.txt` של ה-prompts וה-`.gitkeep` נשארים מקומיטים.
  - **תיעוד vault מלא:** [[file-yuval-md]], [[skill-gpt-image-gen]], [[file-gitkeep-yuval-reference]], [[file-gitkeep-yuval-outputs]], [[file-gitkeep-output-images]] + עדכון [[_index]] עם הקטגוריה החדשה "סקילים פרויקט-מקומיים".

- **Decisions:**
  - **המודל קבוע ב-`gpt-image-2`** (אזהרה גדולה ב-SKILL). המשתמש הבהיר: המודל קיים, יצא 2026-04-21, ייתכן שלא בידע פנימי ישן יותר. אם הקריאה נכשלת — לחשוד ב-API key/parameters, לא בשם המודל.
  - **גישת merge — "Copy to Output/images/"** (לא reference ל-`yuval/outputs/` ישירות, ולא base64 ב-HTML). יתרון: `Output/` נשאר self-contained וניתן להעברה. החיסרון: כפילות של PNGs — מקובל.
  - **Yael writes MD+HTML with placeholders in both; Raeuven substitutes** (לא רגנרציה של HTML). יתרון: deterministic literal string-replace, צעד אחד פחות.
  - **כלים של יובל: 4** (`Read, Write, Bash, Glob`) — Bash חיוני לקריאת ה-API, Glob לסריקת רפרנס, Write לתמונה ול-`.txt`, Read לרפרנס. בלי Edit (לא עורך קבצים) ובלי Skill (קורא לסקיל דרך Bash).
  - **שיטה B (python stdlib) היא ברירת המחדל בפועל** ל-Windows / Git Bash; שיטה A (curl+jq) נשארה כתיעוד ו-fallback ב-environments עם jq.

- **Notes / Caveats:**
  - לא בוצע smoke test end-to-end לסקיל — דורש `OPENAI_API_KEY` תקין + תקציב פעיל ב-OpenAI. אומת רק structural (frontmatter, נתיבים, gitignore).
  - PNG generation לא ידידותי לסביבת CI אוטומטית — לכן לא ברצף בדיקות.
  - יעל **כן יוצרת HTML עם placeholders כטקסט-שורה** (לא בתוך `<img>`). ראובן עושה literal substitution — דורש שה-substitution string יהיה ייחודי באמת. אם משתמש כותב `{{IMAGE_NEEDED:` במאמר עצמו, יהיה collision.

- **Related:** [[file-yuval-md]], [[skill-gpt-image-gen]], [[file-claude-md]], [[file-yael-md]], [[file-env]], [[file-env-example]], [[file-gitignore]], [[file-gitkeep-yuval-reference]], [[file-gitkeep-yuval-outputs]], [[file-gitkeep-output-images]]

### 2026-05-13 — יצירת sub-agent chen (חוקרת הרשת) + זרימה חן→יעל→יובל [shipped]

- **What was done:**
  - **Sub-agent חדש** [[file-chen-md|חן]] ב-`.claude/agents/chen.md` — `tools: WebSearch, WebFetch, Read, Write, Edit, Glob, Grep`. Body בעברית: תפקיד והערך המוסף ("מידע עכשווי, מקורות אמיתיים, לא הזיות"), טעינת קונטקסט חובה (`Read` + `Grep` של `chen/Memory/searches.md` עם חלון 30 יום), הגדרת "נושא דינמי" (חדשות / מחירים / השקות → תמיד לחפש מחדש), workflow מלא (זיכרון → WebSearch → WebFetch → סינון → טיפול בכישלון עד 3 שאילתות → שמירה ל-`Content/<YYYY-MM-DD>-<slug>.md` עם YAML frontmatter → לוג ב-Memory → דיווח), קריטריונים למקור איכותי, פורמט entry קבוע ב-Memory.
  - **תיקיית עבודה חדשה** [[file-chen-memory-searches|chen/Memory/]] עם `searches.md` (header + הפניה לפורמט) ו-`.gitkeep`.
  - **עדכון [[file-claude-md|CLAUDE.md]]:** (a) בלוק חן הקצר ("החוקרת. אוספת מידע") הוחלף בבלוק מלא בסגנון יעל/יובל עם triggers בעברית/אנגלית; (b) סעיף חדש "תהליך מחקר → תוכן → תמונות" שמתאר את הזרימה חן → (אופציונלי) יעל → (אופציונלי) יובל, ואת תנאי הסיום (רק חן אם הבקשה הייתה רק מחקר); (c) `chen/Memory/` נוסף למבנה התיקיות, ו-`Content/` הורחב כדי לציין שגם חן יכולה להניח שם קבצים; (d) הערת הסיום עודכנה — שלושת הסוכנים מוגדרים, השלב הבא slash commands.
  - **תיעוד vault מלא:** [[file-chen-md]], [[file-chen-memory-searches]] + עדכון [[_index]].

- **Decisions:**
  - **7 כלים** (WebSearch, WebFetch, Read, Write, Edit, Glob, Grep) — בלי Bash (WebSearch/WebFetch built-in), בלי Skill, בלי Agent. מאפיין מבדל עיקרי מ-LLM ידע: WebFetch מספק מידע עכשווי + לינק.
  - **קובץ flat** (תואם ל-yael/yuval).
  - **YAML frontmatter ב-`Content/<YYYY-MM-DD>-<slug>.md`** עם `source_url`, `source_title`, `source_date`, `fetched_at`, `query` — אושר עם המשתמש. יעל קוראת רק את הגוף (לפי ה-spec שלה), אז ה-frontmatter לא מפריע, אבל קיים לאודיט וכ-source of truth.
  - **3 retries לפני failure** — מספר שרירותי שעובד טוב. גם הכישלון נרשם ב-Memory כדי שחיפוש עתידי על נושא דומה לא יחזור על אותן שאילתות.
  - **חלון cache 30 יום קשיח ב-prompt** — Open Question אם להגמיש. בינתיים החלטה פשוטה ועקבית; נושאים דינמיים (חדשות/מחירים) ממילא בורחים מה-cache.
  - **אוטו-chain ב-CLAUDE.md, לא ב-chen** — חן לא קוראת ליעל ישירות (אין לה `Agent`). ראובן מחליט: triggers של חן בלבד → עוצרים בחן; חן+יעל triggers → ראובן ממשיך אוטומטית.
  - **שם `chen/Memory/`** (ולא `cache/` או `logs/`) — מבטא גם cache וגם audit trail.
  - **לא הוספנו WebSearch/WebFetch ל-`settings.local.json`** — Claude Code יבקש הרשאה בריצה ראשונה. המשתמש יחליט אם לאשר one-shot או להוסיף ל-allow list.

- **Notes / Caveats:**
  - לא בוצע smoke test end-to-end. שיגור "מצאי לי מאמר על Anthropic MCP" אמור לטריגר את חן בלבד; "מצאי ושכתבי מאמר על X" אמור לעשות chain חן→יעל. תרחיש לבדיקה ידנית בסשן הבא.
  - חן **לא מעדכנת את ה-vault בעצמה** — עקבי עם יעל ויובל. עדכון ה-vault הוא תפקיד ראובן.
  - שלא כמו יעל/יובל אין לחן `chen/reference/` — אין עדיין הגדרה ברורה מה הסטנדרט שצריך לרפרנס לחיפוש מהרשת. ייתכן שיווצר אם תצטבר קולקציה של "מקור טוב לתחילת זרימה".
  - **YAML frontmatter ב-`Content/`** — לפי ה-spec של [[file-yael-md|יעל]] היא מתחילה לקרוא מהגוף, אבל הנחת ה-fronmatter לא נבדקה end-to-end איתה. יש סיכון קטן שתשכתב את ה-frontmatter במקום להתעלם — לאמת בריצה הראשונה.

- **Related:** [[file-chen-md]], [[file-chen-memory-searches]], [[file-claude-md]], [[file-yael-md]], [[file-yuval-md]], [[file-gitkeep-content]]
