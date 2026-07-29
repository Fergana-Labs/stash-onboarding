---
name: stash-use-memory
description: Answer questions that depend on the user's own terms, people, systems, history, or working methods by reading their curated memory wiki — index first, then pages, then raw sources. Use whenever a request contains a name, acronym, project, or phrase that carries local meaning, and whenever an answer would otherwise be guessed.
---

# Use memory

The memory wiki is a compiled cache of this person's world: their terms, what
happened, and how they do things. It is small, it cites its sources, and it is
never complete. Read it before answering anything that depends on local
context.

The wiki lives in one folder — `./memory/` unless the caller says otherwise.

## What is in it

| File | What it holds |
|---|---|
| `terms.md` | Index of every term — people, systems, projects, jargon — one line each, linking to `terms/<slug>.md` |
| `events/events.md` | Reverse-chronological timeline of what happened, linking to one page per event |
| `procedures/procedures.md` | Index of repeatable methods and policies, linking to one page per procedure |
| `data.md` | Where the raw data lives: which integrations, which containers, how to read them |
| `log.md` | Curator run history — what was read and when. Coverage, not evidence |

Pages under `terms/`, `events/`, and `procedures/` carry frontmatter with
`as_of`, `status`, `aliases`, and `sources`. Lead with what a page presents as
current; history sits below it.

## 1. Always on

Any term that looks like it carries context is a lookup, not a guess. Proper
nouns, acronyms, product and project names, internal jargon, "the strategy doc",
"the usual process" — if the phrase points at something specific in this
person's world, check the wiki before answering.

Do not wait to be asked to consult memory. Do not answer from the general
meaning of a word when a local meaning may exist.

## 2. Know what you don't know

The wiki is a cache, not the world. Absence from it is not evidence of absence.

- Ask the user if there is information missing or if you are uncertain. This is especially true if a term is used in a way that doesn't make sense in context and you can't find it in the wiki. Or if there's a procedure or task that you don't have enough context to do. 
- Separate confirmed facts from proposals, drafts, and unverified mentions
- Respect `as_of`. If a page is stale relative to the question, say so and go to
  the source in `data.md`.
- When the missing piece is something the user knows — an owner, a location, a
  scope, an intended outcome — ask one precise question instead of inventing an
  answer. Then solve the request.
- When a page says its collection is source-authoritative, the named source
  decides current membership, not the page. Enumerate that container at query
  time and report any pagination or access caps.

Never present coverage as a finding. "The wiki has no page on X" is a statement
about the wiki, not about X.

## 3. Progressive disclosure

Search narrow and then widen

1. **Indexes first.** Grep or keyword-search `terms.md`, `events/events.md`, and
   `procedures/procedures.md` for the term and its plausible aliases. These
   files are small enough to read whole.
2. **Open the page** the index points at. Read one related page if the first
   names it as governing or disambiguating.
3. **Follow the term through the wiki.** Grep its name and its frontmatter
   aliases across `events/` and `procedures/` to find what happened to it and
   how it gets handled. Pages carry no backlinks — grep is the backlink.
4. **Search the whole wiki** when the indexes miss — grep across
   `terms/`, `events/`, and `procedures/` for the phrase, since a term may live
   inside a page as an alias or a mention rather than as its own entry.
5. **Go to raw sources** for freshness, a conflict, an ambiguity, or a fact
   the wiki does not carry. Use `data.md` to find the right container and read
   that container — not every connected source.

Search the user's own words first, then the canonical name. A page's
`aliases` hold the phrasings actually observed, so grep hits the page even when
the user calls it something the title never says.

Keep the mechanics out of the answer. Answer as someone who knows these things,
not as someone reporting on a filing system: never mention the wiki, its
indexes, its pages, or your search path. "There is nothing on X" — not "the
wiki has no page for X". Cite the page and, where it mattered, the raw source;
do not narrate the search.

## 4. Do not edit the wiki

Retrieval never writes. The curator is the only writer — concurrent edits
corrupt the indexes and the run log it depends on.

When the user corrects something, or confirms a fact the wiki lacks, drop a
short note for the next curation run in the inbox folder — `./memory-inbox/`
unless the caller names another, and always outside the memory root. Record what
was asked, what the wiki said, what the user confirmed, and how far the
correction applies. Nothing inside the memory root changes.

Use the correction immediately in the current conversation. It becomes canonical
only after the curator compiles it.
