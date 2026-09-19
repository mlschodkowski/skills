# Visual companion

Browser companion for mockups, diagrams, and visual options. Use it
when the user would understand the question better by seeing it than
by reading it.

Use the browser for layouts, architecture diagrams, side-by-side visual
comparisons, look-and-feel, and spatial relationships. Use the terminal
for requirements, conceptual A/B/C choices, tradeoff lists, and
technical decisions. A question *about* a UI topic is not automatically
a visual question.

## How it works

The server watches a directory for HTML files and serves the newest one.
Write HTML to `screen_dir`. The user clicks in the browser. Selections
are recorded in `state_dir/events`.

If the file starts with `<!DOCTYPE` or `<html`, the server serves it as
is (and injects the helper script). Otherwise it wraps the fragment in
the frame template. Write fragments by default.

## Start

```bash
scripts/start-server.sh --project-dir /path/to/project
```

The script prints JSON with `port`, `url`, `screen_dir`, and
`state_dir`. It also writes that JSON to `$STATE_DIR/server-info`. Tell
the user to open the URL. Pass `--project-dir` so mockups persist in
`.superpowers/brainstorm/` and survive restarts. Without it, files go
to `/tmp`. Remind the user to gitignore `.superpowers/` if needed.

Keep the server alive across turns. If the environment reaps detached
processes, launch in the foreground with the platform's background
mechanism (`--foreground` where the script supports it). If the URL is
unreachable from the browser, bind a non-loopback host:

```bash
scripts/start-server.sh \
  --project-dir /path/to/project \
  --host 0.0.0.0 \
  --url-host localhost
```

`--url-host` controls the hostname printed in the JSON.

## Loop

1. Confirm `$STATE_DIR/server-info` exists and `$STATE_DIR/server-stopped`
   does not. Restart with `start-server.sh` if needed. The server exits
   after 30 minutes idle.
2. Write a new HTML file in `screen_dir` with a semantic name
   (`layout.html`, `layout-v2.html`). Never reuse a filename. Use the
   Write tool, not a heredoc. The server serves the newest file.
3. Remind the user of the URL, say what is on screen, and end the turn.
4. On the next turn, read `$STATE_DIR/events` if it exists (JSON lines).
   The terminal message is the primary feedback; events are structured
   clicks. The last `choice` is usually the selection; the click path
   can show hesitation.
5. If feedback changes the current screen, write a new file. Only move
   on when the current step is settled.
6. When the next step does not need the browser, push a waiting screen
   so the old choice is not left up:

```html
<div style="display:flex;align-items:center;justify-content:center;min-height:60vh">
  <p class="subtitle">Continuing in terminal...</p>
</div>
```

Stop with `scripts/stop-server.sh $SESSION_DIR`. Project-dir mockups
remain in `.superpowers/brainstorm/`.

## Fragments

Write only the inner content. Example:

```html
<h2>Which layout works better?</h2>
<p class="subtitle">Consider readability and visual hierarchy</p>

<div class="options">
  <div class="option" data-choice="a" onclick="toggleSelect(this)">
    <div class="letter">A</div>
    <div class="content">
      <h3>Single Column</h3>
      <p>Clean, focused reading experience</p>
    </div>
  </div>
  <div class="option" data-choice="b" onclick="toggleSelect(this)">
    <div class="letter">B</div>
    <div class="content">
      <h3>Two Column</h3>
      <p>Sidebar navigation with main content</p>
    </div>
  </div>
</div>
```

Add `data-multiselect` on `.options` for multiple selections.

Cards:

```html
<div class="cards">
  <div class="card" data-choice="design1" onclick="toggleSelect(this)">
    <div class="card-image"><!-- mockup --></div>
    <div class="card-body">
      <h3>Name</h3>
      <p>Description</p>
    </div>
  </div>
</div>
```

Also available: `.mockup` / `.mockup-header` / `.mockup-body`, `.split`
for side-by-side, `.pros-cons`, `.mock-nav`, `.mock-sidebar`,
`.mock-content`, `.mock-button`, `.mock-input`, `.placeholder`, `.section`,
`.label`, `.subtitle`.

Scale fidelity to the question. Put the question on the page. Two to
four options. Use real content when placeholder content would hide the
issue.

Frame template: `scripts/frame-template.html`. Helper: `scripts/helper.js`.

## Events

`$STATE_DIR/events` is one JSON object per line, cleared when you push
a new screen:

```jsonl
{"type":"click","choice":"a","text":"Option A - Simple Layout","timestamp":1706000101}
```

If the file is missing, the user did not click. Use their terminal text.
