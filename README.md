# GitHub Librarian

An [agent skill](https://agentskills.io/home) that spawns an isolated subagent to investigate GitHub repositories via the `gh` CLI and return concise, path-first findings with line-ranged evidence.

## What it does

When the answer to a question likely lives in one or more GitHub repos and you don't want to burn turns on exploratory `gh search`, tree probes, and file reads in your main session, this skill delegates the search to an isolated subagent. It:

- Runs targeted `gh search code`, tree, and contents API calls in a fresh `/tmp` workspace
- Caches only the files needed to prove an answer
- Cites code locations as `path:lineStart-lineEnd` from real file content (never from search snippets alone)
- Returns a compact Markdown report with Summary, Locations, Evidence, and Searched sections
- Aims for ≤10 tool calls per investigation

## Installation

### As a Claude Code plugin

```shell
/plugin marketplace add diegopetrucci/ai-agents-skills
/plugin install github-librarian@diegopetrucci-claude-plugins
```

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
