# explain

An agent skill that teaches any subject as a **concept ladder**: a numbered climb of one-sentence rungs, where each rung adds exactly one new idea on top of the rungs below it. The reader climbs one small step at a time, never holding too much at once, and never jumping ahead to understand the step they are on.

The output is a single self-contained HTML page (all CSS and JS inline, no network dependency) that the agent hands back as a local file or a localhost URL.

## Install

```bash
npx skills add danjutan/explain
```

Works with Claude Code and any other agent supported by [`npx skills`](https://github.com/vercel-labs/skills).

## Use

```
/explain why does ice float?
/explain how our auth middleware validates sessions
/explain            (no argument: explains the thing just worked on)
```

The skill dispatches the heavy work to a **background agent**, so your session's context does not grow while the explainer is built. The invoking session resolves the subject (plus any session-specific pointers), launches the agent, and hands off the finished file; the agent grounds and builds:

1. **Ground** (agent). For a repo subject it reads the actual files and runs commands; for a general concept it verifies anything uncertain with web search. Every claim in the ladder must trace to something verified.
2. **Build** (agent). It fills an HTML scaffold with rungs following the method in [`ladder.md`](skills/explain/ladder.md): bite-sized, self-contained, building; terms introduced before they are used; inline SVG diagrams only where words genuinely cannot carry the picture.
3. **Hand off** (session). On a machine with a local browser it hands you the `file://` path; on a remote or headless box it serves the explainer directory on localhost 8888 and hands you the URL (or, if another process holds that port, hands you the file path instead).

## Where explainers go

Explainers land in: `~/.claude/explainers/`, regardless of which project or agent you run the skill from. If you view them as a project artifact, feel free to make them land in the current project directory.

## Files

- [`skills/explain/SKILL.md`](skills/explain/SKILL.md): the skill entry point (the dispatcher that launches the background agent)
- [`skills/explain/build.md`](skills/explain/build.md): the agent's complete task (ground, build, save)
- [`skills/explain/ladder.md`](skills/explain/ladder.md): the ladder method, with a worked example
- [`skills/explain/scaffold.html`](skills/explain/scaffold.html): the page template

## License

[MIT](LICENSE)
