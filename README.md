# AI Engineer Handbook

A single-file website: six study books for a 26-week path from backend engineer
to AI application engineer, with a day-by-day plan, quizzes and progress tracking.

Everything is in `index.html`. No build step, no server, no dependencies.
The only outside resource is the Google Fonts stylesheet; without internet the
page falls back to system fonts and works the same.

## Run it locally

Double-click `index.html`, or open it from any browser's File menu.

Progress (ticked days, checklists, start date) is saved in the browser's
localStorage for that file's location. If you move the file or open it from a
different browser, progress starts fresh.

## Put it on the web

### Option A: GitHub Pages (free, public URL)

1. Create a new repository on your **personal** GitHub account, for example
   `ai-engineer-handbook`. Make it **Public** (GitHub Pages on free accounts
   requires a public repo).
2. Upload `index.html` to the root of the repo (drag it onto the repo page, or
   `git init`, `git add index.html`, `git commit`, `git push`).
3. In the repo: **Settings → Pages → Build and deployment**
   - Source: *Deploy from a branch*
   - Branch: `main`, folder `/ (root)` → **Save**
4. After a minute or two the site is live at
   `https://<your-username>.github.io/ai-engineer-handbook/`

To update, replace `index.html` and push. Pages redeploys automatically.

### Option B: Netlify Drop (free, unlisted URL, no account needed to try)

1. Go to <https://app.netlify.com/drop>
2. Drag the folder containing `index.html` onto the page.
3. You get a URL like `https://random-words-1234.netlify.app` right away.
   Sign in (free) to keep the site and rename it.

The URL is public but not listed or indexed anywhere, which is a reasonable
middle ground if you don't want a public repo.

### Option C: Cloudflare Pages

Same idea as Netlify: <https://pages.cloudflare.com>, "Upload assets", drop the
folder. Free, fast, custom domains supported.

## Lesson pages

`lessons/` holds one full lesson page per study session (`day-01.html`, `day-03.html`, ...).
Each day in the plan links to its lesson with "Open the lesson". Keep the `lessons/`
folder next to `index.html` when you host or move the site. `lessons/lesson.css` is
the shared stylesheet.

## Editing the content

`source/` holds the editable pieces:

- `source/parts/*.html` — the shelf and the six books, one file each
- `source/tools/daily_plan.py` — the day-by-day plan as data (tasks and quizzes),
  plus the code that renders it into each book
- `source/tools/patch-*.txt` — small style and shelf fragments

To rebuild after editing:

```bash
cd source
python tools/daily_plan.py parts          # regenerates the daily plan blocks
cat parts/00-head.html parts/10-shelf.html parts/11-book1.html parts/12-book2.html \
    parts/13-book3.html parts/14-book4.html parts/15-book5.html parts/16-book6.html \
    parts/99-tail-v2.html > stitched.html
# the generator links a day to lessons/day-NN.html only when that file exists
```

Then wrap `stitched.html` in the document skeleton exactly as `index.html` is:
`<!doctype html><html lang="en"><head>` + base styles before the content's
`<title>`, `</head><body>` before `<header class="top">`, and `</body></html>`
at the end. Or simply edit `index.html` directly; it's plain HTML.

## Privacy notes

- The page contains no personal data. Your progress never leaves your browser.
- Two passing references to internal engineering terms ("VBD", "rounding ADR")
  appear in explanatory notes. They are generic architecture vocabulary, not
  confidential, but you can search and reword them before publishing if you prefer.
