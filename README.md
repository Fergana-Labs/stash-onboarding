# Stash memory skills

Three skills that build a personal memory wiki out of what you already do — your
agent sessions and your connected integrations — and then answer from it.

The problem they solve: every new agent session starts from zero, so you
re-explain the same customers, systems, and conventions forever. These skills
compile that context once, keep it current, and route a future agent to the
smallest page that answers the question.

## The loop

```
onboard ──▶ onboarding brief ──▶ curate ──▶ memory wiki ──▶ use
                                    ▲                        │
                                    └──── memory-inbox ◀─────┘
                                          (your corrections)
```

| Skill | What it does |
|---|---|
| `stash-onboard-memory` | Installs and verifies Stash, interviews you about the context you keep re-explaining, inventories what your integrations can actually reach, and writes the onboarding brief. Then runs the first curation pass and proves it on a question you care about. |
| `stash-curate-memory` | Surveys every reachable source and writes a source map, then fans out subagents per source and merges their proposals into one page per term, event, and procedure. Runs again incrementally as things change. |
| `stash-use-memory` | Answers from the wiki: always on for terms that carry local meaning, honest about what it doesn't know, index before page before raw source, and never writes. |

## What gets built

```
memory/
  log.md              what each curation run read and changed
  terms.md            index of every term — people, systems, projects, jargon
  data.md             where the raw data lives and how to read it
  terms/<slug>.md     one page per term
  events/             a dated timeline, one page per thing that happened
  procedures/         one page per repeatable method or policy
```

Three kinds of page, three questions: **terms** answer *what is this thing?*,
**events** answer *what happened?*, **procedures** answer *how do we do this?*

The wiki is derived and disposable — raw sources stay authoritative, and every
substantive claim cites the record it came from. Curation writes to a plain
folder; where that folder ends up living is a separate concern.

## Install

### Claude Code

```shell
/plugin marketplace add Fergana-Labs/stash-onboarding
/plugin install stash-memory@fergana-labs
/reload-plugins
```

Skills are namespaced by the plugin, so they invoke as
`/stash-memory:stash-onboard-memory`. To try it without installing, clone the
repo and run `claude --plugin-dir ./stash-onboarding`.

### Codex

Codex loads skills from `~/.agents/skills` (or `.agents/skills` in a repo). Each
skill directory goes directly under it:

```shell
git clone git@github.com:Fergana-Labs/stash-onboarding.git
cp -R stash-onboarding/skills/* ~/.agents/skills/
```

Then invoke with `$stash-onboard-memory`.

### Anything else

Each directory under `skills/` is a self-contained skill: a `SKILL.md` plus its
`references/` and `assets/`. Point any agent that reads Markdown instructions at
`SKILL.md` and it will work.

## Start here

Run `stash-onboard-memory`. It walks the whole path — install, interview, source
inventory, brief, first curation run, and a real question answered from the
result — in one session.

If you already have a brief, run `stash-curate-memory` directly and give it the
brief path and a folder to write into.

## How it decides what is true

- Your explicit corrections outrank everything. Then your statements, then
  approved source records, then agent output you accepted, then agent proposals
  — which stay labeled as proposals.
- The assistant half of a transcript is not ground truth. Extraction reads your
  turns first.
- Newest *applicable* evidence wins, not the newest timestamp.
- Absence from the wiki is never evidence of absence. Coverage gaps get named,
  not smoothed over.
