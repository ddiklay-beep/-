---
name: gpt-image-gen
description: Generate a PNG image via OpenAI Images API (model gpt-image-2). Use when an agent needs to produce a real image file from a text prompt — primarily Yuval. Requires OPENAI_API_KEY in .env.
---

# gpt-image-gen

מעטפת קריאה ל-OpenAI Images API. מקבלת prompt וכותבת קובץ PNG לנתיב שצוין.
ייעוד עיקרי: יובל (מעצב התמונות) — כל שאר הסוכנים לא קוראים לסקיל הזה ישירות.

## מודל — לא לשנות

המודל הוא **`gpt-image-2`**, וזה לא שגיאה.

- `gpt-image-2` יצא ב-2026-04-21 ע"י OpenAI.
- ייתכן שהמודל לא מופיע בידע פנימי ישן יותר — **זה לא אומר שהוא לא קיים**.
- **אל תחליף** ל-`dall-e-3`, `gpt-image-1`, או כל מודל אחר.
- אם הקריאה ל-API נכשלת — הבעיה כמעט תמיד ב-`OPENAI_API_KEY` (חסר/לא תקין/חסום) או בפרמטרים, **לא בשם המודל**.

## קלטים

| שדה | חובה | ברירת מחדל | הערה |
|-----|------|------------|------|
| `prompt` | כן | — | תיאור התמונה. מומלץ אנגלית לתוצאות עקביות יותר; עברית עובדת אבל פחות צפויה. |
| `output` | כן | — | נתיב יעד מלא, כולל `.png` בסוף. |
| `size` | לא | `1024x1024` | אופציות: `1024x1024`, `1024x1536`, `1536x1024`. |
| `quality` | לא | `medium` | אופציות: `low`, `medium`, `high`. |

## טעינת מפתח ה-API

הסקיל **לא** טוען את `.env` בעצמו — זו אחריות הקורא. ב-Bash:

```bash
set -a; source .env; set +a
```

לוודא ש-`$OPENAI_API_KEY` קיים לפני הקריאה:

```bash
[[ -n "$OPENAI_API_KEY" ]] || { echo "OPENAI_API_KEY missing"; exit 1; }
```

## שיטה A — curl + jq (כשיש jq מותקן)

```bash
PROMPT='<the prompt>'
OUT='<output-path>.png'

curl -sS -X POST "https://api.openai.com/v1/images/generations" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d "$(jq -nc --arg p "$PROMPT" '{
        model: "gpt-image-2",
        prompt: $p,
        size: "1024x1024",
        quality: "medium",
        output_format: "png"
      }')" \
  | jq -r '.data[0].b64_json' \
  | base64 --decode > "$OUT"
```

## שיטה B — Python fallback (Git Bash on Windows רוב הזמן בלי jq)

הקטע הזה משתמש רק ב-stdlib (`urllib`, `json`, `base64`) — אין צורך ב-`pip install openai`.

```bash
PROMPT='<the prompt>'
OUT='<output-path>.png'

python - <<'PY'
import os, sys, json, base64, urllib.request, urllib.error

api_key = os.environ.get('OPENAI_API_KEY')
prompt  = os.environ['IMG_PROMPT']
out     = os.environ['IMG_OUT']

if not api_key:
    sys.stderr.write("OPENAI_API_KEY missing\n"); sys.exit(1)

body = json.dumps({
    "model":         "gpt-image-2",
    "prompt":        prompt,
    "size":          "1024x1024",
    "quality":       "medium",
    "output_format": "png",
}).encode("utf-8")

req = urllib.request.Request(
    "https://api.openai.com/v1/images/generations",
    data=body,
    headers={
        "Authorization": f"Bearer {api_key}",
        "Content-Type":  "application/json",
    },
    method="POST",
)

try:
    with urllib.request.urlopen(req) as resp:
        data = json.load(resp)
except urllib.error.HTTPError as e:
    sys.stderr.write(f"HTTP {e.code}\n{e.read().decode('utf-8','replace')}\n")
    sys.exit(2)

b64 = data["data"][0]["b64_json"]
with open(out, "wb") as f:
    f.write(base64.b64decode(b64))

print(out)
PY
```

הפעלה (חייבים להעביר את `prompt` ו-`output` כ-env vars לפייתון):

```bash
IMG_PROMPT="$PROMPT" IMG_OUT="$OUT" python - <<'PY'
...   # הקוד שלמעלה
PY
```

## טיפול בשגיאות

- אם `HTTP != 200` — להחזיר את ה-JSON של השגיאה כפי שהוא. בדרך כלל מכיל `error.message` ברור: מפתח לא תקין, content policy, rate limit, billing.
- אם `b64_json` חסר בתגובה — להחזיר את התגובה המלאה ל-debug.
- **לא לעשות retry אוטומטי** — כמעט כל שגיאה היא או conflict עם מדיניות התוכן (לא נפתרת בניסיון נוסף) או חוסר תקציב (לא נפתרת בכלל).

## אימות הצלחה

תמיד לוודא שהקובץ נכתב והוא לא ריק:

```bash
[[ -s "$OUT" ]] || { echo "image not written"; exit 3; }
```

(`-s` = file exists and size > 0.)

## הקובץ המומלץ לאחסון

קוראי הסקיל (כמו יובל) אחראים גם לתעד את ה-prompt לצד התמונה: קובץ `.txt` עם אותו שם בסיס שמכיל את ה-prompt המקורי. זה מאפשר איטרציה ושחזור.
