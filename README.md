# GitHub Librarian

Researches GitHub repos via the `gh` CLI and returns concise, path-first findings with line-ranged evidence.

## What it does

When the answer to a question likely lives in one or more GitHub repos and you don't want exploratory `gh search`, tree probes, and file reads polluting your main session, github-librarian takes that work elsewhere — to an isolated subagent when one's available — and reports back with concise path-first findings. It:

- Runs targeted `gh search code`, tree, and contents API calls in a fresh `/tmp` workspace
- Caches only the files needed to prove an answer
- Cites code locations as `path:lineStart-lineEnd` from real file content (never from search snippets alone)
- Returns a compact Markdown report with Summary, Locations, Evidence, and Searched sections
- Aims for ≤10 tool calls per investigation

## Installation

Two install paths exist. They are **not** equivalent — pick based on your harness.

### As a Claude Code plugin (real subagent isolation)

If you're on Claude Code, install via the marketplace. This wires up the `github-librarian` agent and `/github-librarian` slash command, and uses Claude Code's built-in Task subagent so the investigation runs in a separate context — `gh` responses, cached files, and tree dumps stay out of your main conversation.

```shell
/plugin marketplace add diegopetrucci/ai-agents-skills
/plugin install github-librarian@diegopetrucci-claude-plugins
```

### As a skill via `npx skills`

For all other harnesses, use `npx`:

```bash
npx skills add https://github.com/diegopetrucci/github-librarian --skill github-librarian
```

The skill's `SKILL.md` will delegate to a Task / general-purpose subagent if one is available, and fall back to running inline in your session otherwise. **In the inline-fallback case there is no context isolation** — every `gh` response and file Read lands in the main conversation.

## Usage

- **Claude Code:** `/github-librarian <query>` — pass scope hints (repo names, owners, refs, paths) inline when you have them.
- Or invoke the `github-librarian` subagent directly via the Task tool.

Example:

```
/github-librarian where does anthropics/claude-code define the marketplace.json schema?
```

## More Skills Like This

Found this skill useful? Browse all my hand-crafted ones in the [AI Agents skills](https://github.com/diegopetrucci/ai-agents-skills) repo.

## License

MIT
