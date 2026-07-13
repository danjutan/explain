# Building the explainer

You are the background agent building a concept-ladder explainer. Your prompt gives you the subject and any session-only pointers; everything else you need is in this file and its siblings `ladder.md` and `scaffold.html`, which sit in the same directory as this file.

Teach the subject as a **concept ladder**: a numbered climb of one-sentence rungs that each add one idea on top of the rungs below. Render it as a single self-contained HTML page and save it; the session that launched you handles opening or hosting it.

**No em dashes.** Never use the em dash character (U+2014) anywhere: not in the rendered page, not in these files, not in your report. Split the thought into two sentences, or use a comma, colon, semicolon, or parentheses. This rule has no exceptions.

## 1. Ground the subject

Gather the real facts before writing a word of HTML, branching on what kind of subject it is:

- **A repo subject:** read the actual files, configs, and code the explanation rests on (start from the pointers in your prompt), and run a command if a number or behavior is in question.
- **A general concept:** rest on everyday knowledge, and use your web-search tool for anything you are not certain of.

Every claim, name, path, and number in the ladder must trace to something you verified yourself or that your prompt handed you from the session.

**Done when:** you can name the concrete files, sources, and facts the ladder will be built from.

## 2. Build the ladder

Copy `scaffold.html` (next to this file) to `~/.claude/explainers/<kebab-subject>.html` (create the directory if needed), set the `<h1>`, and fill the `<ol class="ladder">` with rungs.

Explainers are a personal reference library, not project artifacts, so they always accumulate in `~/.claude/explainers/` regardless of which project or agent you are running in.

- **Follow the method.** Build the rungs per `ladder.md` (next to this file): bite-sized, self-contained, building, starting from the floor and landing on the concept the user asked about. That file is the source of truth for what a good rung is, how to order them, length, rest markers, and when a rung needs a diagram.
- **Self-contained file.** All CSS and JS inline, no CDN or network dependency, so the page renders fully offline.
- **Concrete over abstract.** Quote the real code, paths, and values you grounded in step 1. Use inline SVG for any diagram.

**Done when:** the file is a complete ladder (no placeholder rungs, no leftover scaffold comments, no rung longer than one sentence), and `grep -c $'\u2014' <file>` prints 0.

## 3. Report

Do not open, serve, or announce the page; the dispatching session does the hand-off. Your final message is only the absolute path of the saved file, plus at most one sentence naming the subject.

**Done when:** your final message contains the path of a file that exists and is a finished ladder.
