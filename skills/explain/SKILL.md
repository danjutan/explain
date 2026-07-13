---
name: explain
description: Build a concept-ladder explainer as a self-contained HTML page, in a background agent, and hand off a working address for it.
disable-model-invocation: true
argument-hint: "What should I explain?"
---

Teach one subject as a **concept ladder**: a numbered climb of one-sentence rungs rendered as a single self-contained HTML page. The heavy work (grounding, writing) runs in a **background agent** so this session's context stays flat. Your job here is only to dispatch and then hand off the finished file; the agent's job is defined in [build.md](build.md).

**No em dashes.** Never use the em dash character (U+2014) in anything you write about this work; use a comma, colon, semicolon, parentheses, or two sentences instead. (build.md binds the agent to the same rule.)

## 1. Resolve the subject and its pointers

The subject is `$ARGUMENTS`. If empty, it is the thing just worked on or discussed this session.

The agent starts blank, so collect what it cannot rediscover on its own:

- **A session subject:** the specific file paths, commands, values, and decisions from this conversation that the explanation rests on. Pointers only (paths and names), not file contents.
- **A general concept:** the subject line alone is enough.

**Done when:** you can state the subject in one line, plus every session-only pointer the agent will need.

## 2. Dispatch

Launch one background agent (in Claude Code: the Agent tool, background by default). Its prompt is exactly two things:

1. The subject and pointers from step 1.
2. The absolute path to this skill's `build.md` (prefix this skill's base directory), with the instruction: "Read this file and follow it completely; it is your entire task."

Do none of the build work yourself: no reading the subject's files, no HTML. Then tell the user the explainer is building in the background.

**Done when:** the agent is launched and the user knows it is running.

## 3. Hand off

The agent reports back with the path of the saved page. The page is fully self-contained, so the hand-off depends only on where the user's browser runs. Pick the branch that matches this session:

- **Local browser.** The user has a GUI browser on this machine: hand them the absolute file path and the matching `file://` URL, and open it with the OS opener (`xdg-open`, `open`) if one is available.

- **Remote or headless.** The session runs on a remote machine, container, or devbox that the user views through a tunnel or forwarded port. Serve `~/.claude/explainers/` on localhost **8888** if nothing is serving it yet; never fight another process for the port. Three outcomes:

  1. `curl -sf -o /dev/null http://localhost:8888/<kebab-subject>.html` succeeds: a previous run's server already covers the new file. Give the user `http://localhost:8888/<kebab-subject>.html`.
  2. That fails but `curl -s -o /dev/null http://localhost:8888/` succeeds: something else owns the port. Tell the user localhost:8888 was taken and give them the `file://` link instead.
  3. Both fail: the port is free. Start the server so it outlives the turn (in Claude Code, the Bash tool's `run_in_background`), then give the user the URL:

     ```bash
     cd ~/.claude/explainers && python3 -m http.server 8888 >/dev/null 2>&1
     ```

**Done when:** the user holds a working address for the page: a `file://` path that exists, or a localhost URL that `curl -sf` returns.
