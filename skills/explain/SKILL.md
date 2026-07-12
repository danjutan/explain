---
name: explain
description: Build a concept-ladder explainer as a self-contained HTML page and hand it off as a local file or localhost page.
disable-model-invocation: true
argument-hint: "What should I explain?"
---

Teach one subject as a **concept ladder**: a numbered climb of one-sentence rungs that each add one idea on top of the rungs below. Render it as a single self-contained HTML page and hand the user a working address for it.

**No em dashes.** Never use the em dash character (U+2014) anywhere: not in the rendered page, not in these files, not in your replies about the work. Split the thought into two sentences, or use a comma, colon, semicolon, or parentheses. This rule has no exceptions.

## 1. Scope and ground the subject

The subject is `$ARGUMENTS`. If empty, it is the thing just worked on or discussed this session.

Then **ground** it. Gather the real facts before writing a word of HTML, branching on what kind of subject it is:

- **A repo subject:** read the actual files, configs, and code the explanation rests on, and run a command if a number or behavior is in question.
- **A general concept:** rest on everyday knowledge, and use your web-search tool for anything you are not certain of.

Every claim, name, path, and number in the ladder must trace to something you verified this session.

**Done when:** you can name the concrete files, sources, and facts the ladder will be built from.

## 2. Build the ladder

Copy [scaffold.html](scaffold.html) to `~/.claude/explainers/<kebab-subject>.html` (create the directory if needed), set the `<h1>`, and fill the `<ol class="ladder">` with rungs.

Explainers are a personal reference library, not project artifacts, so they always accumulate in `~/.claude/explainers/` regardless of which project or agent you are running in.

- **Follow the method.** Build the rungs per [ladder.md](ladder.md): bite-sized, self-contained, building, starting from the floor and landing on the concept the user asked about. That file is the source of truth for what a good rung is, how to order them, length, rest markers, and when a rung needs a diagram.
- **Self-contained file.** All CSS and JS inline, no CDN or network dependency, so the page renders fully offline.
- **Concrete over abstract.** Quote the real code, paths, and values you grounded in step 1. Use inline SVG for any diagram.

**Done when:** the file is a complete ladder (no placeholder rungs, no leftover scaffold comments, no rung longer than one sentence), and `grep -c $'\u2014' <file>` prints 0.

## 3. Hand off

The page is fully self-contained, so the hand-off depends only on where the user's browser runs. Pick the branch that matches this session:

- **Local browser.** The user has a GUI browser on this machine: hand them the absolute file path and the matching `file://` URL, and open it with the OS opener (`xdg-open`, `open`) if one is available.

- **Remote or headless.** The session runs on a remote machine, container, or devbox that the user views through a tunnel or forwarded port: serve the explainer directory on localhost **8888**, reusing an existing server only if it already serves this explainer:

  ```bash
  curl -sf -o /dev/null http://localhost:8888/<kebab-subject>.html \
    || ( cd ~/.claude/explainers && python3 -m http.server 8888 >/tmp/explainer-8888.log 2>&1 & )
  ```

  Start the server in the background so it outlives the turn (in Claude Code, the Bash tool's `run_in_background`). If the start fails because another process owns 8888 (check `/tmp/explainer-8888.log`), that server has the wrong root: stop it, or serve on 8889 and adjust the URL. Then give the user the exact URL to open: `http://localhost:8888/<kebab-subject>.html`.

**Done when:** the user holds a working address for the page: a `file://` path that exists, or a localhost URL that `curl -sf` returns.
