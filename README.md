# kimi-state

> Persistent memory and state infrastructure for Kimi Code CLI.
> Adapted from [gstack](https://github.com/garrytan/gstack) and [ECC](https://github.com/affaan-m/ecc), rewritten for zero-dependency operation using Python 3 + bash.

---

## What This Is

This repo provides a portable state layer for AI agent sessions. It tracks:

- **Timeline** — session history per project (`timeline.jsonl`)
- **Learnings** — durable insights that compound across sessions (`learnings.jsonl`)
- **Reviews** — review history per branch (`<branch>-reviews.jsonl`)
- **Checkpoints** — context snapshots you can restore later (`checkpoints/`)
- **Config** — preferences persisted across sessions (`config.yaml`)

Unlike the original gstack, this requires **no Bun, no Node.js, no Claude Code**. It runs entirely on Python 3 + bash, which are already present on virtually every Linux/macOS system.

---

## Install

```bash
git clone https://github.com/kevincouton/kimi-state.git ~/.kimi-state
export PATH="$HOME/.kimi-state/bin:$PATH"
```

Add to your shell profile (`.bashrc`, `.zshrc`, etc.):

```bash
export PATH="$HOME/.kimi-state/bin:$PATH"
export KIMI_STATE_HOME="$HOME/.kimi-state"
```

---

## Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `kimi-slug` | Resolve project slug + branch from git | `eval "$(kimi-slug)"` |
| `kimi-config` | Read/write preferences | `kimi-config set proactive false` |
| `kimi-timeline-log` | Record session events | `kimi-timeline-log '{"skill":"review","event":"started"}'` |
| `kimi-learnings-log` | Save a durable insight | `kimi-learnings-log '{"type":"pitfall","key":"...","insight":"...","confidence":9}'` |
| `kimi-learnings-search` | Query past learnings | `kimi-learnings-search --limit 10` |
| `kimi-review-log` | Record review outcomes | `kimi-review-log '{"issues":3,"critical":1}'` |
| `kimi-checkpoint` | Save/restore context | `kimi-checkpoint save "mid-refactor"` |

---

## State Directory Layout

```
~/.kimi-state/
├── config.yaml
├── projects/
│   └── owner-repo/
│       ├── timeline.jsonl
│       ├── learnings.jsonl
│       ├── main-reviews.jsonl
│       └── checkpoints/
│           └── main_20260604_120000.md
└── slug-cache/
    └── _home_user_project
```

---

## Origins

- **gstack** (Garry Tan) — AI engineering workflow skills, MIT license
- **ECC** (affaan-m) — Cross-harness agent performance system, MIT license

Both were analyzed, stripped of harness-specific infrastructure (Claude Code plugins, Codex symlinks, Bun dependencies), and rewritten as portable bash utilities using Python 3 for JSON/YAML handling.

---

## License

MIT (same as gstack and ECC)
