# Project template with agent guides

**Start a new project here** with the `agent-guides` bundle already in place: the method its coding
sessions follow, the engineering knowledge they consult, and the tool that checks both, in `.agents/`.
Replace this file with your project's own read-me once the bootstrap has run.

## What it holds

| Path | What it is | Whose |
|---|---|---|
| `.agents/` | the bundle's release, exactly as `bundle.py export` writes it; its version is in `.agents/README.md` | the release: never edited here |
| `.claude/agents/knowledge-reviewer.md` | the reviewer subagent, copied from `.agents/agents/`, run only on request | the release |
| `.github/workflows/agents.yml` | CI: `bundle.py verify` and the checksums | this project |
| `.githooks/pre-commit` | the same check before every commit | this project |
| `.gitignore` | OS, editor, Python and assistant local state | this project |

**There is no `.agents/carrier.toml`, on purpose.** It holds a repository's own random id and record
(`adopted`, `adapted`, `declined`), so it is never copied from another repository: each project mints
its own at its bootstrap. Until then the CI and the hook check `.agents/` as a release
(`verify --release`), and afterwards as this project's copy (`verify`).

There is no `AGENTS.md` or `CLAUDE.md` either: the bootstrap writes them after it has asked what the
project is, read what is there and researched its stack, so that they describe this project rather
than a guess.

## Starting a project

1. **Create the repository** with *Use this template* on GitHub, and clone it.
2. **Enable the commit hook**, once per clone: `git config core.hooksPath .githooks`. The tool needs
   Python 3.11 or newer; the hook finds one when `python3` is older.
3. **Check the copy**: `python3 .agents/tools/bundle.py verify --release`.
4. **Optionally, list private terms** in `~/.config/agent-guides/private-terms.txt` (one per line,
   never committed): names that must never reach `.agents/`, such as a client or an internal host.
   `bundle.py privacy` fails on any of them.
5. **Run the bootstrap**: open Claude Code at the repository root and paste the block under
   *Paste this to start* in [`.agents/method/prompt-bootstrap.md`](.agents/method/prompt-bootstrap.md).
   It asks five questions first; in a project that is still empty, say in your answer what you are
   building, its language and framework, since there is little to read. It then mints the id
   (`bundle.py carrier-id --mint`), proposes the files (`AGENTS.md`, the decisions log, the roadmap,
   the gate) and writes them only after you approve. When it lists existing conventions, the
   workflow, the hook and the reviewer above come from this template and are the method's own
   wiring, not conventions to adopt around.
6. **Commit** the result. From then on, every session follows the session loop the root file points
   to.

## Later releases

A project started here is a carrier like any other: a newer release arrives by update
(`.agents/method/prompt-update.md`, from `.agents/incoming/`), and what the project learns goes back as
proposals (`.agents/method/prompt-harvest.md`, into `.agents/proposals/`). Never edit a file in
`.agents/` other than `carrier.toml` and your own proposals; `bundle.py verify` fails on one that
differs from its release.

This template is refreshed from each release, tagged `vX.Y.Z` with the bundle's version. A project
already started from it does not change when the template does.
