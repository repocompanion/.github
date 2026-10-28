<div align="center">

# Repo Companion

**Docs your coding agent can actually find.**

Git-backed documentation and guidance for coding agents, reviewed through GitHub
pull requests.

[Website](https://repocompanion.com) ·
[Docs](https://repocompanion.com/docs/) ·
[Install](https://repocompanion.com/install/) ·
[Demo](https://repocompanion.com/mcp/) ·
[Discussions](https://github.com/repocompanion/companion/discussions)

[![Latest release](https://img.shields.io/github/v/release/repocompanion/companion?include_prereleases&style=flat-square&label=release)](https://github.com/repocompanion/companion/releases/latest)
[![License](https://img.shields.io/github/license/repocompanion/companion?style=flat-square)](https://github.com/repocompanion/companion/blob/main/LICENSE)
[![Go](https://img.shields.io/github/go-mod/go-version/repocompanion/companion?style=flat-square)](https://github.com/repocompanion/companion/blob/main/go.mod)

</div>

---

Agents can write code. They cannot know your team's patterns, decisions, or
standards unless those docs are somewhere they can find — and someone keeps
them true.

Repo Companion keeps that knowledge in **one central Git repository**. The
`companion` CLI and MCP server answer *“what guidance applies to this task?”*
with ranked, cited documents. When something is missing or wrong, an agent
proposes a change through the same reviewed pull-request workflow humans use.

**Agents propose. Humans merge.**

## How it works

1. **Ask.** `companion context` resolves the project, team, and languages.
   `companion guidance "implement an SQS consumer in Go"` ranks the patterns,
   ADRs, and standards that apply.
2. **Edit.** Each change gets a branch, a worktree, and a draft PR. A local
   overlay makes pending documents visible to search and guidance.
3. **Review.** `companion change submit` lints the docs, validates code
   references, and marks the PR ready. A human merges under branch protection.

```text
CLI / MCP client
      │
      ▼
read-only mirror ──► changeset worktree ──► draft PR ──► human review & merge
```

## Install

Homebrew installs the `companion` binary on macOS (Intel and Apple Silicon) and
Linux (x86_64 and arm64):

```bash
brew install repocompanion/tap/repo-companion
companion version
```

Prebuilt archives for macOS, Linux, and Windows are on
[Releases](https://github.com/repocompanion/companion/releases/latest). You can
also [`go install`](https://github.com/repocompanion/companion#go-install) it or
[build from source](https://github.com/repocompanion/companion#build-from-source).

## Try it offline

The demo creates a throwaway docs store, a small Go repository, and a changeset.
It needs no GitHub account, token, or network access.

```bash
git clone https://github.com/repocompanion/companion.git
cd companion
make build
bash docs/demo-cli-only.sh
```

## Connect an agent

The MCP server runs over stdio. No port is opened and no daemon is started.

```bash
claude mcp add --scope user companion -- companion mcp
```

Claude Code, Cursor, and any MCP client work. For agents without MCP,
`companion export` writes a managed `AGENTS.md` block, an `llms.txt`, or a
JSON/Markdown context bundle.

## What is in the box

- **One central store** with `org/`, `teams/`, and
  `projects/<owner>/<repo>/` areas.
- **Guidance, not grep** — task-ranked patterns, ADRs, and standards with
  project → team → org precedence.
- **Local BM25 search** with snippets, line numbers, and matched terms.
- **Code references** validated against the repository, with drift warnings. Go
  is supported natively; other languages use optional Universal Ctags.
- **Explicit changesets** — no background sync, polling, or auto-push.
- **MCP tools** for context, guidance, docs, changesets, reviews, code maps,
  and pull requests.
- **Local-first** — no daemon, no telemetry, no open port.

## Safety model

- `main` is read-only locally and protected on GitHub.
- Every write is committed immediately and scanned for likely secrets.
- Paths reject traversal, `.git`, and symlink escapes; `base_rev` blocks stale
  writes.
- Agents can never merge.

## Repositories

| Repository | What it is |
|---|---|
| [companion](https://github.com/repocompanion/companion) | CLI, MCP server, and documentation |
| [homebrew-tap](https://github.com/repocompanion/homebrew-tap) | Homebrew formula for `repo-companion` |
| [.github](https://github.com/repocompanion/.github) | Organization profile (this repository) |

## Status

**v0.2, pre-1.0.** The core workflow is usable, but interfaces may change
between minor releases. The PR workflow is GitHub-only today. There is no web
UI, semantic search, or background daemon — by design.

See the [roadmap](https://github.com/repocompanion/companion/blob/main/ROADMAP.md),
[versioning policy](https://github.com/repocompanion/companion/blob/main/VERSIONING.md),
and [changelog](https://github.com/repocompanion/companion/blob/main/CHANGELOG.md).

## Contributing

Contributions are welcome. Read
[CONTRIBUTING.md](https://github.com/repocompanion/companion/blob/main/CONTRIBUTING.md)
and the
[Code of Conduct](https://github.com/repocompanion/companion/blob/main/CODE_OF_CONDUCT.md).
Questions and design discussion belong in
[Discussions](https://github.com/repocompanion/companion/discussions);
reproducible bugs belong in the issue tracker. Report security issues privately
through [SECURITY.md](https://github.com/repocompanion/companion/blob/main/SECURITY.md),
never in a public issue.

<div align="center">
<sub>Apache-2.0 · Built with Go · Docs in Git, review in PRs, humans in charge.</sub>
</div>
