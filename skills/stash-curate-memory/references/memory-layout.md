# Memory layout

```text
<memory-root>/
  log.md              append-only run history
  terms.md            index of every term, one line each
  data.md             where the data lives and how to read it
  terms/<slug>.md
  events/
    events.md         reverse-chronological timeline, one line each
    <YYYY-MM-DD>-<slug>.md
  procedures/
    procedures.md     index of every procedure, one line each
    <slug>.md
```

Slugs are kebab-case and stable. Renaming means updating the index row and
keeping the old slug as an alias — never orphan a link.

## Progressive disclosure

The three indexes plus `data.md` are all an agent should need to read before
knowing which page to open. Keep them loadable at the start of any session:
indexes under ~400 words, `data.md` under ~600, any page under ~600. An index
row is a pointer, not a summary — if it starts explaining, the explanation
belongs on the page. Group rows under headings when an index gets long; never
drop a row, since that drops the route.

## Pages

Every page under `terms/`, `events/`, and `procedures/` opens with:

```yaml
---
id: kebab-case-slug
kind: term | event | procedure
status: active | proposed | superseded | uncertain
as_of: YYYY-MM-DD
aliases: [observed alias, former slug]
sources: [stable source reference]
---
```

`as_of` is the newest effective date among the claims the page presents as
current — not the date of the run. Aliases are only forms actually observed or
confirmed by the user.

Substantive claims carry a stable source reference and its date, in whatever
form the source uses (`slack://channel/ts`, a URL, a session id and turn, a file
path). Reference at the end of a section rather than after every sentence, but a
section with no reference is not shippable. The onboarding brief is provenance
for the user's own beliefs and preferences, not for facts about the world.

## Index rows

```markdown
- [**<Term>**](terms/<slug>.md) — <one clause: what it is and why it matters here>
- **YYYY-MM-DD** — [<what happened>](<YYYY-MM-DD>-<slug>.md)
- [**<Procedure>**](<slug>.md) — <trigger>: <what it accomplishes>
```

## `data.md`

The source map. One section per source, written so a later run or subagent can
navigate without re-surveying: how to read it, its containers, visible date
range, rough volume, how to enumerate, how to query incrementally, access and
pagination limits, which of the user's priorities it bears on, and a watermark
**per container** — one noisy channel must not stall a quiet one. Date the
survey. End with a table of sources named in the brief that are not reachable
and why.

## `log.md`

Append-only, newest at the bottom, never rewritten. One entry per run:

```markdown
## Run YYYY-MM-DD HH:MM — bootstrap | update

- **Read:** <source/container: window, record count>
- **Watermarks:** <container: old -> new>
- **Created / Updated / Superseded:** <page paths, each with a phrase on what changed>
- **Open conflicts:** <page: the two claims, why unresolved>
- **Skipped:** <source/container: reason>
```

With no shared change feed behind the integrations, this log and the watermarks
are the only record of coverage. If a run dies partway, the log says where to
resume.

Nothing here is curator-only — every file is readable by a retrieving agent.
Keep scratch state outside the memory root.
