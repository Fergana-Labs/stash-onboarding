# Stash memory skills

These skills build a personal memory wiki out of existing data: your
agent sessions and your connected integrations.

The problem we solve: every new agent session starts from zero, so you
keep re-explaining context and conventions. These skills compile that 
context, keep it current, and route agents to the right information.

## Start with one prompt

Paste this into any coding agent that can run shell commands such as Claude Code,
or Codex.

```text
Set up my Stash memory. Clone https://github.com/Fergana-Labs/stash-onboarding.git
into a temp directory, read skills/stash-onboard-memory/SKILL.md there along with
every reference and asset it links, then follow it end to end — interview me,
inventory my sources, and build the wiki. When you finish, offer to copy the
skills into ~/.claude/skills and ~/.agents/skills so they load in future sessions.
```

Before you start, connect the integrations you want the wiki built from such as Slack,
Drive, Notion, or GitHub, to that agent. The skill can only inventory sources the agent
is already connected to. 

The agent will interview you, survey every source, and run a full
curation pass.

## The loop

```
onboard ──▶ onboarding brief ──▶ curate ──▶ memory wiki ──▶ use
                                    ▲                        │
                                    └──── updated data ◀─────┘
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

There are three folders mapping to the types of memory in neuroscience: **terms (semantic)** answer *what is this thing?*,
**events (episodic)** answer *what happened?*, **procedures (procedural)** answer *how do we do this?*

The wiki is derived so that raw sources stay authoritative, and claims cite the records they came from. It can best be 
thought of as an index, reasoning cache, or contextual meta-data over your data sources. 

## Install in your agent

The one-prompt path above is enough to build the wiki. Install the skills when
you want them loaded in every session.

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

## Once installed

Run `stash-onboard-memory` if you haven't built a wiki yet. This will walk you through installation and curation of your knowledge base.

## How it decides what is true

- Your explicit corrections outrank everything. Then your statements, then
  approved source records, then agent output you accepted, then agent proposals
  — which stay labeled as proposals.
- The assistant half of a transcript is not ground truth. Extraction reads your
  turns first.
- Newest *applicable* evidence wins, not the newest timestamp.
- Absence from the wiki is never evidence of absence. Coverage gaps get named,
  not smoothed over.
