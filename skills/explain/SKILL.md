---
name: explain
description: Build a concept-ladder explainer as a self-contained HTML page, in a background agent, and hand off a working address for it.
disable-model-invocation: true
argument-hint: "What should I explain?"
---

Teach one subject as a **concept ladder**: a numbered climb of one-sentence rungs rendered as a single self-contained HTML page. The heavy work (grounding, writing) runs in a **background agent** so this session's context stays flat. Your job here is only to dispatch and then hand off the finished file; the agent's job is defined in [build.md](build.md).

**No em dashes.** Never use the em dash character (U+2014) in anything you write about this work; use a comma, colon, semicolon, parentheses, or two sentences instead. (build.md binds the agent to the same rule.)

## Settings

- `URL_TEMPLATE`: `file://{path}` — the hand-off URL.
`{path}` is the saved page's absolute path; `{filename}` is its name within `~/.claude/explainers/`. If you have server rooted at that directory, use e.g. `http://localhost:8888/{filename}`.

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

The agent reports back with the path of the saved page. Hand the user the URL formed by filling `URL_TEMPLATE` from that path, and open it with the OS opener (`xdg-open`, `open`) if one is available.

**Done when:** the user holds a working address for the page.
