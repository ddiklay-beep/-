---
title: Output/images/.gitkeep
tags:
  - file-doc
  - owner/reuven
  - infra/placeholder
aliases:
  - gitkeep-output-images
status: committed
---

# Output/images/.gitkeep

> [!info] Placeholder
> - **נתיב:** `Output/images/.gitkeep`
> - **בעלות:** ראובן
> - **סוג:** קובץ ריק; שומר את התיקייה בגיט. ה-PNGs עצמם gitignored.

## תפקיד
שומר את `Output/images/` קומיטד בגיט. זה היעד שראובן מעתיק אליו את התמונות של יובל לאחר ההפקה, כדי ש-`Output/<name>.md` ו-`Output/<name>.html` יוכלו להפנות ל-`images/<slug>.png` בצורה self-contained (אם מעבירים את `Output/` למקום אחר — הקישורים נשארים). הארכיון המקורי נשאר ב-[[file-gitkeep-yuval-outputs|yuval/outputs/]].

## קבצים קשורים
- [[file-claude-md]] — שלב 4 בתהליך "מאמר עם תמונות" — ראובן מעתיק לכאן
- [[file-yuval-md]] — המקור של ה-PNGs
- [[file-yael-md]] — ה-MD/HTML שמפנים לכאן
- [[file-gitignore]] — מחריג PNGs בתיקייה
- [[file-gitkeep-output]] — תיקיית האב
- [[project-file-inventory]]
