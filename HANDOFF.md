# AI Engineer Handbook — handoff for continuing in a new session

Written 2026-11-01. Read this first if continuing the lesson-writing work in a fresh Claude session.

## What this is
A self-contained learning website for Suresh (a .NET/C# backend engineer at Trimble, works on
a multi-tenant accounting service) to move into AI application engineering over 26 weeks.
Six "books" (one per plan phase), a day-by-day plan (130 sessions over 182 days), and one
full lesson page per session with diagrams, code, exercises, videos, a 6-question checkpoint
quiz and a "Done when" checklist.

Published artifact (private): https://claude.ai/artifact/Jr8gT4pk7YVdxWQkuda59E
The published page is `ai-engineer-handbook.html` plus supporting files `lessons/*.html` and
`lessons/lesson.css`, published with the Artifact tool using `root` = the ai-handbook folder
and a `files` list of relative paths. Files not re-sent are kept, so only new/changed files
need to be listed on each publish.

## Where files live
Working copy (session scratchpad; may not survive):
  C:\Users\skariba\AppData\Local\Temp\claude\c--Users-skariba-Source-Repos-prism-accounting\10c5bf01-3b68-4687-b317-b386c85c464a\scratchpad\
    ai-handbook\parts\*.html       shelf + six books + head/tail (stitched into the main page)
    ai-handbook\lessons\*.html     lesson pages, day-NN.html, plus lesson.css
    ai-handbook\ai-engineer-handbook.html   stitched main page (artifact body, no doctype)
    tools\daily_plan.py            THE PLAN DATA: tasks + quiz per session, renders the
                                    day-by-day blocks into each book part; links a day to
                                    lessons/day-NN.html only if that file exists
    tools\diagrams_book1.py        inserted "picture of the day" blocks into Book 1 lessons
    tools\patch-css.txt, patch-shelf.txt

Durable copy (this folder): C:\Users\skariba\Documents\ai-engineer-handbook\
    index.html        standalone page (doctype + skeleton wrapped around the artifact body)
    lessons\          same lesson pages; keep next to index.html when hosting
    source\parts\, source\tools\   copies of the above
    README.md         hosting instructions (GitHub Pages / Netlify / Cloudflare)
    HANDOFF.md        this file

If the scratchpad is gone, rebuild the working copy from source\ and lessons\ here.

## Day numbering
Week w has sessions on days (w-1)*7 + d for d in {1,3,4,6,7} (Mon, Wed, Thu, Sat, Sun);
d=2,5 are rest days. Books start at weeks 1, 5, 9, 14, 18, 22 (Book 3 and 6 have 5 weeks).
Hours: Mon/Wed/Thu 2 h, Sat 4 h, Sun 2 h. Kind per day is Learn/Build/Review as in daily_plan.py.

## Progress (lesson pages)
DONE: Book 1 (days 1,3,4,6,7,8,10,11,13,14,15,17,18,20,21,22,24,25,27,28) — with diagrams, published
DONE: Book 2 (days 29,31,32,34,35,36,38,39,41,42,43,45,46,48,49,50,52,53,55,56) — published
DONE: Book 3 (days 57..91, all 25) — published
DONE: Book 4 (days 92..119, all 20) — published (artifact v8)
DONE: Book 5 (days 120..147, all 20) — validated, published (artifact v9), synced here. lesson.css gained
  .boxes .good/.warn, .layers span, .vs panels, .pill g/y/r (see 'additions for Books 5-6' at the end of the file).
  tools/validate.py checks tags, links, diagram, quiz count, done section, css vars: run
  PYTHONIOENCODING=utf-8 python tools/validate.py ai-handbook/lessons
DONE: Book 6 (days 148..182, all 25) — validated, published (artifact v10), synced here.

STATUS: ALL 130 LESSON PAGES COMPLETE. 'coming soon' count = 0. Every day in index.html links to lessons/day-NN.html.
Remaining work, if any, is maintenance: fix typos, re-verify external links/videos periodically, update numbers.
Exact per-day titles, tasks and quiz Q/A for every remaining day are in tools/daily_plan.py (PLAN dict).
Each lesson must teach the content of that day's task list and end with that day's quiz among its checkpoint questions.

## Lesson page template (copy an existing day-NN.html; keep this structure exactly)
- <!doctype html> full document; <title>Day N · Title</title>; Google Fonts link; <link rel="stylesheet" href="lesson.css">
- <body data-b="B"> where B = book number (sets accent colour)
- <header class="top"> with: <button class="back" onclick="history.back()">← Back to the plan</button>,
  <span class="crumb">Book B · Week W · Day N</span>, <nav class="dnav"> prev/next lesson links (day-NN.html)
- <main class="wrap">
  - <header class="lh">: eyebrow (Kind · hours · weekday), h1, lede, .goal box, <ol class="tl"> timeline
  - <section class="pic">: 1–2 <div class="dg"> "Picture of the day" diagrams (REQUIRED on every page)
  - numbered <section> parts: <div class="sec-h"><span class="n">1</span><h2>…</h2><small>mins</small></div>
    content: p, ul, .tbl tables, pre.code (spans .k keyword, .cm comment), .steps ol, .note / .note.warn,
    .csharp two-column, .vids with .vid cards (ONLY verified videos, list below), .dg diagrams anywhere
  - "Common mistakes" <ul class="pits">
  - "Checkpoint" <div class="quiz"> with 6 <details class="q"><summary>Q</summary><p>A</p></details>
    (one of them is the day's quiz from daily_plan.py)
  - <section id="done"> <ul class="check"> 5–6 checkbox items, then <nav class="pager"> prev/next
- Last day of a book: next link is ../index.html#book-(B+1); first day of a book: prev is previous day.

## Diagram kit (in lesson.css; NO Mermaid — user found it hard to read)
.dg (card) > .dg-t (title) + content + .dg-cap (caption; <b> for the takeaway)
.flow (horizontal boxes; .keep prevents stacking on phones) > .node (+ .hl key step, .you your code,
  .model the model, .data data/files, .bad/.good/.warn, .ghost dashed, .wide) separated by <div class="arr"></div>
  (.arr data-l="label" for labelled arrows); .flow.col vertical; .loop dashed loop note
.layers (stacked rows; .hl/.you/.data), .boxes (grid of cards), .vs (left | arrow | right),
.lanes > .lane (label + bar), .bars > .bar (.bl label, .bt > i style="--v:NN%" [.alt .bad .good .warn .gap], .bv value),
.stackbar > i style="--v:..;--m:.." , .heat table (td style="--m:NN%", td.hi), .ladder > div (<b>n</b><span>),
.tokens > span, .legend > span > i.you/.model/.data/.hl/.bad, .svgbox > inline <svg> (theme colours via var(--c1..c6), var(--ink), var(--soft))
Colour meaning convention: green-tinted = your code, blue-tinted = the model, amber = data/files, solid = key step.

## Verified YouTube videos (oEmbed-checked; use only these or re-verify new ones)
x7X9w_GIm1s Fireship Python in 100s · 3dt4OGnU5sM Corey comprehensions · daefaLgNkw0 Corey dicts ·
W8KRzm-HUcc Corey lists/tuples/sets · ZDa-Z5JzLYM Corey OOP 1 · vBH6GRJ1REM mCoding dataclasses ·
xvb5hGLoK0A ArjanCodes Protocol vs ABC · q5uM4VKywbA Corey CSV · 6tNS--WetLI Corey unittest ·
cHYq1MRoyI0 freeCodeCamp pytest · ULxMQ57engo ArjanCodes unit tests · ftmdDlwMwwQ mCoding async ·
GpqAQxH1Afc ArjanCodes asyncio · Vj-iU-8_xLs ArjanCodes Pydantic · tLKKmouUams freeCodeCamp FastAPI ·
0sOvCWFmrtA freeCodeCamp API dev 19h · zjkBMFhNj_g Karpathy intro LLMs · 7xTGNNLPyMI Karpathy deep dive ·
zduSFxRajkE Karpathy tokenizer · wjZofJX0v4M 3B1B transformers · eMlx5fFNoYc 3B1B attention ·
9-Jl0dxWQs8 3B1B facts · zxQyTK8quyY StatQuest transformers · kCc8FmEb1nY Karpathy build GPT ·
NIWwJbo-9_8 Corey try/except · nghuHvKLhJA Corey f-strings · bD05uGo_sVI Corey generators ·
-aKFBoZpiqA Corey context managers · FsAPt_9Bf3U Corey decorators · Kg1Yvry_Ydk Corey venv ·
5cvM-crlDvg Corey str/repr · DZwmZ8Usvnk Corey conditionals · 6iF8Xb7Z3wQ Corey loops ·
9Os0o3wzS_I Corey functions · k9TUPpGqYTo Corey strings · khKv-8q7YmY Corey ints/floats ·
CqvZ3vGoGs0 Corey modules · YYXdXT2l-Gg Corey install · jTYiNjvnHZY Corey iterators ·
T-D1OfcDW1M IBM RAG · klTvEwg3oJ4 Fireship vector DBs · 8OJC21T2SL4 Kamradt text splitting ·
LCEmiRjPEtQ Karpathy Software 3.0 (YC) · 1bUy-1hGZpI IBM LangChain · 00Q0G84kq3M IBM RAG vs fine-tuning ·
F8NKVhkZZWI IBM AI agents · iYr1xZn26R8 Chris Alexiuk LoRA · eur8dUO9mvE IBM MCP ·
jkrNMKz9pWU Jeremy Howard Hackers' Guide · WO2X3oZEJOA Computerphile glitch tokens ·
Gjnup-PuquQ Fireship Docker · sal78ACtGTc Andrew Ng agentic workflows (Sequoia) ·
qYNweeDHiyU IBM AI/ML/DL/GenAI · 5sLYAQS9sWQ IBM how LLMs work · bZQun8Y4L2A Karpathy State of GPT ·
2TJxpyO3ei4 pixegami RAG tutorial · eBVi_sLaYsc YC vertical agents
Verify any new ID: curl "https://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=ID&format=json"

## Build / validate / publish procedure (after writing lesson pages)
1. python tools/daily_plan.py ai-handbook/parts        (re-renders plan; adds lesson links for existing files)
2. cat parts/00-head.html parts/10-shelf.html parts/11-book1.html ... parts/16-book6.html parts/99-tail-v2.html > ai-engineer-handbook.html
3. Validate every lessons/day-*.html: balanced tags (HTMLParser stack check), prev/next links exist,
   has class="dg", >=5 details.q, id="done". Validate main page tags and that every lessons/ href exists.
   node -e parse check on the main page <script>.
4. Artifact publish: file_path = ai-engineer-handbook.html, root = ai-handbook folder,
   files = ["lessons/day-NN.html", ...] for new/changed pages (+ "lessons/lesson.css" if changed).
5. Rebuild Documents\index.html: strip the claude:viewport-fit-sides meta, insert "</head>\n<body>" before
   <header class="top">, prepend doctype/head skeleton (charset, viewport, base reset), append </body></html>;
   copy lessons\ and source\.

## Style notes from the user
- Visual over prose: diagrams, tables, bars; short captions. Every page opens with a picture.
- No Mermaid. Hand-built CSS/SVG diagrams only.
- Windows/PowerShell commands; C# comparisons; accounting/finance examples (invoices, tenants, MSAs).
- Honest about numbers: illustrative figures are labelled as such; prices are "assumed, check current pricing".
- Videos must be verified to exist; never invent IDs.
